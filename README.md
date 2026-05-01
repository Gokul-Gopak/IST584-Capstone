# ML-Based Runtime Malware Detection

## Project Overview
This project focuses on protecting containerized cloud environments from advanced security threats, specifically the Kinsing cryptojacker. Traditional defense systems that rely on signatures struggle to keep up with modern malware that changes appearance and blends into cluster networks.

To address this, the project introduces a machine-learning-powered detection engine that analyzes network traffic patterns in real time to stop container abuse before it causes harm.

---

## How It Works
The system operates as a closed loop that monitors, analyzes, and responds to container traffic:

### 1. Telemetry Ingestion
Network traffic data is captured directly from the Kubernetes cluster.

### 2. Feature Processing
Key flow metrics—such as connection duration and throughput (bytes per second)—are extracted from the traffic records.

### 3. Machine Learning Inference
A trained Random Forest classifier evaluates these features to distinguish normal behavior from anomalies.

### 4. Automated Response
The engine triggers automated actions based on its confidence level to contain threats:

- **Confidence > 85%** → `KILL_POD`  
  Terminates the compromised container immediately.

- **Confidence 60% – 85%** → `QUARANTINE_NETNS`  
  Isolates the container’s network namespace.

- **Confidence < 60%** → `LOG_AND_MONITOR`  
  Continues observation for further analysis.

---

## Key Metrics & Results
The Random Forest classifier was evaluated using a combined dataset of **158,621 network records**.

- **94% Accuracy**  
  Strong reliability in detecting malicious patterns.

- **94% Macro F1-Score**  
  Balanced performance across both benign and anomalous classes.

- **96% Precision (Benign)**  
  Minimizes false positives and avoids unnecessary disruptions.

- **96% Recall (Anomalies)**  
  Effectively identifies true malicious activity before lateral movement occurs.

---

## Summary
This project demonstrates how machine learning can provide proactive, real-time protection for containerized environments by detecting and responding to threats based on behavioral patterns rather than static signatures.
