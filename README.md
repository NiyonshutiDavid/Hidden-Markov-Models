# Hidden Markov Models for Human Activity Recognition

HMM for recognizing human activities from accelerometer and gyroscope data.

**Team**: Afsa Umutoniwase, David Niyonshuti

## Project Overview

Building an HMM to detect activity states (standing, walking, jumping, still) from sensor measurements.

## Dataset

- **Total Samples**: 50 recordings
- **Activities**: Standing (13), Walking (12), Jumping (13), Still (12)
- **Total Duration**: >6 minutes across all activities
- **Devices**: iPhone 11 Pro + Samsung Galaxy S23
- **Sampling Rate**: 100 Hz (harmonized)
- **Format**: CSV files containing accelerometer, gyroscope, and metadata

### Data Structure
```
data/
├── Raw Data/          # 50 activity folders
│   └── [Activity]_[Number]/
│       ├── AccelerometerUncalibrated.csv
│       ├── GyroscopeUncalibrated.csv
│       └── Metadata.csv
└── Cleaned Data/      # Processed outputs
    ├── features_extracted.csv
    ├── features_normalized.csv
    └── performance_metrics.csv
```

## Installation

### Requirements
- Python 3.8+
- pip

### Setup - Local IDE

1. Clone the repository:
```bash
git clone <repository-url>
cd Hidden-Markov-Models
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the notebook:
```bash
jupyter notebook HMM_Formative2.ipynb
```
### Google colab setup

1. Go to https://colab.research.google.com/
2. Upload the notebook after downloading it from github repo
3. Choose your Runtime type and make sure it is running
4. Access the Runtime terminal(command prompt) at the lower section where there is variables and terminal icon and click it.
<img width="461" height="72" alt="Screenshot 2025-10-31 at 17 35 22" src="https://github.com/user-attachments/assets/24cc75b6-815e-439e-99cf-b22270fe26b4" />
5. Clone the repo to access the raw data and necessary prerequisites 
```bash
git clone <repository-url>
cd Hidden-Markov-Models
```
6. Run all cells

## Notebook Structure

### 1. Data Loading
Load and organize sensor data from nested folders.

### 2. Feature Extraction
Extract 24 features from time windows:
- 20 time-domain (mean, variance, RMS for accel/gyro, SMA)
- 4 frequency-domain (dominant frequency, spectral energy)
Window size: 1.5s (150 samples), 50% overlap
Total: 398 windows from 50 samples

### 3. Feature Normalization
Apply StandardScaler (Z-score normalization)

### 4. HMM Training
Train HMM models using Baum-Welch algorithm

### 5. Model Evaluation
Evaluate performance with confusion matrix, sensitivity, specificity, and accuracy

## Features

20 time-domain features:
- Mean, variance, RMS (6 each for accel + gyro)
- SMA (2)

4 frequency-domain features:
- Dominant frequency (accel + gyro)
- Spectral energy (accel + gyro)

## Model

- **Type**: Gaussian HMM
- **States**: 4 activities (standing, walking, jumping, still)
- **Features**: 24 dimensions
- **Training**: Baum-Welch algorithm
- **Decoding**: Viterbi algorithm

## Results

80/20 train-test split with performance metrics:
- Sensitivity, specificity, and accuracy per activity
- Results saved in `data/Cleaned Data/performance_metrics.csv`

## Files

- `HMM_Formative2.ipynb` - Main analysis notebook
- `requirements.txt` - Python dependencies
- `data/Cleaned Data/` - Processed features and metrics
- `/Visualizations` - Images of the plotted visualizations on data, features extraction, and performance analysis plots
