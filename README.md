# Description

This is a simple project for MLOps course @ HSE MLHLS. Since the main goal of this project is to try out tools like poetry and pre-commit, the DL part is rather lousy.

The task is simple: take data from https://archive.ics.uci.edu/ml/machine-learning-databases/00203/YearPredictionMSD.txt.zip and train a model on it!

# About the dataset:

Prediction of the release year of a song from audio features. Songs are mostly western, commercial tracks ranging from 1922 to 2011, with a peak in the year 2000s.

For full info see: https://archive.ics.uci.edu/dataset/203/yearpredictionmsd

# Project structure

In no particular order in the ```music_year_prediction``` folder:

* model.py - contains a LinearBlock and a LinearModel
    * LinearBlock - a basic block, made of Linear, BatchNorm and LeakyReLU
    * LinearModel - a proper model made from LinearBlocks with some functions for loading/saving/predicting/etc.

* dataset.py - contains a MusicDataset and a function to create train/test sets
    * MusicDataset - a basic adaptation of torch Dataset

* logger.py - contains a Logger class
    * Logger - logs metrics with WandB (default) or MLFlow, configurable

* trainer.py - contains a Trainer
    * Trainer - used to train the model

* utils.py - contains a couple of useful functions

Files ```train.py``` and ```infer.py``` in the repository root contain a bare minimum for you to try this project for yourself.


# Config structure

This project uses Hydra for configuration purposes. Parameters can be configured in ./configs/config.yaml and include:

* model
    * block_count - how many simple blocks you want, int
    * hidden_size - the hidden size of Linear layers, int
    * save_name - path to save the model to, str
    * pull_dvc - for inference, do you want to pull my pretrained model?, bool

* optim
    * optim_type - Adam or SGD, str
    * lr - learning rate, float

* trainer
    * epochs - how many epochs you want, int
    * batch_size - the batch size, int

* dataset
    * train_size - what portion of the dataset should be used as train, int

* logger
    * type - what logger you want: WandB or MLFlow, str
    * mlflow_uri - the MLFlow uri, defaults to 128.0.1.1:8080, str



# How to run?
* Clone the repo
* Create a new virtualenv
* Install using poetry: ```poetry install```
* Install pre-commit: ```pre-commit install```
* Check that everything is ok: ```pre-commit run -a```
* Run training: ```python train.py```
* Run inference: ```python infer.py ```
