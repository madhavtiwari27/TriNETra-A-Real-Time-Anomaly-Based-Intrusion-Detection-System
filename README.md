# TriNETra: A Real-Time Anomaly Based Intrusion Detection System🛡️

**TriNETra** is an innovative, high-performance Anomaly-Based Intrusion Detection System designed to monitor network traffic in real-time and proactively detect Denial of Service (DoS) and Probe attacks. It combines optimized machine learning (XGBoost/Decision Tree) with a novel **Genetic Algorithm (GA)** for feature selection and a dynamic **60-second sliding window** to ensure low-latency and highly sensitive detection.


## 💡 Key Features

- **Real-Time Packet Capture:** Utilizes **_pyshark_** for continuous, high-speed capture and dissection of live network packets.
  
- **GA-Optimized Classification:** Employs a **_Genetic Algorithm_** to select the minimal, most discriminant feature subset, reducing feature count by over 50% for high-speed prediction.

- **Attack Masking Prevention:** Implements a dynamic **_60-second history timeout_** logic to ensure statistical features are always based on recent traffic, dramatically increasing sensitivity to short-burst attacks.

- **High-Performance ML:** Uses a Decision Tree Classifier (benchmarked against XGBoost) for fast, multi-class classification into **_Normal, DoS, or Probe_**.

- **Intuitive GUI:** Features a **_PyQt5_** graphical user interface for real-time logging, anomaly alerting, and post-session visualization.

- **Proactive Defense:** Provides early warnings against suspicious activities like port scanning and slow-rate probing.


