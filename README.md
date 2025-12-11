# TriNETra: A Real-Time Anomaly Based Intrusion Detection System🛡️

**TriNETra** is an innovative, high-performance Anomaly-Based Intrusion Detection System designed to monitor network traffic in real-time and proactively detect Denial of Service (DoS) and Probe attacks. It combines optimized machine learning (XGBoost/Decision Tree) with a novel **Genetic Algorithm (GA)** for feature selection and a dynamic **60-second sliding window** to ensure low-latency and highly sensitive detection.



## 💡 Key Features

- **Real-Time Packet Capture:** Utilizes **_pyshark_** for continuous, high-speed capture and dissection of live network packets.
  
- **GA-Optimized Classification:** Employs a **_Genetic Algorithm_** to select the minimal, most discriminant feature subset, reducing feature count by over 50% for high-speed prediction.

- **Attack Masking Prevention:** Implements a dynamic **_60-second history timeout_** logic to ensure statistical features are always based on recent traffic, dramatically increasing sensitivity to short-burst attacks.

- **High-Performance ML:** Uses a Decision Tree Classifier (benchmarked against XGBoost) for fast, multi-class classification into **_Normal, DoS, or Probe_**.

- **Intuitive GUI:** Features a **_PyQt5_** graphical user interface for real-time logging, anomaly alerting, and post-session visualization.

- **Proactive Defense:** Provides early warnings against suspicious activities like port scanning and slow-rate probing.



## ⚙️ System Architecture & Workflow

The **TriNETra** system operates via a streamlined, three-stage pipeline to achieve low-latency anomaly detection:

1. **Capture & Preprocessing:** The system captures packets using **_pyshark_** and immediately calculates 18 crucial KDD-like statistical features. The dynamic **_60-second sliding window_** ensures feature integrity against attack masking.

2. **Optimized Classification:** The feature vector is fed into the highly efficient Decision Tree model, which utilizes the GA-optimized feature subset for maximum speed. The model classifies the traffic as **_Normal, DoS, or Probe_**.

3. **Output & Control:** The **_ABNIDS.py_** orchestrator updates the **_PyQt5 GUI_** with real-time logs and filtered anomaly alerts, providing clear visual feedback to the operator.



## 📸 Interface Screenshots

The application's interface, built using **PyQt5**, provides immediate visual feedback on the system's status and detected anomalies.

1. **Main Monitoring Dashboard**
   This view shows the primary window with the control panel, the **_Capturing Panel_** (live traffic logs), and the **_Result Panel_** (filtered anomalies).

   <img width="910" height="883" alt="Screenshot 2025-11-25 100354" src="https://github.com/user-attachments/assets/4d7b5e71-de02-4c09-bf61-b408b9c7ef90" />

2. **Post-Monitoring Visualization**
   After monitoring is stopped, the system generates a graphical summary of the session's findings, detailing the total count of classified traffic.

   <img width="642" height="559" alt="Screenshot 2025-11-25 100648" src="https://github.com/user-attachments/assets/0ac9c45c-db15-452b-8fa3-c1ae56b483ba" />



## 🚀 Getting Started

### Prerequisites

You will need **_Python 3.x_** and the following system dependencies:
- **_tshark_** (The command-line tool for Wireshark, required by pyshark).
- **_Root/Administrator Privileges_** (Required to capture raw packets on a network interface).

### Installation

1. Clone the repository:
   
   ```bash
   git clone https://github.com/madhavtiwari27/TriNETra.git
   cd TriNETra
   ```

2. Install the necessary Python libraries:

   ```bash
   pip install pyshark pandas scikit-learn numpy xgboost PyQt5 matplotlib
   ```

### Usage

1. **Prepare Training Data:**

   - Ensure your raw **_KDD-like_** training and testing datasets are prepared.
   - Run the necessary data cleaning via **_Preprocess.py_** to convert categorical data to the required numerical format.
  
2. **Train the Model & Optimize Features:**

   - Run the main GUI file:

     ```bash
     python ABNIDS.py
     ```

   - In the GUI, use the **_Train Model_** function to load your preprocessed training/testing datasets. This step will execute the **_Genetic Algorithm_** to find the optimal feature mask and train the final Decision Tree classifier.
  
3. **Start Real-Time Monitoring:**

   - Select your network interface.
   - Click the **_Start Monitoring_** button. The system will begin continuous real-time packet capture, feature extraction, and anomaly classification.
   - Detected attacks will be logged in the **_Result Panel_**.



## 📦 Project File Structure

| **File**        | **Role**                         | **Description** |
|----------------|------------------------------|-------------|
| **ABNIDS.py**  | System Orchestrator & GUI    | Main executable. Manages the application lifecycle, GUI (PyQt5), thread control, and visualization. |
| **packet.py**  | Feature Engineering Core     | Handles real-time packet dissection (pyshark), calculates the 18 statistical features, and implements the critical 60-second history timeout logic. |
| **classifier.py** | ML Prediction Logic       | Defines the Decision Tree Classifier, trains the model with the GA feature mask, and maps numerical outputs (0–9) to attack labels (Normal, DoS, Probe). |
| **tree.py**    | GA Controller                | High-level orchestration of the Genetic Algorithm, including population initialization, fitness evaluation, selection, crossover, and mutation. |
| **class_.py**  | GA Population Manager        | Manages the collection of Individual (chromosome) objects and implements the core reproduction mechanics (crossover, mutation). |
| **Individual.py** | GA Chromosome Unit       | Defines the feature mask (chromosome) and calculates its own fitness score by calling classifier.get_fitness. |
| **Preprocess.py** | Data Preprocessing        | Offline script to clean raw datasets, map categorical values (protocol, service, attack names) to numerical representations, and select the 18 relevant features. |
| **XGB.py**     | Benchmark Script             | Standalone script to train and evaluate an XGBoost Classifier as a performance benchmark against the main Decision Tree model. |
