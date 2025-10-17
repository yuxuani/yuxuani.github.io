---
layout: page
title: SensorGAN
description: Facial Paresis Analysis with CycleGAN
img: assets/img/project_covers/mindfield-biosystems-NnKXOTBJvfQ-unsplash.jpg
importance: 2
category: work
---

***Removing the sensors -- Facial Feature Reconstruction with CycleGAN in Facial Palsy Patients***

This study explores the use of Deep Learning, specifically CycleGAN (Zhu, 2017), to reconstruct facial features obscured by sEMG sensors in patients with facial palsy. The model removes visual obstructions like sEMG sensors while preserving facial features and natural expressions.

**Tech**: CycleGAN ·  Generative Adversarial Networks · Deep Learning ·PyTorch · Computer Vision

The approach builds on the earlier work led by one of our colleagues (Büchner, 2023), which initially focused on healthy subjects. In our extension, we applied the model to medically complex cases of unilateral synkinetic chronic facial palsy, where asymmetrical muscle activity and involuntary co-activations introduce additional challenges. We conducted systematic evaluations across multiple recording sessions and different facial movement tasks. Both quantitative metrics—including SSIM, LPIPS, and FID—and qualitative visual assessments were used to measure reconstruction accuracy, realism, and preservation of facial identity. Our analysis showed that the model performs best when trained and tested on data from the same recording session, while LPIPS scores were the most consistent with perceived visual quality.

These findings suggest that GAN-based reconstruction has the potential to restore obscured facial features of facial palsy patients and provide useful insights for research and clinical applications. While the results are promising, further investigation is needed to fully understand its limitations and generalization across diverse patient populations.

## Reference
[Project: Bridging the Gap – Mimics and Muscles](https://inf-cv.uni-jena.de/home/research/learning3d/facial-paresis-analysis/)

Zhu, Jun-Yan ; Park, Taesung ; Isola, Phillip ; Efros, Alexei A.: Unpaired Image-To-Image Translation Using Cycle-Consistent Adver- sarial Networks, 2017, 2223–2232

Büchner, Tim ; Guntinas-Lichius, Orlando ; Denzler, Joachim: Improved Obstructed Facial Feature Reconstruction for Emotion Recognition with Minimal Change CycleGANs. In: Blanc-Talon, Jaques (Hrsg.) ; Delmas, Patrice (Hrsg.) ; Philips, Wilfried (Hrsg.) ; Scheunders, Paul (Hrsg.): Advanced Concepts for Intelligent Vision Systems. Cham : Springer Nature Switzerland, 2023 (Lecture Notes in Computer Science). – ISBN 978–3–031–45382–3, S. 262–274