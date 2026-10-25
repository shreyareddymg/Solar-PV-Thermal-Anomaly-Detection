# Solar PV Thermal Anomaly Detection

## Overview

This project explores UAV-based solar photovoltaic (PV) fault detection using YOLOv8n, fixed-threshold anomaly detection, and neighbourhood-normalized anomaly analysis.

It also includes heuristic severity scoring and automated inspection report generation using a large language model.

## Objectives

* Detect and classify solar PV faults.
* Compare fixed-threshold and neighbourhood-normalized detection methods.
* Evaluate performance using Precision, Recall, and F1-score.
* Assign heuristic visual-priority severity scores.
* Generate automated inspection reports.

## Technologies

* Python
* PyTorch
* YOLOv8 and Ultralytics
* NumPy and pandas
* Groq API and `openai/gpt-oss-20b`
* Google Colab

## Dataset

The project uses the Solar Panel Fault Detection dataset from Kaggle.

The dataset is not included in this repository. Users should obtain it from the original source and configure the notebook's dataset paths.

## Results

The project compares YOLOv8n against fixed-threshold and neighbourhood-normalized approaches.

In the preliminary evaluation on 15 test images, YOLOv8n performed better than the two threshold-based methods. The small test set limits the generalizability of this finding.

## Severity Scoring

Severity scores use local image contrast, detected area, and model confidence. They are heuristic visual-priority indicators and are not calibrated measurements of physical fault severity.

## Limitations

* Small test set.
* Neighbourhood-normalized detection produces false positives.
* Image intensity is not calibrated physical temperature.
* Severity scoring requires further validation.

## Future Work

* Evaluate on a larger and more diverse dataset.
* Improve neighbourhood-based anomaly detection.
* Incorporate calibrated temperature and environmental measurements.
* Add georeferenced anomaly mapping.
* Validate severity scores against expert assessments and actual power loss.

## Disclaimer

This project is an experimental study and is not intended to replace professional solar PV inspection.
