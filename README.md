# Hidden Markov Models for Human Activity Recognition

This project implements a complete Hidden Markov Model (HMM) pipeline for recognizing human activities from accelerometer and gyroscope sensor data collected via mobile devices.

## Project Overview

The goal is to build an HMM that can infer human activity states (standing, walking, jumping, still) from noisy sensor measurements. The project follows a complete machine learning workflow from data collection to model evaluation.

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

### Setup

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

## Notebook Structure

The `HMM_Formative2.ipynb` notebook contains the complete pipeline:

### 1. Data Loading and Organization
- Load sensor data from nested folder structure
- Categorize by activity type
- Display activity distribution

### 2. Feature Extraction
- Extract 24 features from time windows:
  - 17 time-domain features (mean, variance, RMS, SMA)
  - 4 frequency-domain features (dominant frequency, spectral energy)
- Window size: 1.5 seconds (150 samples) with 50% overlap
- Total: 398 windows from 50 samples

### 3. Feature Normalization
- Apply StandardScaler (Z-score normalization)
- Save normalized features

### 4. HMM Implementation and Training
- Train activity-specific HMM models
- Apply Baum-Welch algorithm
- Display transition matrix

### 5. Model Evaluation
- Compute confusion matrix
- Calculate sensitivity, specificity, and accuracy
- Visualize emission probabilities

## Feature Engineering

### Time-Domain Features (17)
- **Mean** (6): Average acceleration/rotation per axis
- **Variance** (6): Signal variability
- **RMS** (6): Root mean square energy
- **SMA** (2): Signal Magnitude Area

### Frequency-Domain Features (4)
- **Dominant frequency** (2): Primary frequency component
- **Spectral energy** (2): Total frequency power

## Model Architecture

- **Type**: Gaussian Hidden Markov Model
- **Hidden States**: 4 (standing, walking, jumping, still)
- **Features**: 24-dimensional feature vectors
- **Training**: Baum-Welch algorithm
- **Prediction**: Activity-specific likelihood scoring

## Results

Performance metrics computed on test set (80/20 split):
- **Sensitivity**: True positive rate per activity
- **Specificity**: True negative rate per activity  
- **Accuracy**: Overall classification accuracy

Results saved in `data/Cleaned Data/performance_metrics.csv`.

## Files

- `HMM_Formative2.ipynb` - Main analysis notebook
- `requirements.txt` - Python dependencies
- `data/Cleaned Data/` - Processed features and metrics

## Key Features

- Clean, organized notebook with logical flow
- Comprehensive feature extraction (time + frequency domain)
- Multiple HMM models for activity classification
- Detailed performance evaluation
- Ready for project submission
