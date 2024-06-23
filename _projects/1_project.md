---
layout: page
title: Cognitive Modelling
description: 
img: assets/img/cl_background.jpg
importance: 1
category: pillars
related_publications: false
---

## Overview

Cognitive modeling is a critical part for realizing AIDA3's vision. In general, there are ve research questions related to this topic: 1) how to dene and quantify cognitive load (CL) and situation awareness (SA); 2) how to classify and predict CL and SA in real time; 3) can we quantify operators' expertise using CL and SA during a mission; 4) what is the minimal set up for answering research question 2) and 3); 5) how to design the system so that CL and SA never exceed the safety thresholds.

CL and SA are two separate concepts. Together, they describe a person's cognitive states. In general, CL can be interpreted as the amount of mental eort and resources required to process information, perform tasks, or solve problems, and SA can be interpreted as the perception of the elements in the environment within a volume of time and space, the comprehension of their meaning, and the projection of their status in the near future. In recent years, estimating CL and SA via various sensors and machine learning techniques has become popular. Among all sensors, electroencephalography (EEG) and eye tracker are the most popular due to their non-intrusive nature. An extensive research has been done. Nevertheless, there exist several research gaps. Firstly, it is well known that human's cognitive states consist of multiple modalities. For instance, CL is found to be related to both brain's activities and eye movements. However, the majority of the works only consider one modality when they model CL and SA. Secondly, although machine learning algorithms such as the support vector machine and random forest are widely used for estimating CL and SA with physiological data, deep learning models such as convolutional neural network or recurrent neural network are rarely used. This is because the size of the experiment data is usually too small to fully take advantages of deep learning models. Thirdly, current works mostly estimate CL and SA in a short and simple scenarios and they do not demonstrate the real-time applicability. Based on the aforementioned research gaps, we design an experiment and collect data using sensors for various modalities (EEG, eye tracker, and webcam), and propose a multimodal deep learning model. Within the experiment, there are two tasks, one is a simple visual tracking task that aims to collect physiological data in a controlled environment, and the other one is a mission planning task that aims to collect physiological data in a realistic environment. The multimodal deep learning model utilizes and combines the extracted features from each sensor to estimate and predict CL and SA in real-time.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/willis.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images, edit it however you want, and even put citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
