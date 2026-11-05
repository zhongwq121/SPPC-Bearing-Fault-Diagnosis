# SPPC-Bearing-Fault-Diagnosis

# SPPC: Selective Physics-Based Prediction Correction for Cross-Machine Bearing Fault Diagnosis

**A physics-informed, post-hoc prediction correction method for inner-race and outer-race bearing faults.**

> **Repository status:** This repository currently provides a project overview only. The source code, experiment configurations, and reproduction scripts have **not yet been released**. We plan to add them after the implementation and release materials have been verified.

## Overview

Diagnostic models deployed on previously unseen machines may recognize a bearing fault while confusing its location, particularly between inner-race and outer-race faults. These two fault locations have different bearing characteristic orders, which provide a mechanical reference for revisiting a model's prediction.

**Selective Physics-Based Prediction Correction (SPPC)** is a post-hoc framework that uses bearing-specific physical evidence to selectively revise predictions from an already trained and frozen diagnostic model. It does not retrain or modify the backbone. SPPC preserves the backbone's normal/fault decision and considers only **Inner ↔ Outer** corrections.

## Framework

> **Framework figure:** To be added.

<!--
To add the final SPPC framework figure:
1. Upload the image to assets/sppc_framework.png.
2. Delete the placeholder quotation above.
3. Uncomment the Markdown image line below (remove the leading and trailing HTML comment markers).

![SPPC framework](assets/sppc_framework.png)
-->

## Method

SPPC combines three elements:

1. **Bearing-specific physical evidence.** Given validated bearing geometry (or known theoretical characteristic orders) and a usable speed/angle reference, SPPC constructs an envelope order spectrum and evaluates candidate bands around the BPFI and BPFO harmonics. Band-averaged spectral amplitudes reduce the first-order scoring bias caused by different numbers of spectral bins.
2. **Multi-harmonic comparisons.** Physical evidence is accumulated across harmonics, with decisions evaluated at the fixed prefix set **K = {1, 2, 4, 8, 12}**.
3. **Selective correction.** A physical decision can replace the original Inner/Outer prediction only when the required physical-information conditions hold and all five prefix decisions agree. Otherwise, the original prediction is retained. Predictions of **Normal** are never changed.

The physical-information eligibility conditions rely on available, validated machine information; they do not constitute an online detector of incorrect bearing metadata or speed measurements.

## Evaluation

The method is studied using six frozen diagnostic backbones and two distinct evaluation settings:

| Setting | Datasets | Purpose |
| --- | --- | --- |
| Method development and analysis | CWRU, UOTTAWA, MFPT, DZLRSB | Examine prediction correction, physical evidence, and sensitivity to metadata errors |
| Independent external validation | Paderborn | Evaluate the fixed correction rules on a separate bearing platform |

The four development datasets were used during method development and should **not** be interpreted as independent tests of the final rule-selection process. The Paderborn evaluation was conducted with the SPPC rules and parameters fixed.

## Code availability

**Code is not available in this repository at present.** This initial README is intended to document the method and evaluation scope. Planned future additions include the SPPC implementation, preprocessing and evaluation configurations, and instructions for reproducing the reported experiments. Release details will be updated here when confirmed.

The original bearing datasets are maintained by their respective providers and are not redistributed through this repository.

## Paper and citation

**Manuscript:** *Selective Physics-Based Prediction Correction for Cross-Machine Bearing Fault Diagnosis*

A paper link and BibTeX citation will be added when publication or preprint details are available.

## License

A software license will be specified when the implementation is released.
