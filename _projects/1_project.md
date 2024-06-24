---
layout: page
title: Cognitive Modelling
description: 
img: assets/img/cl_background.png
importance: 1
category: pillars
related_publications: false
---

## Overview

Cognitive modeling is a critical part for realizing AIDA3's vision. In general, there are five research questions related to this topic: 1) how to define and quantify cognitive load (CL) and situation awareness (SA); 2) how to classify and predict CL and SA in real time; 3) can we quantify operators' expertise using CL and SA during a mission; 4) what is the minimal set up for answering research question 2) and 3); 5) how to design the system so that CL and SA never exceed the safety thresholds.

CL and SA are two separate concepts. Together, they describe a person's cognitive states.
In general, CL can be interpreted as the amount of mental effort and resources required to process information, perform tasks, or solve problems, and SA can be interpreted as the perception of the elements in the environment within a volume of time and space, the comprehension of their meaning, and the projection of their status in the near future. In recent years, estimating CL and SA via various sensors and machine learning techniques has become popular. Among all sensors, electroencephalography (EEG) and eye tracker are the most popular due to their non-intrusive nature. An extensive research has been done. Nevertheless, there exist several research gaps. Firstly, it is well known that human's cognitive states consist of multiple modalities. For instance, CL is found to be related to both brain's activities and eye movements. However, the majority of the works only consider one modality when they model CL and SA. Secondly, although machine learning algorithms such as the support vector machine and random forest are widely used for estimating CL and SA with physiological data, deep learning models such as convolutional neural network or recurrent neural network are rarely used. This is because the size of the experiment data is usually too small to fully take advantages of deep learning models. Thirdly, current works mostly estimate CL and SA in a short and simple scenarios and they do not demonstrate the real-time applicability. Based on the aforementioned research gaps, we design an experiment and collect data using sensors for various modalities (EEG, eye tracker, and webcam), and 1 propose a multimodal deep learning model. Within the experiment, there are two tasks, one is a simple visual tracking task that aims to collect physiological data in a controlled environment, and the other one is a mission planning task that aims to collect physiological data in a realistic environment. The multimodal deep learning model utilizes and combines the extracted features from each sensor to estimate and predict CL and SA in real-time.

## Experiment Setup And Design

Our experiment (IRB-2023-1933) uses a EEG, an eye tracker, a webcam, and a microphone for collecting data. A photo of one of our staff wearing the EEG and eye tracker is shown in Fig. 1. Before the experiment starts, we set up and calibrate the EEG and eye tracker for the best accuracy. The EEG device is the actiCHamp Plus from Briain Vision, which is a 32-channel wet EEG device with up to 100kHz sampling rate. We make sure the impedance of every electrode is below 30k ohms (10k ohms for the reference and ground electrodes) to reduce the noise, an example is shown in Fig. 2. The eye tracker is the Pupil Core from Pupil Labs [1]. We use the built-in calibration program to calibrate it once before the experiment starts and once after each break in the experiment. After each calibration, we ask the subject to look at certain things shown on the monitor and we only proceed if the eye tracker can identify the gaze position accurately. The experiment has two sections. The first section of is a simple visual tracking task with or without a secondary task. This first section is also referred to as "task 1". Task 1 contains multiple trials. In each trial, the subject needs to watch a 10-second video where a red arrow and one or more white arrows move in a constant speed, as shown in Fig. 3. At the end of the video, the arrows will disappear and the subject needs to indicate the position and heading of all arrows by clicking with a mouse, as shown in Fig. 4. In this part, there is an undo button at the top left corner of the monitor for the subject to undo the clicks. Then, the subject needs to complete a NASA-TLX survey where an example is shown in Fig. 5. Completing the NASA-TLX survey is the end of one trial. The indicated position and heading of all arrows are used to compared with the true position and heading to derive labels for the subject's situational awareness (SA) level, and the NASA-TLX survey result will be used as the label of the subject's cognitive load (CL) level. After 15 trials, the subject needs to conduct another 15 trials but with the addition of the secondary task. The secondary task is called verb generation and it requires the subject to verbally respond to a noun with a related verb. In task 1, the noun is announced every 3 seconds. Completing the 15 trials with secondary task is the end of task 1.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/willis.jpg" title="wearable setup" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/eeg_impedance.jpg" title="impedance" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    One of our staff wearing the EEG and eye tracker on the left. The EEG impedance of a subject prior to the start of the experiment on the right.
</div>

The nouns for the secondary task are meticulously selected. Firstly, we build a dictionary by combining the noun list from [2] and [3]. Secondly, we use the medical research council psycholinguistic database [4] to obtain the familiarity, imaginability, and Thorndike-Lorg written frequency. Those metrics are widely used in the literature and compared to other metrics, they are available for most nouns in the dictionary. The nouns that do not have one of those values available are removed from the dictionary. Thirdly, we use density-based spatial clustering of applications with noise (DBSCAN) to cluster 190 words. Lastly, we use the Euclidean distance to connect similar nouns one by one and further group those words into subgroups, e.g., 2 words in each subgroup of task 1 and 80 words in each subgroup of task 2.

 <div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/task_1.jpg" title="task 1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3: The screenshot of a 10-second video in task 1
</div>

 <div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/task_1_clicks.jpg" title="task 1 clicks" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 4: The screenshot of how the subject clicks in task 1
</div>

 <div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/nasa_tlx.jpg" title="nasa tlx survey" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 5: The screenshot of a NASA-TLX survey
</div>

The second section of the experiment is a mission planning task. This second section is also referred to as "task 2". There are 4 trials in task 2: 1) plan a mission for one UAV without secondary task, 2) plan a mission for one UAV with secondary task, 3) plan missions for two UAVs without secondary task and with an intruder, and 4) plan missions for two UAVs with secondary task and an intruder. Before trials, the subject will watch a series of training videos that give instructions on how to use the system. After the training videos, we guide the subject through a test session where the subject needs to plan a mission that goes around an airport. Trials will begin after we are sure that the subject has learned how to use the system. A screenshot of a trial is shown in Fig. 6. The secondary task in task 2 is also verb generation, but nouns are announced every 15 seconds instead of 3 seconds.
During each trial, the subject also needs to conduct the instantaneous self-assessment (ISA)
every minute. To do so, we program the monitor to show a five red rectangles and numbers at the top left corner of the monitor every minute. After the subject clicks a rectangle that best represents the subject's perceived CL at that moment, they will disappear. At the end of every trial, the subject needs to complete a NASA-TLX survey, followed by a 5-minute break. The ISA result will be used as the reference label of the subject's CL.

 <div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/task_2.jpg" title="task 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 6: The screenshot of a trial in task 2
</div>

## Multimodal Deep Learning Framework

Estimating and predicting CL and SA in real-time is formulated as a supervised multiclass classification and regression problem. The training data is the data collected from task 1. CL labels are the results from NASA-TLX survey and SA labels are computed using the subject's indicated position and heading of all arrows. In total, three modalities that have been shown in the literature to be closely related to cognitive states are considered (EEG, eye tracker, and webcam video) [5]. The use of all modalities (EEG, eye tracker, webcam video) and multimodal deep learning for cognitive states has not been commonly found in the literature. To utilize all modalities effectively, a multimodal learning framework is proposed, shown in Fig. 7. Since the EEG data has very low signal-to-noise ratio, it is preprocessed using EEGLAB [6] to eliminate as many noises and artifacts as possible before deriving various features.

For the EEG, we derive the power spectral density (PSD) and microstates. PSD represents the proportion of the total signal power contributed by each frequency component of the EEG signals, and it is usually divided into several frequency bands: delta (0.5-4 Hz),
theta (4-8 Hz), alpha (8-13 Hz), beta (14-30 Hz), and gamma (>30 Hz). Microstates are obtained by clustering the brain's electric field configuration when the global field potential
(GFP) is at its local peak as that is usually when the EEG signal has the highest signalto-noise ratio. By backfitting the EEG signal into the found patterns, the EEG signal can be represented as a series of changes in the brain's electric field pattern. The activities of both frequency bands and microstates are found to be highly correlated to human's CL and SA. For the eye tracker, the derived features are the pupil diameter, gaze speed, and blink. For the webcam, facial landmarks are first determined with tools such as Dlib [7] and facial expression features such as eye aspect ratio, mouth aspect ratio, and nose to jaw distance are derived. Note that all derived features can be obtained in real-time.

After the preprocessing, EEG, eye tracker, and webcam video data are sent to their corresponding module, which can be any deep learning model that can learn time series data and videos in real-time. The current design chooses the transformer encoder, bidirectional encoder representations from transformers (BERT), for the strong performance and interpretability provided by the multi-head attention [8]. In addition, BERT can be modified into the video vision transformer (ViViT) [9], which is developed specifically for learning video data. After the data is encoded into input embeddings by each Module, they are concatenated and sent to a transformer decoder. The decoder combines the input embeddings and the output embedding (estimated CL and SA in the past, shown as solid lines in Fig. 7),
and outputs the current and future CL and SA. If the outputs of the multimodal learning framework are the CL and SA levels, which are classified from the labels, the evaluation metrics can be accuracy, confusion matrix, precision, recall, and F1 score. If the outputs are the raw Cl and SA scores, the evaluation metrics can be mean absolute error (MAE), mean squared error (MSE), and root mean squared error (RMSE).

There are two reasons for using a Transformer-based architecture for our Multimodal deep learning framework: 1) Performance and 2) Interpretability. Over the years, the Transformer and its variants have achieved state-of-the-art performance in natural language processing, computer vision, and also time series forecasting, anomaly detection, and classification [10].

The multi-head attention enables the Transformer to attend to long sequence data and very efficient parallel training. The encoder-decoder design also makes the Transformer versatile enough to be pre-trained and then fine-tuned to sub-tasks [8]. In addition, the multi-head attention provides insights into the temporal and feature-wise interactions [11], and build causal graphs of the input [12]. The insights can be connected with an ablation study, which can be easily conducted with the multimodal deep learning framework, to further investigate the results and prepare for realizing the framework in real operations where all modalities may not be available.

Our contributions are 1) A real-time applicable multimodal deep learning framework that utilizes three critical modalities (EEG, eye tracker, and webcam video) for CL and SA
estimation and prediction, 2) An attention and ablation study based causal analysis between features of each modality, and 3) Provide a new multi-modality dataset for cognitive states study.

 <div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/framework_cognitive.jpg" title="deep learning framework" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 7: The multimodal deep learning framework
</div>

## References

[1] M. Kassner, W. Patera, and A. Bulling, "Pupil: an open source platform for pervasive eye tracking and mobile gaze-based interaction," in *Proceedings of the 2014 ACM*
International Joint Conference on Pervasive and Ubiquitous Computing: Adjunct Publication, UbiComp '14 Adjunct, (New York, NY, USA), p. 1151–1160, Association for Computing Machinery, 2014.

[2] J. Kurland, A. Reber, and P. Stokes, "Beyond picture naming: Norms and patient data for a verb-generation task," *American Journal of Speech-Language Pathology*, vol. 23, no. 2, pp. S259–S270, 2014.

[3] Y. G. Abdullaev and M. I. Posner, "Event-related brain potential imaging of semantic encoding during processing single words," *NeuroImage*, vol. 7, no. 1, pp. 1–13, 1998.

[4] Medical Research Council, "Mrc psycholinguistic database." https://websites.psychology.uwa.edu.au/school/MRCDatabase/uwa_mrc.htm, 1990.

[5] J. Zhou, K. Yu, F. Chen, Y. Wang, and S. Z. Arshad, *Multimodal behavioral and physiological signals as indicators of cognitive load*, p. 287–329. Association for Computing Machinery and Morgan & Claypool, 2018.

[6] A. Delorme and S. Makeig, "Eeglab: an open source toolbox for analysis of singletrial eeg dynamics including independent component analysis," *Journal of Neuroscience* Methods, vol. 134, no. 1, pp. 9–21, 2004.

[7] D. E. King, "Dlib-ml: A machine learning toolkit," *J. Mach. Learn. Res.*, vol. 10, p. 1755–1758, dec 2009.

[8] J. Devlin, M.-W. Chang, K. Lee, and K. Toutanova, "Bert: Pre-training of deep bidirectional transformers for language understanding," *arXiv preprint arXiv:1810.04805*, 2018.

[9] A. Arnab, M. Dehghani, G. Heigold, C. Sun, M. Luˇci´c, and C. Schmid, "Vivit: A
video vision transformer," in *Proceedings of the IEEE/CVF International Conference* on Computer Vision (ICCV), pp. 6836–6846, October 2021.

[10] Q. Wen, T. Zhou, C. Zhang, W. Chen, Z. Ma, J. Yan, and L. Sun, "Transformers in time series: a survey," in Proceedings of the Thirty-Second International Joint Conference on Artificial Intelligence, IJCAI '23, 2023.

[11] Y. Hao, L. Dong, F. Wei, and K. Xu, "Self-attention attribution: Interpreting information interactions inside transformer," *Proceedings of the AAAI Conference on Artificial* Intelligence, vol. 35, pp. 12963–12971, May 2021.

[12] R. Y. Rohekar, Y. Gurwicz, and S. Nisimov, "Causal interpretation of self-attention in pre-trained transformers," in *Advances in Neural Information Processing Systems* (A. Oh, T. Naumann, A. Globerson, K. Saenko, M. Hardt, and S. Levine, eds.), vol. 36, pp. 31450–31465, Curran Associates, Inc., 2023.
