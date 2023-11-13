# Machine Anomaly Detection using Wavenet

## Introduction

Following the lecture on CNNs and RNNs, you will work on a causal 1D CNN model called [Wavenet](https://arxiv.org/abs/1609.03499) to detect anomalous sounds events as described in [this paper](https://www.eurasip.org/Proceedings/Eusipco/Eusipco2018/papers/1570437578.pdf). 

The following video provides a good overview of the application space of Wavenet to **generate** speech - it is used across many Alphabet services.

```{eval-rst}

.. youtube:: 9eLNUB62HRI
   :width: 560
   :height: 315
   :align: center
   :target: https://www.youtube.com/watch?v=9eLNUB62HRI
   :alt: Generative Time Series Models - WAVENET
```

## Task 1 - Code the Wavenet model (35 pioints)

Use Tensorflow / Keras  implementation of Wavenet (see the example in your textbook) or the equivalent in Pytorch. 

Note that in your case you will use Wavenet to **detect** anomalous sounds events which means that you will use wavenet as a **predictor** rather than a **generator**. Therefore the architecture will be slightly different especially in the head. 

Your code must match the architecture shown in the paper and should include post-processing steps. Please note that the authors do not mention about any multichannel input (each channel is a different microphone) and the dataset provides for those. You need to try to accommodate them in your model. 
 
## Task 2 - Prepare and consume the Training and Test Datasets (35 points)

For evaluating the model, you will use this [dataset](https://arxiv.org/pdf/1908.03299.pdf) for the toy car sub-dataset for the continuous (CNT) data collection. The data can be downloaded [here](https://zenodo.org/records/3351307#.XT-JZ-j7QdU) but you need to have a significant disk space to extract the 7z files. **Avoid downloading the dataset** from this original URL that is provided here for information only - we have prepared a streaming dataset version based on the webdataset spec that you can find in [the Hugging Face Hub](). 

**NOTE: The author is in the process of releasing the webdataset version of the dataset. Please check back later.**

You need to use [TorchData](https://pytorch.org/data/beta/index.html) to stream the data from the Hugging Face Hub and either process the data online for training & evaluation purposes or create a subset of the dataset for training and evaluation as required for your model. You may use [Audio WebDataset extension](https://github.com/archinetai/audio-data-pytorch) to help you with consuming the audio files by the rest of the pipeline.

The authors have published [this github repp](https://github.com/YumaKoizumi/ToyADMOS-dataset) where you can find the training and test dataset processing steps that you may borrow.

## Task 3 - Train and Evaluate the Model (30 points)

Perform model training and specify clearly the hyper-parameters you used, showing an attempt to optimize them. You need to include a plot of loss vs number of epochs for the test dataset and report the F1 score. 