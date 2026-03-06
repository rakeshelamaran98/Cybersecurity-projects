## Methodology

This project was conducted in four phases — simulating CAN bus attacks in a virtual environment, capturing and labelling over 20.6 million CAN frames, building three intrusion detection approaches, and evaluating them against the same dataset. All work was done using open-source automotive security tools with no real vehicles involved

## 🛠️ Tools and Environment

| Tool | Purpose |
|---|---|
| ICSim | Instrument cluster simulator — virtual CAN bus environment |
| SocketCAN / vcan0 | Linux virtual CAN interface |
| can-utils (candump, cansend, cangen) | CAN traffic generation and capture |
| Caring Caribou | Automotive security research tool |
| Python (scikit-learn, pandas, numpy) | Feature extraction, ML training, evaluation |

> **Note:** All attacks were simulated in a controlled virtual environment. No real vehicles were used or harmed.

## Attack Simulation and Data Collection
Five attack types were simulated against a virtual CAN bus: denial-of-service, ID spoofing, replay, fuzzing, and stealth injection. Raw CAN traffic was captured using candump, parsed into structured CSV files, and labelled for both binary and multiclass classification. The final dataset contained over 20.6 million CAN frames.

## IDS Development and Evaluation
Three detection approaches were built and evaluated against the same dataset — a rule-based IDS, a machine learning IDS (Random Forest, Extra Trees, Decision Tree, Logistic Regression), and a hybrid IDS combining both layers. The hybrid approach achieved 98% binary accuracy with the lowest false positive rate and a detection latency of 2.1ms
