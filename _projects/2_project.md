---
layout: page
title: Safe Landing
description: 
img: assets/img/ResearchThrust3.png
importance: 2
category: pillars
giscus_comments: false
---

## Safe Landing Controller

Safety assurance for Unmanned Aerial Systems (UASs) throughout their operations is crucial as UASs are becoming more of interest in our daily aerial operations. Especially during the landing phase of flight, the slow-speed environment may pose serious risks to the UASs when there is a presence of external disturbances such as wind and noise. Our analysis kickstarts the safety verification methods to ensure the UAS landing can be successful, minimizing the need for human intervention, unnecessary go-arounds, and forced landings.

# Robustness and Safety Verification of Total Energy Control System Under Disturbances
Our work on the safety verification for fixed-wing vehicle robustness applies Linear Matrix Inequality (LMI) techniques to perform safety verification of a fixed-wing aircraft's Total Energy Control System (TECS) and demonstrate the Bounded-Input Bounded-Output (BIBO) stability of the system. Our approach focuses on a continuous time longitudinal model of a fixed-wing aircraft with bounded wind disturbances. The TECS controller contains cascaded Proportional-Integral (PI) controllers which complicate the safety verification process as the integrator states must also be considered. We reconsider the TECS controller with a Linear Quadratic Regulator (LQR) with output feedback and show the PI controller gains can be autotuned. We also simulate the longitudinal states of the fixed-wing aircraft with bounded disturbances for verification of the method.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/TECS_full_diagram.png" title="tecs diagram" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    TECS Diagram
</div>

The developed tool will assist the landing and perform robustness analysis under adverse landing conditions, such as narrow runways, short runways, or inclined runways. We define the aircraft frame of references and implement disturbance wind into the system. From there, LMI techniques allow us to efficiently compute for the bounded states of the aircraft.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/aircraft-frame.png" title="vehicle reference" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Vehicle Frame of Reference with Wind
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/theta_bound_w1 1.png" title="low disturbance" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/theta_bound_w2 1.png" title="high disturbance" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Pitch State bounds with low disturbance on the left and high disturbance on the right
</div>