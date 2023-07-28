# Preposition-Error-Correction-Tool

## Abstract

Prepositions are one of the most challenging units encountered by second language learners of English. They are
frequently used and are highly polysemous in nature. Moreover, their usage is highly dependent upon the underlying
context of the sentence and the intent of the speaker which turns out to be a major challenge in developing a
preposition correction system. In this paper, we present a preposition error correction system which is a sequence
tagger based on a transformer encoder that predicts token-level edit operations to remove preposition errors from a
given sentence. Our system is trained over synthetic data constructed using Google's One billion word benchmark
corpus. For training, we used a new optimiser - Ranger which is a combination of Rectified Adam and Look Ahead
optimiser. It helped to reduce the time required for training by about 6 folds. Our system outperformed
state-of-the-art approaches and achieved precision, recall and f0.5 score of 91.4, 77.27 and 88.27 respectively on a
dataset prepared from preposition exercises collected from different websites and grammar books.


## Introduction

In the past few years, Neural Machine Translation approaches and Transformer based sequence-to-sequence models have been extensively used for the task of grammatical error correction and are known to produce state-of-the-art results over benchmark gec1 datasets[12]. However, almost all of these approaches have been applied to a bigger task of grammatical error correction and very few have analysed the performance of the Transformer based encoder- decoder models specifically on the task of preposition error correction. Also, there are some drawbacks of them which make them inconvenient for practical use, like:
1. Slow training.
2. Demand for large amounts of annotated training data.
 
 We have used an iterative sequence tagger based on a transformer encoder to predict token-level edit operations [4] for correcting the preposition errors in a sentence. For each source token in the input sentence, a softmax layer on the top of the encoder predicts an edit operation out of a confusion set. The system predicts four basic edit operations namely keep a token, delete a token, append a token and replace a token. The system is trained over a synthetic dataset constructed by us using Google's one billion word corpus[37]. Additionally, we have incorporated in our training procedure the new state-of-the-art Ranger2 optimiser which is a combination of Rectified Adam and lookahead optimiser. It is known to outperform all other optimisers for the image classification task on the Imagewoof dataset3. However, not much analysis has been done on the performance of the optimiser in the field of natural language processing which proved to be a motivation for us to incorporate it into our system.
Some improvements of our system over the previously discussed approaches are:
● Ranger optimiser helps to increase the speed of training and also the accuracy of the system.
● Synthetic data eliminates the need for large quantities of human-annotated data. Small and diverse datasets will serve the purpose of augmenting large datasets for training.


## Method

Our proposed system is an iterative sequence tagger which is inspired by GECToR[4]. It is an encoder made up of a pre-trained BERT-like transformer- xlnet [40] stacked with two linear layers and softmax layers on the top. The system is trained for tagging each token xi in the input (incorrect) sentence (x1....xN) with a token-level transformation T(xi) discussed in section 1.2. These predicted tag-encoded transformations are then applied to the input sentence to recover the output sentence. We have used iterative tagging as it may take more than one iteration of prediction and correction for sentences having multiple preposition errors. The steps involved in the construction of our system are given as follows:
1. Construction of the dataset
2. Preprocessing of data.
3. Training.
4. Evaluation.

Each step has been discussed in detail in the
following sections.

![image](https://github.com/NalinC2002/Preposition-Error-Correction-Tool/assets/76205943/336ca1fc-3db0-4dd2-9712-fe12dcdd16fe)

Most of the Neural Machine Translation approaches have used gold standard publicly available annotated datasets for training their neural-network models. However, we couldn’t use the same data to train our preposition correction model because of the following reasons:
1. It consisted of all types of grammatical errors while we needed a dataset containing only preposition errors.
2. We required a large annotated dataset for training our model while the available public datasets are small in size. Therefore, we constructed a synthetic dataset to train our model by recording the commonly made preposition errors and their frequencies from the public datasets and then introducing them into a clean native dataset.


## Results

We evaluated our models on the CoNLL- 2014 test set, BEA-2019 test dataset and on a dataset of 106 sentences containing preposition exercises collected from the web and grammar books. We evaluated our system with ERRANT9. A comparison of our results with other gec tools is given in the table below. It is clear from the results that our model performs better than other approaches on the third dataset containing preposition exercises. It is also noticeable that the f-score is comparatively less than other approaches when tested over the public datasets. 

![image](https://github.com/NalinC2002/Preposition-Error-Correction-Tool/assets/76205943/f76bbe51-24d2-4412-8f65-2b19259643e4)
