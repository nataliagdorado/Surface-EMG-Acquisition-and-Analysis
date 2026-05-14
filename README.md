# Surface EMG Acquisition and Analysis: A Biomedical Pipeline

This repository contains the code and analysis for the acquisition and processing of Surface Electromyography (sEMG) signals using the BITalino platform. The project develops a complete pipeline from raw data conversion to the extraction of temporal and spectral features for muscle fatigue study

## 📌 Project Overview
The objective is to process forearm muscle signals captured via BITalino to evaluate physiological conditions such as fatigue and environmental factors like Power Line Interference (PLI).

## 🛠 Experimental Setup
* **Device:** BITalino (r)evolution (10-bit resolution, $f_s = 1000$ Hz).
* **Configuration:** Bipolar electrodes on the forearm, reference electrode on the elbow.
* **Protocols:**
    * **Protocol 1:** Maximum Voluntary Contractions (MVC) in a quiet environment.
    * **Protocol 2:** MVCs near an electrical socket to record PLI noise.
    * **Protocol 3:** 1-minute endurance contraction for fatigue analysis.

## 💻 Signal Processing Pipeline

### 1. Digital-to-Physical Conversion
Conversion of ADC counts to Millivolts (mV) using the BITalino transfer function:
$$EMG(mV) = \frac{(\frac{ADC}{2^n} - 0.5) \cdot VCC}{G_{EMG}} \cdot 1000$$

### 2. Filtering & Preprocessing
* **Band-Pass Filter:** 4th-order Butterworth (20–450 Hz) to remove motion artifacts and noise.
* **Notch Filter:** 50 Hz Recursive IIR filter to eliminate Power Line Interference.
* **Artifact Removal:** Implementation of adaptive excision methods to handle transient motion spikes (specifically for cable motion artifacts observed in experimental data).

### 3. Feature Extraction
* **Temporal:** Automated MVC detection using a threshold-based algorithm ($Mean_{noise} + 6\sigma_{noise}$) and Root Mean Square (RMS) calculation.
* **Spectral:** Power Spectral Density (PSD) estimation using Welch's method to analyze frequency shifts during fatigue.

## 📈 Key Results
* **SNR Analysis:** Quantified degradation in signal quality near power sockets (up to 25 dB drop) and successful recovery using digital filters.
* **Fatigue Markers:** Tracking of Mean Frequency (MNF) and Median Frequency (MDF) shifts during sustained contractions.

## 📂 Requirements
* Python
* NumPy, SciPy, Matplotlib, Pandas
* Google Colab
