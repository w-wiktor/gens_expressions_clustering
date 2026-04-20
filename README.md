# 🧬 Comprehensive Project Report: Gene Expression Time-Series Clustering

## 🎯 Project Objective
The primary goal of this study was to identify distinct patterns of gene expression across seven sequential time points. By using unsupervised machine learning, we aimed to categorize genes based on their dynamic behavior (their 'profile') rather than their absolute expression magnitude.

## 📊 Data Engineering & Preprocessing
A critical challenge in this dataset was the presence of missing values. We implemented two distinct strategies: 
1.  **Full Dataset Preservation (Imputation):** To maximize statistical power, we applied **linear interpolation** followed by a median fill for any remaining NaNs. This allowed us to retain the full set of **614 genes**.
2.  **Normalization:** We applied `StandardScaler` to the profiles. This step is crucial because it ensures the clustering algorithm groups genes that share the same *trend* (e.g., rising or falling together) regardless of whether one gene has a much higher baseline expression than another.

## 🛠 Methodology
- **Dimensionality Reduction:** PCA was used to map the 7-dimensional time data into 2D space, allowing us to visually verify that the clusters were naturally separating.
- **Optimal K Selection:** We used the **Elbow Method** (tracking 'Inertia') and **Silhouette Analysis**. While a binary split (k=2) was mathematically strong, **k=3** was selected because it provided a more nuanced and biologically relevant classification of the gene responses.

## 📈 Detailed Cluster Results
With the K-Means model set to 3 clusters, we observed the following behaviors:

*   **Cluster 0: The Baseline Group (n=345)**
    - **Behavior:** These genes show relatively flat or 'noisy' horizontal profiles.
    - **Interpretation:** Likely representing 'housekeeping' genes that maintain constant activity levels during the observed period.

*   **Cluster 1: The Early Responders (n=180)**
    - **Behavior:** This group shows high variability in the early time points, often with a slight downward trend or transient fluctuations.
    - **Interpretation:** Genes that are involved in the immediate reaction to the initial stimulus but stabilize or deactivate as time progresses.

*   **Cluster 2: The Activated Group (n=89)**
    - **Behavior:** A very distinct and consistent upward trend across the time series.
    - **Interpretation:** Genes that are being progressively 'turned on' or upregulated, representing the core biological response being studied.

## ⚙️ Implementation & Deployment
To make this analysis actionable, we implemented a **Prediction System**. The `predict_gene_cluster` function allows researchers to input a new 7-point expression sequence; the system automatically scales the data and assigns it to one of the three established biological profiles in real-time.

## 🧠 Final Conclusion
By moving from data deletion to **imputation**, we successfully analyzed 63% more genes than the initial attempt. The transition to a 3-cluster model provided a significantly clearer picture of the 'Strong Activation' group (Cluster 2), which is often the primary focus in genetic research.
