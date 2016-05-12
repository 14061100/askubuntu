## AskUbuntu Question Dataset

This repo contains a preprocessed collection of questions taken from [AskUbuntu.com](http://www.askubuntu.com). It also comes with 400*20 mannual annotations, marking pairs of questions as "similar" or "non-similar".

### Reference
[1] [Semi-supervised Question Retrieval with Gated Convolutions](http://arxiv.org/abs/1512.05726). Lei et. al. NAACL 2016

### Files
  - text_tokenized.txt.gz is the corpus file
  - train_random.txt
  - dev.txt and test.txt
  - heldout.txt
  - vector/vectors_pruned.200.txt.gz

### Formats

#### 1. Corpus file ``text_tokenized.txt.gz``
Each line of the corpus file contains three fields seperated by tab "\t" -- (1) the question ID, (2) the list of words in question title, and (3) the list of words in question body. For instance:
```
9     how do i enable automatic updates ?    update manager is constantly offering me updates ( e.g . security fixes , updates from ppas ) . how can i tell my ubuntu installation to automatically download and install updates whenever they become available ?
11    how do i install adobe flash player ?   i have had significant problems with watching flash video in 64-bit ubuntu . does anyone know of a good way to get flash running on the platform ?
```
The question bodies are truncated at a maximum of 100 words. There are 167K questions in total.

<br>

#### 2. Training file ``train_random.txt``
Each line of this file has also three fields, namely (1) the query question ID, (2) the list of similar question IDs, and (3) the list of randomly selected question IDs. 
```
240299    168608 390642   368007 70009 48077 376760 438005 228888 142340 220049 195789 25591 ...
121116    278152 46624 291050   373136 325070 114969 366710 234216 379879 343950 237685 286190 ...
```
The list of similar questions are user-marked duplicates in AskUbuntu. The random questions are used as negative examples during training. 

<br>

#### 3. Human annotations for evaluation ``dev.txt`` ``test.txt``
Each line contains (1) the query question ID, (2) the list of similar question IDs, (3) the list of non-similar question IDs and (4) the associated BM25 scores of these questions computed by the Lucene search engine. The number of similar or non-similar questions for each query is 20 in total, and there are 200 query questions in each of the file.
```
501754    399513 491992 218016 50146 456861     399513 491992 218016 459246 17630 50146 144028 269913 438505 416899 428574 23596 456861 400442 23731 386606 396630 462024 313023 419839    29.87237 28.53559 28.197691 26.987028 24.890223 24.815313 24.733963 24.114239 23.958801 23.728823 23.62108 23.566372 23.409262 22.863033 22.843576 22.579468 22.531168 22.23379 22.026878 22.001768
408066    132837 157668   219491 132837 251348 470629 279126 288347 133390 131053 261114 389546 150574 125455 51420 157668 363403 38026 354685 270025 24213 87279    36.245964 35.97274 34.907314 34.627953 34.331802 34.014793 33.55112 33.326748 33.212143 33.181896 33.129414 33.081596 32.86806 32.53924 31.769056 31.455008 31.166483 31.027262 30.502405 30.370914
```
For similar question retrieval (or classification) task, the BM25 scores can be used as a baseline, or as additional features for model combination.

**Note:** a few of the queries have zero similar questions among the 20 candidates, which we excluded during evaluation.

<br>

#### 4. Heldout questions ``heldout.txt``
This file simply contains a list of question IDs that is held out from the training. This set can be used for evaluating language model or summarization model etc.

<br>

#### 5. Pre-trained word vectors ``vectors_pruned.200.txt.gz``
We also provide a set of 200-dimension pre-trained word vectors. We used this set for our experiments. 

<br>

#### To-do
  - [x] better description of data
  - [ ] put raw corpus in this repo ?
  - [ ] put AskUbuntu 2015 version instead of 2014 version as additional resource ?
