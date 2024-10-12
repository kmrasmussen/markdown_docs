markdown
# Understanding LiDAR: A Tool for Analyzing Brain States

LiDAR (which stands for a statistical analysis approach rather than the labeling technology used in mapping) is a fascinating method for analyzing fMRI parcellated time series to understand brain states. This analysis dives deep into the momentary states the brain enters, using a series of complex transformations and clustering techniques to achieve meaningful insights.

## Breaking Down the LiDAR Method

### Step 1: Hilbert Transformation of Time Series

The first step in the LiDAR method involves the **Hilbert transformation** of each time series for various brain regions. For `n` brain regions, this transformation results in a phase and magnitude for each time series. The key output at any specific time point is an `n by n` matrix that represents the **instantaneous phase synchronization** between these brain regions.

### Step 2: Dimensionality Reduction

To manage the complexity and reduce the dimensionality of the data, we focus on the leading eigenvector of the phase synchronization matrix. This eigenvector captures the dominant aspects of instantaneous functional connectivity, transforming our data into an `n-dimensional` vector for each time point.

### Step 3: Clustering Time Points into States

We then cluster these vectors, each representing a time point, into different states. The assumption is that brain activity does not move in a completely continuous space but rather transitions between discrete states. The clustering helps us identify these states.

### Step 4: Analyzing State Transitions

Once clustering is complete and different states are identified, transitions between them can be analyzed. We can create a transition matrix to understand the probability of moving from one state to another. However, in the LiDAR-PMS approach, the focus is more on the time spent in each state rather than these transitions. By counting the number of time points in each state, we can determine the probability of being in each state, forming what is known as the **Probability Mass Function (PMF)**.

## Applying LiDAR in Simulations

The process doesn't end with analyzing real brain data. To validate and understand the robustness of our findings, we can simulate brain activity:

1. **Simulation of Brain Regions**: Generate time series for simulated brain regions.
2. **Repeat the Analysis**: Apply Hilbert transformation, compute eigenvectors, and assign states to each time point in the simulated data.
3. **Compute Simulated PMS**: Compare the simulated PMS (Probability Mass Function of States) to the real data's PMS.

### Why Use PMS?

One question that arises is why this specific statistic, the PMS, is more effective for fitting a brain model than other statistics. For instance, wouldn't a non-dynamic functional connectivity measure be sufficient? It's critical to ensure the PMS's reproducibility and validity. To do this, data size requirements need to be estimated and validated, potentially using extensive population-level datasets, such as those from the Human Connectome Project (HCP).

## Ensuring Robustness and Reproducibility

### Challenges with PMF Consistency

A significant challenge is ensuring that the clusters we define in our analysis remain consistent across different subsets of data:

- **Variable Clustering**: If the clustering is performed on different subsets of sessions, the clusters might differ. This inconsistency can hinder the reproducibility of the PMF.
- **Use of Adjusted Rand Index**: To counter this, metrics like the adjusted Rand index could be useful. This index can provide a measure of similarity between two clustering results, even if the number of clusters or their labels differ.

### Practical Analysis Strategy

A possible approach is to perform clustering on increasing sizes of data subsets and compare the results with a holdout set. This helps determine the data size required to achieve consistent clustering and, hence, a reliable PMF.

## Conclusion

LiDAR offers a powerful framework for analyzing and simulating brain states through fMRI time series data. Its application spans from real-time data analysis to creating robust simulations, providing insightful metrics like the Probability Mass Function of States. By addressing challenges in reproducibility and leveraging comprehensive datasets, LiDAR enables a deeper understanding of the dynamic nature of brain activity.

