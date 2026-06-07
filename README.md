# Wearable Sensor-Based Exercise Classification & Repetition Counting

An end-to-end machine learning system for recognizing strength training exercises and automatically counting repetitions using wearable inertial sensor (IMU) data from accelerometer and gyroscope signals.

---

## Overview

This project focuses on building a complete **human activity recognition pipeline for fitness tracking**, using raw time-series data collected from wearable devices during gym exercises such as bench press, squat, row, overhead press, and deadlifts.

The system processes noisy sensor signals, extracts meaningful temporal and frequency-domain features, and applies machine learning models to classify exercises and quantify workout performance through automatic repetition counting.

---

## Key Features

* End-to-end pipeline from raw IMU sensor data to final predictions
* Multi-class exercise classification using classical machine learning models
* Automated repetition counting using signal peak detection
* Advanced signal processing and feature engineering for time-series data
* Comparative evaluation of multiple feature sets and model architectures
* Robust preprocessing pipeline including filtering and outlier handling

---

## Dataset

* **Source:** Custom MetaMotion wearable sensor dataset
* **Sensors Used:** Accelerometer (12.5 Hz), Gyroscope (25 Hz)
* **Exercises:** Bench press, squat, row, overhead press, deadlift
* **Labels:** Exercise type, intensity category (heavy/light), participant ID
* **Structure:** Multiple recorded sets per exercise per participant

---

## Data Processing Pipeline

### Raw Data Handling

* Loaded multiple CSV files from wearable recordings
* Parsed metadata from filenames (exercise type, participant, category)
* Synchronized accelerometer and gyroscope streams
* Converted timestamps into structured time-indexed format

### Signal Processing

* Resampled data to uniform time intervals (200 ms)
* Applied **Butterworth low-pass filtering** to reduce sensor noise
* Handled missing values using interpolation
* Removed outliers using statistical filtering methods

---

## Feature Engineering

### Time-Domain Features

* Rolling mean and standard deviation features
* Signal magnitude (acceleration and angular velocity)
* Temporal abstraction over sliding windows

### Frequency-Domain Features

* Fast Fourier Transform (FFT) over sliding windows
* Dominant frequency detection
* Power spectral energy and weighted frequency measures

### Dimensionality Reduction

* Principal Component Analysis (PCA) for feature compression
* Correlation-based feature selection

### Additional Transformations

* Signal magnitude computation (acceleration + gyroscope norms)
* K-Means clustering for motion pattern exploration

---

## Models Used

The following machine learning models were evaluated:

* Random Forest
* Neural Networks (MLP)
* Decision Trees
* K-Nearest Neighbors (KNN)
* Naive Bayes

---

## Repetition Counting

A custom repetition counting system was developed using:

* Low-pass filtered motion signals
* Peak detection using local extrema analysis
* Exercise-specific threshold tuning
* Robust evaluation against labeled repetition counts

This enables automated tracking of workout volume from raw sensor data.

---

## Evaluation (Results)

### Exercise Classification Performance

* The system achieved strong classification performance across multiple models and feature sets.
* **Best model: Random Forest**
  * **Accuracy: ~99.5%**
* Neural Networks also performed competitively, closely matching ensemble methods.
* Feature engineering (PCA + FFT + temporal features) significantly improved performance compared to raw sensor signals.

### Model Comparison (Summary Insight)

| Model               | Performance Insight                                      |
| ------------------- | -------------------------------------------------------- |
| Random Forest       | Best overall accuracy and stability                      |
| Neural Network      | High performance with well-engineered features           |
| KNN / Decision Tree | Good baseline performance, slightly lower generalization |
| Naive Bayes         | Fast but less expressive for complex patterns            |


### Repetition Counting Performance

* Rep counting system achieved low error against labeled repetitions
* **Mean Absolute Error** was minimized using:
  * Exercise-specific signal selection (acceleration vs gyroscope)
  * Adaptive cutoff tuning per exercise
* Peak detection on filtered signals reliably captured repetition cycles across exercises

### Outcome

* Demonstrated that well-engineered time-series features can achieve performance comparable to more complex models
* Achieved near real-world usable performance for both:
  * Exercise classification
  * Automated workout repetition tracking

---

## Key Insights

* Feature engineering significantly improved model performance compared to raw signals
* Frequency-domain features helped distinguish similar movement patterns
* Low-pass filtering was critical for stable repetition detection
* Different exercises require different signal channels for optimal rep counting
* Simple ML models performed extremely well with well-engineered features

---

## Limitations

* Small dataset size with limited participants
* Exercise generalization across unseen users may be limited
* Rep counting is sensitive to threshold tuning per exercise
* No deep learning models were explored for sequence modeling

---

## Future Work

* Extend system to real-time wearable deployment
* Incorporate deep learning (LSTM/Transformer-based time-series models)
* Improve generalization across users and devices
* Add real-time feedback for gym coaching applications
* Expand dataset with more exercises and environments

---

## Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* SciPy
* Matplotlib, Seaborn
* Signal Processing (FFT, filtering techniques)
