<!--
*** Thanks for checking out this README Template. If you have a suggestion that would
*** make this better, please fork the repo and create a pull request or simply open
*** an issue with the tag "enhancement".
*** Thanks again! Now go create something AMAZING! :D
-->




<!-- PROJECT LOGO -->
<br />
<p align="center">

  <h3 align="center">Discovering small-molecule senolytics with deep neural networks</h3>

  <p align="center">
    Supporting code for the paper
  </p>
</p>



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Code](#about-the-code)
* [Running the code](#running-the-code)
  * [Checkpoint files](#checkpoint-files)
  * [Usage](#usage)
* [Contact](#contact)



<!-- ABOUT THE PROJECT -->
## About the Code

The files in this repository contain a Jupyter notebook and final Chemprop checkpoints for the models described in the paper "Discovering small-molecule senolytics with deep neural networks", published in <i>Nature Aging</i> (2023). The code requires <a href="https://github.com/chemprop/chemprop">ChemProp</a> and Python with the appropriate packages installed. In particular, please ensure that at least the following two packages are installed:
<ul>
<li><a href="https://github.com/chemprop/chemprop">Chemprop</a> (commit 9c8ff4074bd89b93f43a21adc49b458b0cab9e7f was used)</li>
<li><a href="https://www.rdkit.org/">RDKit</a> (version 2021.09.01 was used)</li>
</ul>
Details on installation, the packages required, and the Jupyter notebook code platform are provided below.

<!-- GETTING STARTED -->
## Running the code

### Jupyter notebook

The Jupyter notebook is the main accompanying file to the paper, "Discovering small-molecule senolytics with deep neural networks". It reproduces the Chemprop model training and prediction steps used in the paper, thereby providing an integrated platform for interested readers to develop and apply their own Chemprop models to senolytic compound discovery.

Key dependencies for the Jupyter notebook:


<ul>
<li>requirements.txt: A Python requirements file detailing all the package dependencies needed to successfully execute all commands in this notebook.
</li>
<li>train.csv: A CSV file containing the SMILES strings and activity values of compounds in the training set. The default file provided is the training set of 2,352 compounds described in the main text, with activity values defined by the cell viability criteria described in the main text. There are a total of 45 active (ACTIVITY=1) compounds; the remaining compounds are inactive (ACTIVITY=0).
</li>
<li>
hyperparameters.json: A JSON file containing key hyperparameters specifying the architecture of the Chemprop model used. By default, the parameters used are: depth=2, dropout=0.0, ffn_num_layers=3, and hidden_size=600, as detailed further in the Methods section of the main text.
</li>
<li>test.csv: A CSV file containing the SMILES strings of compounds for which Chemprop predictions of senolytic activity will be made. The default file provided is the set of 266 curated and experimentally tested compounds in our study, a subset of the 804,959 compounds described in the main text; this smaller subset was provided to facilitate evaluation for setups with less computational power. For the full set of compounds computationally evaluated in the paper, please refer to Supplementary Dataset 2. 
</li>
</ul>

### Checkpoint files

In the folder entitled "checkpoints", there are 20 ChemProp checkpoints files, which correspond to the ensemble of 20 final Chemprop models described in the paper. These checkpoint files may be used to predict senolytic activity following the chemprop_predict command used in the Jupyter notebook.


## Usage

### Installation and dependencies for the Jupyter notebook

Dependencies for successful execution of the notebook are described in the "requirements.txt" file. It is important to have Chemprop installed. Our recommended way of doing so is to follow the <a href="https://github.com/chemprop/chemprop">Official Instructions</a> using Conda: at the command line, enter:

<ul>
<li>conda create -n chemprop python=3.8</li>
<li>conda activate chemprop</li>
<li>conda install -c conda-forge rdkit</li>
<li>pip install git+https://github.com/bp-kelley/descriptastorus</li>
<li>pip install chemprop</li>
</ul>

These commands will help install Chemprop and associated dependent Python packages (the accompanying "environment.yml" file details all of Chemprop's dependencies). In order to access Chemprop from the Jupyter notebook, assuming that Jupyter notebook has not been installed in the Chemprop environment, run the following commands at the command line:

<ul>
<li>conda activate chemprop</li>
<li>conda install jupyter</li>
<li>conda install notebook</li>
<li>jupyter notebook</li>
</ul>

The last command should launch the Jupyter notebook. All cells in the notebook can then be executed to reproduce (using just one Chemprop model, and not an ensemble of 20) the Chemprop model training and prediction steps used in the paper. This provides an integrated platform for interested readers to develop and apply their own Chemprop models to senolytic compound discovery.

### Checkpoint files

The checkpoint directory, which contains all 20 pre-trained Chemprop models used for the final predictions made in our study, can also be passed directly into Chemprop (using the Jupyter notebook if one desires) to generate new predictions. For instance, for SMILES strings that are listed in a file "test.csv", please run:
```sh
chemprop_predict --test_path test.csv --checkpoint_dir "./checkpoints" --preds_path "predictions.csv" --features_generator rdkit_2d_normalized --no_features_scaling
```
This will tell chemprop_predict to use all of the checkpoints (in the same directory as the Jupyter notebook) to make predictions of senolytic activity. The resulting prediction scores are the average of all 20 Chemprop models in the ensemble. 

<!-- CONTACT -->
## Contact

For questions or comments about this repository, please reach out to felix j wong at gmail (no spaces, add domain name). 

