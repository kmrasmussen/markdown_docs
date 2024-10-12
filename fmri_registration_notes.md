# fmri registration notes

* Registrations match two images, giving a correspondence between voxels
* An example is an anatomical image for a subject that is registered to MNI152
* Registrations can be linear or non-linear
* [Klein+08](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2747506/) evaluates 14 non-linear methods and ART, SyN, IRTK, and SPM's DARTEL work best.
* ANT (Advanced Normalization Tools) is part of fmriprep.
* There is info about it here [https://github.com/ANTsX/ANTs/wiki/Anatomy-of-an-antsRegistration-call](https://github.com/ANTsX/ANTs/wiki/Anatomy-of-an-antsRegistration-call)
* ANT uses rigid, then affine, then "SyN".
* It aligns at different resolutions, starting with low resolution, doing different iterations
* It takes a template .nii.gz and a t1brain nii.gz as input
* It has dimensionality paramter `--dimensionality` (to 3), could be fun to use 2d to see it more clearly
* `--winsorize-image-intensities` is used to clip values to an interval
* `--use-histogram-matching` where you make histograms of intensities for both images and match them first, off by default
* initial moving matching: match by mid-point or by center of mass or point of origin (which is given by the image headers), center of mass recommended

## Registration stages

### Rigid stage
* ``--transform Rigid[0.1]` means using rigid transform (linear or affine?) with a gradient descent step size of 0.1
* the `--metric` is used as the "loss" for how to register.
* `--metric MI[$t1brain,$template,1,32,Regular,0.25]` uses Mutual Information of histograms (for the whole image?) and can work for inter-modal (like registering functional to anatomical?). The format is [fixed, moving, parameters], so t1brain is fixed and template is moving (why not other way around?). [fixed, moving, weight, bins, sampling, samplingPercentage] for MI. So here you have weight 1 (normalized to 1), 32 bins, regular sampling, 0.25 used for sampling. Different metrics can be combined this is what weight means, so if you want more MI than CC (another metric) then you increase that value but they are normalized to 1 by the algorithm
* Yes it seems the histogram is a histogram across voxels
* `--convergence [1000x500x250x100,1e-6,10]` means that for the different scales/levels we first use 1000 then 500 then 250 and then 100 iterations for the 4 different scales. But we continue to next scale if improvement in metric is less than 1e-6 for 10 iterations.
* `--shrink-factors 8x4x2x1` means that we have 4 scales, first shinking by 8x compared to full then 4x then 2x then 1x. Notice shrinking image in 3D by 2x decreases number of voxels by 8x. So with these settings eeach level requires 8x more computation.
* `--smoothing-sigmas 3x2x1x0vox` for each scale you would want some kind of smoothing with Gaussian kernel. Here it is the kernel std deviation size in voxels. (Do you first shrink by factor 8 and then use an even larger stddev or is the stddev/voxel size measured relative to original size?)

### Affine stage
The same parameters are used here just now we are fitting an affine transformation instead of a linear transformation

### SyN
`--transform SyN[0.1,3,0] `
* The parameters inside SyN[] are: gradientStep,updateFieldVarianceInVoxelSpace,totalFieldVarianceInVoxelSpace
* Computes a gradient field (like deformation field?) for how much a voxel can move, the gradientStep determines the maximum norm of a such a movement - after each iteration (? each iteration must mean that multiple gradient fields are computed applied after each other)
* updateFieldVarianceInVoxelSpace means that after you have the gradient field you smooth it, so a value of 3 is the kernel size
* SyN stage uses cross-correlation not mutual information, CC good for intramodality: Something like: Sum over all locations x (correlation(voxel ball around x in img1, voxel ball around x in img2)) where the balls are using some radius. Actually a cube is used
* Still also here we have convergence, shink and smoothing-sigmas parameters - so multiple scales for the SyN stage too.

### Additional
* brainlesionmask will restrict computation to some area (is the registration preceded by some kind of stage where we find the area that contains the brain and not eyes and bones or whatever?)
* "antsRegistration can accept masks on the target, moving, or both images. Sometimes you may need to mask both sides with separate masks. In that case you can use something like this: # -x [$fixed_mask,$moving_mask]"
