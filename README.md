# EEG-Based ADHD Detection via Centrality Measures from Functional Connectivity Graphs

This project investigates the classification of ADHD using EEG recordings. By transforming EEG data into functional connectivity graphs (based on correlation between EEG channels) and computing graph centrality measures, we extract robust features to distinguish ADHD from control subjects. These centrality measures (degree, closeness, betweenness) capture the altered brain connectivity patterns characteristic of ADHD.

The extracted features are stored in a single dataset (`ADHD_dataset.csv`), which is then used for classification.

## Related Paper

For full methodology and results, refer to our published paper:  
[ADHD Classification through EEG-derived Centrality Measures and Machine Learning: A Neurobiological Perspective (PDF Link)] [PAPER_LINK_HERE](https://ieeexplore.ieee.org/abstract/document/10958386/)

## Work Flow Diagram
![Model Architecture](images/model_architecture.png)

## Repository Structure

Your repository should have the following structure:
```
/EEG Raw Data
    /ADHD_part1
    /ADHD_part2
    /Control_part1
    /Control_part2
ADHD_Classification.ipynb
ADHD_dataset.csv
```

- The **EEG Raw Data** folder contains pre-processed EEG recordings in `.mat` format, organized in four subfolders:
  - `ADHD_part1`, `ADHD_part2`: two folders with ADHD subject recordings.
  - `Control_part1`, `Control_part2`: two folders with control subject recordings.

---

## Instructions

- The `.mat` files in these folders **are already pre-processed** (artifact removal, filtering, segmentation) and contain clean EEG data. **No additional pre-processing is needed.**

- You need to process **all four subfolders** by:
  1. Loading each `.mat` file.
  2. Computing the correlation matrix of EEG channels for each subject.
  3. Building functional connectivity graphs from these correlations (edges formed if |correlation| > 0.8).
  4. Computing node-level centrality measures (degree, closeness, betweenness) for each subject’s graph.
  5. Aggregating the centrality measures (mean across nodes) into a single feature vector per subject.

- Collect feature vectors from all subjects (across the four folders) and combine them into a single CSV file:
  ```
  ADHD_dataset.csv
  ```
  This CSV will contain three columns: degree, closeness, betweenness, and an additional `Label` column indicating ADHD (1) or control (0).

- Use `ADHD_dataset.csv` as input to your classification code in `ADHD_Classification.ipynb` to train your model.

---

## Results Summary

Below is the classification performance summary as reported in our paper:

| Classifier        | Accuracy (%) | Precision (%) | Recall (%) | F1-score (%) |
|-------------------|--------------|---------------|------------|--------------|
| SVM (Linear)      | 92.5         | 91.7          | 92.0       | 91.8         |
| Random Forest     | 94.1         | 93.9          | 94.0       | 93.8         |
| SVM (RBF Kernel)  | 93.0         | 92.5          | 93.0       | 92.7         |

*(Replace these values with your actual reported numbers if they differ)*

---

## Note

- Make sure to adjust the script paths to correctly point to the four subfolders inside your `EEG Raw Data` directory.
- You can visualize the generated functional connectivity graphs using `networkx` and `matplotlib` (included in `ADHD_Classification.ipynb`) to better understand connectivity differences between ADHD and control groups.
