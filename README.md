# Image MNIST-like classification

## The dataset
* made public with Apache License 2.0 in the repository https://github.com/ardamavi/Sign-Language-Digits-Dataset
* 10 classes of about 200 photes per class = 2k photos in total
* each photo is of a one digit (from the 0-9 range) "spoken" in sign language
* right hands of various individuals are used
## The goal here
* To present a simple pipeline for training and comparing various deep models.
* By a single model we mean a fully defined, compilable, trainable algorithm whose performance is measurd in cross-validation
* We search (a part of) the space of models in the so called grid-search with 5-fold cross-validation collecting a model's mean accuracy and the accuracies' standard devation.

## Subjective summary of the result
* It is easy to go above 96% accuracy, and hard to go above 98%
* If you stay close to the defaults, you do not get a significant change in the accuracy.
* Using data-augmentation was also not a significant modification.
* Order-of-magnitute changes in learning rate and batch size can be observed to result in a deterioration of about few percentage points. But there is no universal rule in sight: the minimal grid that we have covered in the search did not reveal a clear gradient, and the effect is dependent on the architecture.
* Maximum observed for the MobileNet was 98(+-2)%, and for the simpler model 97(+-1)%.


## The models
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
model | no. layers | no. parameters
--- | --- | ---
A | 15 | 457 k
B | 160 | 2620 k

## The results
They were obtained in the notebook [https://github.com/olszewskip/Sign_Language/blob/master/sign_language_DL_with_CV.ipynb].

In the notebook You'll find markdown text intertwined with (mostly short) blocks of pythonic code. Some sample images are also displayed there. You'll also have to look into the notebook, if You're interested in exact values of all other hyperparameters (including e.g. definition of the data-augmentation).

model | batch size | adam's learning rate | augmentation | mean accuracy in CV | 2 * std(accuracy) in CV
---   | ---        | ---                  | ---          | ---                 | ---
A |	32 |	0.0004 |	no |	0.9709 |	0.0081
A |	32 |	0.0004 |	yes |	0.9694 |	0.0040
A | 32 |	0.0010 |	no |	0.9636 |	0.0268
A |	128 |	0.0004 |	yes| 	0.9607 |	0.0101
A |	32 |	0.0010 |	yes |	0.9588 |	0.0130
A | 	64 |	0.0010 |	no |	0.9588 |	0.0207
A |	64 |	0.0004 |	yes |	0.9582 |	0.0248
A |	128 |	0.0004 |	no |	0.9573 |	0.0223
A |	64 |	0.0004 |	no |	0.9548 |	0.0273
A |	128 |	0.0010 |	no |	0.9539 |	0.0207
A |	128 |	0.0010 |	yes| 	0.9529 |	0.0469
A |	64 |	0.0010 |	yes| 	0.9506 |	0.0210
A |64 |	0.0001 |	yes |	0.9496 |	0.0194
A |64 |	0.0001 |	no 	|0.9481 |	0.0155
A |32 |	0.0001 |	no |	0.9476 |	0.0227
A |32 |	0.0001 |	yes |	0.9438 |	0.0397
A |	128 |	0.0001 |	no |	0.9374 |	0.0263
A |	128 |	0.0001 |	yes |	0.9374 |	0.0440
B |	128 |	0.0010 |	yes |	0.9821 |	0.0162
B |	32 |	0.0004 |	no |	0.9806 |	0.0129
B |	128 	|0.0010 	|no |	0.9792 |	0.0160
B |	64 |	0.0004 |	yes |	0.9792 |	0.0206
B |	32 |	0.0010 |	yes |	0.9758 |	0.0224
B |	32 |	0.0004 |	yes |	0.9757 |	0.0412
B |	64 |	0.0010 |	no |	0.9724 |	0.0244
B |	128 	|0.0004 |	yes |	0.9724 |	0.0100
B |	128 |	0.0004 |	no |	0.9680 |	0.0197
B |	64 |	0.0010 |	yes |	0.9676 |	0.0349
B |  64 	|0.0004 	|no |	0.9656 |	0.0345
B |	32 |	0.0010 |	no |	0.9622 |	0.0383
B |	32 |	0.0001 |	yes |	0.9617 |	0.0211
B |	32 |	0.0001 |	no |	0.9529 |	0.0482
B |	64 |	0.0001 |	yes |	0.9461 |	0.0265
B |	64 |	0.0001 |	no |	0.9344 |	0.0374
B |	128 |	0.0001 |	no |	0.9098 |	0.0207
B |	128 	|0.0001 |	yes |	0.9049 |	0.0279
