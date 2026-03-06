## Methodology

## Environment and Tools
All attacks were simulated in a controlled virtual environment using open-source automotive security tools. No real vehicles were used.
ToolPurposeICSimVirtual CAN bus and instrument cluster simulatorSocketCAN / vcan0Linux virtual CAN interfacecan-utils (candump, cansend, cangen)CAN traffic capture and injectionCaring CaribouAutomotive security research and fuzzingPython (scikit-learn, pandas, numpy)Feature extraction, ML training, evaluation

## Attack Simulation and Data Collection
Five attack types were simulated against a virtual CAN bus: denial-of-service, ID spoofing, replay, fuzzing, and stealth injection. Raw CAN traffic was captured using candump, parsed into structured CSV files, and labelled for both binary and multiclass classification. The final dataset contained over 20.6 million CAN frames.

## IDS Development and Evaluation
Three detection approaches were built and evaluated against the same dataset — a rule-based IDS, a machine learning IDS (Random Forest, Extra Trees, Decision Tree, Logistic Regression), and a hybrid IDS combining both layers. The hybrid approach achieved 98% binary accuracy with the lowest false positive rate and a detection latency of 2.1ms
