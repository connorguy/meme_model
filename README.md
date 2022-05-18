## Meme Image Classifier Trainer with Model Upload to Cloud Storage
#### Overview
This is an end to end model trainer for creating an image classifier for memes. Once a model is trained it is uploaded to Azure cloud storage. The following is the general flow of this trainer:

1. Meme titles are pulled using the imgflip api to get a list of meme titles.
2. This list is then used to create a Bing image search for each meme that returns a list of image URLs to be downloaded for training. 
3. Finally the training is run and the model is saved to a cloud storage to be pulled in by another service.

This notebook is run on a cadence so that a consumer of the model can pull in the latest model at any given point from cloud storage.

The model is pretty good at guessing any meme seen in the titles list, but being reliant on the imgflip api caps what is seen. The api is supposed to return the top 100 or so memes that are popular on the site, but this appears to be somewhat hit or miss in testing.

Training was based around the FastAi library and using resnet18.

---

**You can find a [pretrained model here](https://huggingface.co/connorguy/meme-classification/tree/main).**

---
#### Notebook Setup

The following os vars must be set to use Azure services:
```
AZURE_SEARCH_KEY
AZURE_STORAGE_CONNECTION_STRING
STORAGE_SHARE_NAME
```
The image search is can return a flexable number of images by setting `TRAINING_DATA_SIZE` below (with a max of 150 imgs per search).

This notebook is more or less agnostic to what service it is run on, however anything that is specific to Kaggle should be tagged with the comment `only for Kaggle`.
