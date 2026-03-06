# 🚗 Hybrid Intrusion Detection System for CAN Bus Networks

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Status](https://img.shields.io/badge/Status-Research-orange.svg)
![MSc](https://img.shields.io/badge/MSc-Cyber%20Security%20Engineering-purple.svg)

> A lightweight hybrid intrusion detection system that combines rule-based logic with machine learning to detect cyberattacks on in-vehicle CAN bus networks — without destabilising the safety-critical systems it protects.

---

## 🔍 The Problem

The Controller Area Network (CAN) protocol powers communication between electronic control units (ECUs) inside almost every modern vehicle. It was designed in the 1980s for reliability and speed — not security. There is no authentication, no encryption, and no message verification built in.

Anyone with access to the network can send any message. That includes an attacker.

As vehicles become more connected — through Bluetooth, OBD-II ports, over-the-air updates, and V2X communication — the attack surface grows. But the underlying network protocol has not changed.

This project asks: **how do you detect attacks on a network that was never designed to be defended?**

---

## 🎯 What This Project Does

This project simulates five real-world CAN bus attack types, generates a labelled dataset of over 20 million frames, and evaluates three intrusion detection approaches:

- **Rule-Based IDS** — threshold and pattern detection for known attack signatures
- **Machine Learning IDS** — statistical and behavioural anomaly detection using Random Forest, Extra Trees, Decision Tree, and Logistic Regression
- **Hybrid IDS** — combines both layers using a decision fusion engine that routes high-confidence anomalies through rules and subtle patterns through ML

The hybrid approach achieved **98% binary accuracy**, the **lowest false positive rate** of all three methods, and a **detection latency of 2.1 milliseconds** — within the real-time constraints of an active vehicle network.

For simulation setup and tools used, see docs/methodology.md

---

## ⚔️ Attack Types Simulated

| Attack | Description | Detection Challenge |
|---|---|---|
| Denial-of-Service | Floods the bus with high-frequency frames | Easy — high volume, obvious pattern |
| ID Spoofing | Forges CAN frame identifiers | Medium — requires frequency analysis |
| Replay | Re-injects previously captured valid frames | Medium — requires temporal windows |
| Fuzzing | Sends randomised frame payloads | Medium — payload entropy analysis |
| Stealth Injection | Low-rate malicious frames blending into normal traffic | Hard — subtle, designed to evade detection |

---

## 📊 Key Results

### Binary Classification (Normal vs Attack)

| IDS Type | Accuracy | Precision | Recall | F1 Score | False Positive Rate | Latency |
|---|---|---|---|---|---|---|
| Rule-Based | 0.91 | 0.94 | 0.78 | 0.85 | 0.05 | 0.5ms |
| ML Only (Random Forest) | 0.97 | 0.96 | 0.95 | 0.96 | 0.04 | 2.5ms |
| **Hybrid IDS** | **0.98** | **0.97** | **0.97** | **0.97** | **0.03** | **2.1ms** |

### Multiclass Classification (Attack Type Identification)

| IDS Type | Accuracy | Macro F1 | False Positive Rate |
|---|---|---|---|
| Rule-Based | 0.72 | 0.65 | 0.07 |
| ML Only (Random Forest) | 0.92 | 0.89 | 0.07 |
| **Hybrid IDS** | **0.94** | **0.91** | **0.06** |

---

## 🧠 Key Insight

Detection accuracy is not the right metric to optimise for in safety-critical systems.

A false positive in a traditional network triggers an alert. A false positive in a vehicle network can suppress a legitimate safety-critical message — a brake signal, a steering input, an emergency response. The hybrid approach was designed with this constraint in mind, prioritising a low false positive rate alongside high detection accuracy.

**In automotive security, the defence itself can become the risk.**

---

## ⚠️ Limitations

- Simulated environment only — ICSim does not replicate real ECU behaviour or vehicle dynamics
- Dataset imbalance — DoS attacks dominate (~70% of samples), stealth attacks underrepresented
- Limited ML scope — four classifiers tested, no deep learning or RNN-based approaches
- V2X analysis — basic UDP-based simulation, not a full DSRC or C-V2X stack

---

## 📚 Academic Context

This project was developed as part of an MSc dissertation in Cyber Security Engineering at the University of Warwick (WMG), submitted September 2025.

Standards referenced: ISO/SAE 21434, UNECE R155, UNECE R156, IEEE 1609.2, AUTOSAR Adaptive.

---

## 👤 Author

- **Rakesh Elamaran**
- MSc Cyber Security Engineering – University of Warwick
- Security Engineer | Licensed Penetration Tester | NCSC Certified Graduate

🌐 [rakeshelamaran.com](https://rakeshelamaran.com)

---

## 📄 Licence
This project is for viewing and educational reference only. No part of this code may be copied, modified, distributed, or used without explicit written permission from the author.
