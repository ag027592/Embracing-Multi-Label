# Embracing Multi-Label Speech Emotion Recognition Using the All-Inclusive Aggregation Rule

[![Paper](https://img.shields.io/badge/IEEE%20SLT%202024-Paper-00629B?style=flat-square)](https://doi.org/10.1109/SLT61566.2024.10832302)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

Official implementation of **Embracing Ambiguity and Subjectivity Using the All-Inclusive Aggregation Rule for Evaluating Multi-Label Speech Emotion Recognition Systems**, published at the 2024 IEEE Spoken Language Technology Workshop (SLT), pages 502-509.

👥 Authors: Huang-Cheng Chou, Haibin Wu, Lucas Goncalves, Seong-Gyun Leem, Ali N. Salman, Carlos Busso, Hung-yi Lee, and Chi-Chun Lee

## Overview

Speech emotion recognition is unusual among speech tasks: the annotations reflect the subjective perception of individual raters, not an objective property of the signal. Most prior work treats that subjectivity as noise, collapsing ratings into a single consensus label via the majority or plurality rule. That discards every rating that disagrees with the consensus, and it quietly makes the test set easier by removing the ambiguous samples.

This repository implements the **all-inclusive rule (AR)**, which keeps all data, all ratings, and distributional labels as multi-label targets, and evaluates on a complete test set that includes ambiguous samples. Models trained with AR-generated multi-label targets outperform conventional single-label methods on both incomplete and complete test sets, across USC-IEMOCAP, MSP-IMPROV, MSP-PODCAST 1.11, and BIIC-PODCAST 1.01.

Related work: [EMO-SUPERB](https://github.com/ag027592/EMO-SUPERB) (reproducible SER benchmark) and *Minority Views Matter*, IEEE Transactions on Affective Computing 2024 ([doi](https://doi.org/10.1109/TAFFC.2024.3411290)).

# Requirement
* Python ==3.10
* Conda ==23.11.0
* Pytorch ==2.20 
* HuggingFace ==4.36.2

# Dataset Preparation
* Download WAV files into the folder for each database (e.g., data/MSP-PODCAST1.11/Audios) by submitting the EULA form for the six databases.
  * [USC-IEMOCAP](https://sail.usc.edu/iemocap/iemocap_release.htm)
  * [MSP-IMPROV](https://ecs.utdallas.edu/research/researchlabs/msp-lab/MSP-Improv.html)
  * [MSP-PODCAST1.11](https://ecs.utdallas.edu/research/researchlabs/msp-lab/MSP-Podcast.html)
  * [BIIC-PODCAST1.01](https://biic.ee.nthu.edu.tw/open_resource_detail.php?id=63)
  
## Setup Environments
* Step0: Install Conda [Link](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)
* Step1:
  ``` bash
  (base) $ conda create -n all_inclusive python=3.10 -y
  (base) $ conda activate all_inclusive
  (all_inclusive) $ conda install pip
  ```
* Step2: Install Pytorch [Link](https://pytorch.org/get-started/locally/)
* Step3: Install HuggingFace [Link](https://huggingface.co/docs/transformers/installation)

# Parameters Definition
* **output_num**: number of emotions (e.g., 8)
* **corpus**: database (e.g., MSP-PODCAST1.11)
  * **Names of the corpus**: MSP-PODCAST1.11, MSP-IMPROV, USC-IEMOCAP, BIIC-PODCAST1.01
* **model_type**: backbone model (default: wav2vec2-large-robust)
* **seed**: seed number
* **label_rule**: aggregation rule (e.g., M, P, or D)
  * M: Majority rule
  * P: Plurality rule
  * D: All-inclusive rule
* **partition_number**: which partition is the test set (e.g., 1)

# Train SER Systems
* Run **bash run_all_{database_nanme}.sh** to automatically train and evaluate the baseline models
* For instance:
  ``` bash
  (all_inclusive) $ bash run_all_BIIC_PODCAST_P.sh
  (all_inclusive) $ bash run_all_IEMOCAP.sh
  (all_inclusive) $ bash run_all_MSP_IMPROV_P.sh
  (all_inclusive) $ bash run_all_PODCAST_P.sh
  ```

# Evaluate SER Systems

* Run **bash run_all_{database_nanme}_Evaluation.sh** to automatically train and evaluate the baseline models
* For instance:
  ``` bash
  (all_inclusive) $ bash run_all_BIIC_PODCAST_P_Evaluation.sh
  (all_inclusive) $ bash run_all_IEMOCAP_Evaluation.sh
  (all_inclusive) $ bash run_all_MSP_IMPROV_P_Evaluation.sh
  (all_inclusive) $ bash run_all_PODCAST_P_Evaluation.sh
  ```

# Check Results
* All **check point** files will be in the folder, **model**

# Citation
If you find this work useful in your research, please cite:
```
@INPROCEEDINGS{Chou_2024_AllInclusive,
  author={Chou, Huang-Cheng and Wu, Haibin and Goncalves, Lucas and Leem, Seong-Gyun and Salman, Ali N. and Busso, Carlos and Lee, Hung-yi and Lee, Chi-Chun},
  booktitle={2024 IEEE Spoken Language Technology Workshop (SLT)},
  title={Embracing Ambiguity And Subjectivity Using The All-Inclusive Aggregation Rule For Evaluating Multi-Label Speech Emotion Recognition Systems},
  year={2024},
  pages={502-509},
  doi={10.1109/SLT61566.2024.10832302}
}
```

# License
Released under the [MIT License](LICENSE).

