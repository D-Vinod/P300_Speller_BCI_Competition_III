# Implementation of "Ensemble of SVMs for BCI P300 Speller"

## Project Overview
This project implements the methodology outlined in the paper "BCI Competition III: Dataset II - Ensemble of SVMs for BCI P300 Speller" by Rakotomamonjy and Guigue. The approach combines an ensemble of support vector machines (SVMs) and recursive channel elimination to improve P300 classification accuracy, as demonstrated on EEG datasets from the BCI Competition III.

## Files and Directories
- **`data/`**: Contains the dataset used for the implementation (BCI Competition III Dataset II).
- **`scripts/`**: Includes the implementation scripts for preprocessing, training, and evaluation.
- **`results/`**: Stores the output results, figures, and performance metrics.
- **`README.md`**: This file, providing a detailed overview of the project.

## Dataset
The dataset includes EEG recordings from 64 channels for two subjects performing P300 speller tasks. Key features of the dataset:
- **Subjects**: A and B.
- **Recording Setup**: 64-channel EEG with a sampling rate of 240 Hz.
- **Structure**:
  - 85 characters x 7794 samples x 64 channels.
  - Binary labels indicating the presence (1) or absence (0) of the P300 response.

For more details, visit: [BCI Competition III Dataset II](https://www.bbci.de/competition/iii/#data_set_ii).

## Methodology
The implementation comprises three main stages:
1. **Data Preprocessing**
   - **Windowing**: Extract 0 to 667 ms post-stimulus intervals.
   - **Filtering**: Apply a 4th-order Chebyshev bandpass filter (0.1–10 Hz).
   - **Feature Vectoring**: Concatenate decimated samples (14 per channel) into a single feature vector.

2. **Model Training**
   - Train 15 SVM classifiers on partitioned subsets of the training data.
   - Perform channel ranking to identify the most effective channels.
   - Fine-tune the regularization parameter (C).

3. **Character Prediction**
   - Use a double-averaging strategy on decision scores to identify target rows and columns.

## Implementation Details
- **Training Data Partitioning**: The dataset is divided into 15 partitions of five consecutive character epochs each.
- **Channel Ranking**: Channels are ranked based on their contribution to classification accuracy.
- **Parameter Fine-Tuning**: The optimal C parameter is identified from a predefined range ([0.01, 0.05, 0.1, 0.5, 1.0]).

## Results
- **Accuracy Before Fine-Tuning**: 80.5% using all 64 channels.
- **Accuracy After Fine-Tuning**: 85.4% using optimized channels.
- **Channel Selection**: Top 12 channels were found sufficient for accurate classification.
- **Limitations**:
  - Computational constraints limited testing to subsets of the data.
  - Lower accuracy compared to the paper’s results (96.5%) due to limited testing.

## Challenges and Improvements
1. **Channel Ranking**: Future work could explore dynamic ranking methods.
2. **Testing Data**: Incorporate datasets with labeled test samples to assess generalization.
3. **Partitioning**: Optimize data partitioning to improve ensemble performance.
4. **Inter-Subject Variability**: Explore transfer learning to enhance generalizability across users.

## References
1. Rakotomamonjy, A., & Guigue, V. (2008). BCI Competition III: Dataset II - Ensemble of SVMs for BCI P300 Speller. IEEE Transactions on Biomedical Engineering, 55(3), 1147–1154. [DOI](https://doi.org/10.1109/tbme.2008.915728).
2. Farwell, L. A., & Donchin, E. (1988). Talking off the top of your head: toward a mental prosthesis utilizing event-related brain potentials. Electroencephalography and Clinical Neurophysiology, 70(6), 510–523.

---

## Contact
For further inquiries or collaboration, please contact:
- **D.M.D.V. Bandara**
- **A.T.P. Amarasekara**
Department of Electronic and Telecommunication Engineering  
University of Moratuwa  
December 18, 2024

