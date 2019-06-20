---
layout: post
title: "How to avoid doing semi-supervised learning"
---

Semi-supervised learning is useful but complex, so it's better to achieve the same thing by simpler means.


[PUAUC is proportionate to AUC](http://www.machinedlearnings.com/2012/03/pu-learning-and-auc.html)

Ok so now think about F1 - it is based on the confusion matrix and you can optimise any confusion matrix metric with class weights. AUC is just a weighted average of F1 scores. Daisy chain it all together, and you can do PU learning by optimising AUC with class weights.