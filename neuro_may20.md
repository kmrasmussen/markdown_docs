# Neurostuff May 20

## The problem with the esfmri data
The main problem with working with the esfmri data is that even though we have a lot of subjects, each subject has a unique electrode placement. This means that if we fit a whole-brain model to the preop (either group level or subject), and try to stimulate the model to change the dynamics to resemble the postop-stimulation-active state for a specific subject, we are limited by the small amount of postop timepoints we have for this subject.

How much is enough data? It is not clear how this is evaluated.

The problem is that if we proceeded while dealing with this problem we are tackling two problems at once: The problem we are mainly interested in; using recordings from actual causal intervention through stimulation to evaluate the usefulness of whole-brain-models and the ability to simulate stimulation on such a model. This problem would be tackled at the same time as dealing with a general and probably more 

## Idea Scaling laws for simple statistics of fmri data
The simplest thing you can do, is to take MyConnectome fmri data (openneuro) and then scale the amount of fmri data you use and look at
what happens to the statistics, for example, when does the functional connectivity matrix (non-dynamic) start to converge.

The problem here would be that non-dynamic FC matrices are overrated because they hide the dynamic stuff.

Alternatively other statistics such as the LEIDA + clustering + occupancy distribution statistics from the Deco-derived papers.

## Bootstrapping for robustness


## Idea Classifer + model
Instead of saying for example that you are making significance tests based on permutations of HT2A neurotransmitter density maps and
saying that this means your whole-brain models incoorporates HT2A well and that this is evidence of the importance of HT2A, you could try to
first fit PLCB vs DRUG classifiers on the data (eg FC matrices) and then afterways for evaluating whole-brain model you would then simulate
FC matrix and see what the classifier says.

