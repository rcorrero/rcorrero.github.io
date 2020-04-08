---
title: Aprilis – 0.1
created: '2020-04-08T15:02:16.098Z'
modified: '2020-04-08T15:11:47.620Z'
---

# Aprilis – 0.1

## Goals
- Development of a functional framework for creating well-founded statistical models using deep models as inputs. In particular, using the transfer learning method from [this paper](https://science.sciencemag.org/content/sci/353/6301/790.full.pdf?casa_token=IGFOJXgxvdYAAAAA:TSJ7AHkOLDHdUlyEDoHBwwXvdBKQJRost_Qp5YxaAHIUAeOE8enNIUybJ_zpf3mKPTkIWor-v6JtlA), use pretrained models to generate features based on input satellite imagery. Combine these deep features with shallow features which are application-specific, fit a (regularized) regression model over both types of features to predict some dependent variable of interest, i.e. land-value, etc. Using a pretrained model as a base on which to build domain-specific neural classifiers requires adding neural layers and the associated modifications – learn how to do this.

- This framework should encapsulate the structural similarities between the model herein developed and the model of [Germinal](https://projects.richardcorrero.com/notes/germinal.html).
