# Neighbourhood-Normalized Thermal Anomaly Detection for UAV-Based Solar Photovoltaic Inspection

**Document:** Automated Solar PV Inspection Report
**Evaluation Set:** 15 UAV-captured images
**Status:** Preliminary Results — Human Verification Required

---

## 1. Executive Summary

The solar PV fault detection pipeline was evaluated on a limited test set of 15 images, producing 49 detections across six fault classes and three heuristic severity categories: High, Medium, and Low.

The most frequently detected classes were MultiHotSpot (17 detections), SingleByPassed (13), and SingleDiode (11). Of the 49 detections, 14 were categorized as High severity, 24 as Medium, and 11 as Low.

The ten highest-ranked detections all received a High severity classification. Their model confidence values ranged from approximately 0.49 to 0.92, while their detected areas ranged from 0.28% to 1.59%.

The severity score combines local image contrast, detected area, and model confidence. It is a **heuristic visual-priority score**, not a calibrated measure of physical fault severity. Model confidence also does not quantify physical severity.

These findings are preliminary and should be used to prioritize further human inspection rather than to make standalone maintenance decisions.

## 2. Detection Statistics

| Metric                                  |      Result |
| --------------------------------------- | ----------: |
| Test images                             |          15 |
| Total detections                        |          49 |
| Average detections per image            |        3.27 |
| High-severity detections                | 14 (28.57%) |
| Medium-severity detections              | 24 (48.98%) |
| Low-severity detections                 | 11 (22.45%) |
| Model confidence range among detections |   0.49–0.92 |
| Detected area range                     | 0.28%–1.59% |
| Local contrast range                    | 37.40–55.36 |

*Note: Statistics are based on the supplied detection results. Percentages may differ slightly due to rounding.*

## 3. Fault-Class Analysis

| Fault Class       | Detection Count | Percentage |
| ----------------- | --------------: | ---------: |
| MultiHotSpot      |              17 |      34.7% |
| SingleByPassed    |              13 |      26.5% |
| SingleDiode       |              11 |      22.4% |
| SingleHotSpot     |               6 |      12.2% |
| MultiDiode        |               1 |       2.0% |
| StringOpenCircuit |               1 |       2.0% |
| **Total**         |          **49** |   **100%** |

### Observations

* **MultiHotSpot** was the most frequently detected class, accounting for approximately 34.7% of detections.
* **SingleByPassed** and **SingleDiode** were also frequently detected.
* **SingleHotSpot**, **MultiDiode**, and **StringOpenCircuit** appeared less frequently in this test sample.
* Detection frequency alone does not establish the actual prevalence of a fault class. The results may also reflect dataset composition and model behavior.

## 4. High-Priority Findings

The following table lists the ten detections with the highest heuristic severity scores.

| Rank | Image                                                                 | Fault Class    | Confidence | Area (%) | Local Contrast | Severity Score | Category |
| ---: | --------------------------------------------------------------------- | -------------- | ---------: | -------: | -------------: | -------------: | -------- |
|    1 | `101MEDIA_DJI_0385_T_JPG_jpg.rf.a4741f39b710b1e60aa3a5996bd96627.jpg` | SingleByPassed |      0.900 |    1.482 |          42.48 |          83.93 | High     |
|    2 | `101MEDIA_DJI_0435_T_JPG_jpg.rf.156a9022cef8a19d653bb222add4a164.jpg` | SingleDiode    |      0.791 |    1.415 |          41.38 |          81.49 | High     |
|    3 | `101MEDIA_DJI_0477_T_JPG_jpg.rf.e6e020dd4efe1db8461cc749dba7327f.jpg` | MultiHotSpot   |      0.773 |    1.272 |          45.73 |          80.54 | High     |
|    4 | `335_jpg.rf.c86c171d5fd2718151e1d424b021f650.jpg`                     | SingleDiode    |      0.923 |    0.283 |          51.04 |          79.59 | High     |
|    5 | `124_jpg.rf.a50e9cd85618126df170f30070e282b7.jpg`                     | MultiHotSpot   |      0.794 |    0.671 |          50.67 |          78.56 | High     |
|    6 | `101MEDIA_DJI_0435_T_JPG_jpg.rf.156a9022cef8a19d653bb222add4a164.jpg` | SingleDiode    |      0.810 |    1.515 |          37.40 |          78.35 | High     |
|    7 | `335_jpg.rf.c86c171d5fd2718151e1d424b021f650.jpg`                     | SingleDiode    |      0.792 |    0.312 |          55.36 |          77.08 | High     |
|    8 | `101MEDIA_DJI_0435_T_JPG_jpg.rf.156a9022cef8a19d653bb222add4a164.jpg` | MultiHotSpot   |      0.522 |    1.559 |          43.48 |          76.67 | High     |
|    9 | `101MEDIA_DJI_0435_T_JPG_jpg.rf.156a9022cef8a19d653bb222add4a164.jpg` | MultiDiode     |      0.489 |    1.591 |          41.60 |          76.15 | High     |
|   10 | `210_jpg.rf.babdcab5fd00a84a15bb7d95b2d649d5.jpg`                     | MultiHotSpot   |      0.717 |    0.308 |          48.91 |          75.56 | High     |

### Key Findings

* The highest-ranked detections include SingleByPassed, SingleDiode, and MultiHotSpot classifications.
* All ten detections fall into the High category under the current heuristic scoring rule.
* Some detections have relatively low model confidence despite high severity scores, demonstrating that severity ranking and model confidence represent different quantities.
* Multiple detections originate from the same image. They represent individual predicted detections, not necessarily distinct physical modules or independent faults.

## 5. Recommended Inspection Actions

### 5.1 Verify High-Priority Detections

Prioritize human review of the ten highest-ranked detections. Where possible, verify the findings using the original imagery, a suitable infrared camera, and an inspection by a qualified PV technician.

### 5.2 Review MultiHotSpot Detections

Review the 17 MultiHotSpot detections to determine whether the predicted anomalies are visually supported and whether any require further investigation.

### 5.3 Review SingleByPassed and SingleDiode Detections

Examine the 13 SingleByPassed and 11 SingleDiode detections, considering model confidence, detected area, and the available image context.

### 5.4 Record Confirmed Anomaly Locations

Where identifying information is available, record the relevant panel, module, and string identifiers. The current pipeline does not independently establish georeferenced locations.

### 5.5 Refine Detection Criteria

Review false positives and missed detections using ground-truth annotations before adjusting model confidence thresholds or severity criteria. Threshold changes should be evaluated on a separate validation set to avoid overfitting the test results.

## 6. Limitations and Future Improvements

### Limitations

* **Small test set:** Evaluation used only 15 images, so the results may not generalize to other sites or operating conditions.
* **Heuristic severity scoring:** Scores are based on local contrast, detected area, and model confidence; they are not calibrated against actual physical fault severity.
* **Model confidence:** Confidence indicates the model's prediction confidence, not the severity or electrical impact of a fault.
* **Missing physical measurements:** Calibrated temperature, irradiance, wind, and electrical performance measurements were not available for this evaluation.
* **Limited validation:** The results require verification against ground-truth annotations and expert inspection.

### Future Improvements

1. Expand testing to larger and more diverse UAV image datasets.
2. Improve neighbourhood-based anomaly detection to reduce false positives.
3. Incorporate calibrated thermal measurements and environmental variables.
4. Add module localization and georeferenced anomaly mapping.
5. Validate severity scores against expert assessments, measured temperature differences, and actual power loss.
6. Evaluate precision, recall, and F1-score on a larger, representative labeled test set.

## 7. Conclusion

The preliminary evaluation demonstrates a pipeline for solar PV fault detection, classification, heuristic severity ranking, and automated inspection report generation.

The generated results can help prioritize detections for further review. However, the limited test sample and the heuristic nature of severity scoring mean that the system should not be treated as a standalone diagnostic or maintenance decision tool.

**The findings are intended to support human inspection and guide further development and validation of the UAV-based solar PV fault detection pipeline.**
