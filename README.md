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

## Subjective summary of the results
* It is easy to go above 97% accuracy, and hard to go above 99%
* Maximum observed for the MobileNet was 98.5(+-1.2)%, and for the simpler model 98.8(+-0.8)% (see below).
* If you stay close to the defaults, you do not get a significant change in the accuracy.
* Using data-augmentation is not a large (but significant) improvement, especially when using the simpler architecture.
* Order-of-magnitute changes in learning rate and batch size can be observed to result in a deterioration of about few percentage points. But the optimum seems to have been close to the deafults in this case.

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
model | no. layers | no. parameters | initialization
--- | --- | --- | ---
A | 15 | 457 k | random
B | 160 | 2620 k | imagenet

## The results
They were obtained in the notebook [https://github.com/olszewskip/Sign_Language/blob/master/sign_language_DL_with_CV.ipynb].

In the notebook You'll find markdown text intertwined with (mostly short) blocks of pythonic code. Some sample images are also displayed there. You'll also have to look into the notebook, if You're interested in exact values of all other hyperparameters (including e.g. definition of the data-augmentation).

model | batch size | adam's learning rate | augmentation | mean accuracy in CV | 2 * std(accuracy) in CV
---   | ---        | ---                  | ---          | ---                 | ---
A     |		64 	|  0.0004  	| yes 		| 0.9884 	| 	0.0077
A     |		32 	| 	0.0004 	| 	yes 	| 0.9845 	| 	0.0184
A     |		32 	| 	0.0010 	| 	yes 	| 0.9811 	| 	0.0227
A     |		64 	| 	0.0001 	| 	yes 	| 	0.9801 	| 	0.0220
A     | 	32 	| 	0.0001 	| 	yes 	| 	0.9748 	| 	0.0281
A     |		128 | 	0.0004 	| 	yes   | 	0.9739 	| 	0.0241
A     |	  128 | 	0.0001 	| 	yes 	| 	0.9738	|  	0.0188
A     |		128 | 	0.0010 	| 	yes 	| 	0.9710 	| 	0.0415
A     |		32 	| 	0.0010 	| 	no 		| 0.9694 	| 	0.0065
A     |		128 | 	0.0010 	| 	no 	| 	0.9650 	| 	0.0179
A     |		64 	| 	0.0010 	| 	no 	| 	0.9646 	| 	0.0274
A     |		32 	| 	0.0004 	| 	no 	| 0.9616 	  | 	0.0299
A     |	  64	| 	0.0004 	|  no 	| 	0.9574 	| 	0.0267
A     |		32 	| 	0.0001 	| 	no 	| 	0.9544 	| 0.0325
A     |		128	| 	0.0004 	| 	no 	| 	0.9496 	| 	0.0070
A     |	 	128	| 	0.0001 	| 	no 	| 	0.9422 	| 	0.0425
A     |		64 	| 	0.0001 	| 	no 	| 	0.9399 	| 	0.0315
A     |		64 	| 	0.0010 	| 	yes | 	0.9072 	| 	0.2182
B |	32  | 	0.0004  | 		yes  | 		0.9845  | 		0.0118
B |	 	128  | 		0.0004  | 		yes  | 		0.9811  | 		0.0140
B |		64 	 | 	0.0001  | 		yes  | 		0.9811  | 		0.0132
B |	 	128  | 		0.0010 | 	 	yes  | 		0.9802  | 		0.0166
B |		128  | 		0.0010 | 	 	no  | 		0.9777  | 		0.0174
B |		64 | 	 	0.0004 | 	 	yes  | 		0.9772  | 		0.0143
B |		32  | 		0.0001 | 	 	yes  | 		0.9747  | 		0.0226
B |		64  | 		0.0010  | 		yes 	 | 	0.9738  | 		0.0215
B |		32  | 		0.0004  | 		no  | 		0.9738  | 		0.0144
B |		64  | 		0.0010  | 		no  | 		0.9719  | 		0.0448
B |		32  | 		0.0010  | 		yes  | 		0.9718  | 		0.0290
B |	64  | 		0.0004  | 		no  | 		0.9714  | 		0.0147
B |	128  | 		0.0004  | 		no  | 		0.9700  | 		0.0165
B |		128  | 		0.0001 	 | 	yes  | 		0.9695  | 		0.0227
B |		32  | 		0.0001  | 		no 	 | 	0.9544  | 		0.0315
B |		32  | 		0.0010  | 		no  | 		0.9474 | 	 	0.0722
B |		64  | 		0.0001  | 		no  | 		0.9422  | 		0.0199
B |		128  | 		0.0001  | 		no  | 		0.9078  | 		0.0353
