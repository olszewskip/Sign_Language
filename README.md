# Image MNIST-like classification
---
## The dataset
* made public with Apache License 2.0 in the repository https://github.com/ardamavi/Sign-Language-Digits-Dataset
* 10 classes of about 200 photes per class = 2k photos in total
* each photo is of a one digit (from the 0-9 range) "spoken" in sign language
* right hands of various indyviduals are used
## The goal here:
* To present a simple pipeline for training and comparing various deep models.
* By a single model we mean a fully defined, compilable, trainable algorithm whose performance is measurd in crossvalidation
* We search (a part of the) space of models in the so called grid-search with 5-fold cross-validation.
## The results
They were obtained in the notebook [] using Colab.

In the notebook You'll find markdown text intertwined with (mostly short) blocks of pythonic code. Some sample images are also displayed. You'll also have to look into the notebook, if You're interested in exact model architectures and values of all other hyperparameters (including e.g. definition of the data-augmentation).
```
model A =
Conv2D(32,  (3,3)) | MaxPool(3,3) | BatchNorm |
Conv2D(64,  (3,3)) | MaxPool(3,3) | BatchNorm |
Conv2D(128, (3,3)) | MaxPool(3,3) | BatchNorm |
Flatten | Dense(256) | Dropout(0.3) | Dense(256) | Dense(10)
```
```
model B =
MovileNet_V2 |
GlobalMaxPool |
Dense(256) | Dropout(0.3) | Dense(256) | Dense(10)
```
model | batch size | adam's learning rate | augmentation | mean accuracy in CV | 2 * std(accuracy) in CV
---   | ---        | ---                  | ---          | ---                 | ---
A     | 32         | 0.0001               | no           |                     |
A     | 32         | 0.0001               | no           |                     |
