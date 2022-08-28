# MT-MLforACI
Master's Thesis: Machine Learning Approaches for Estimating the Causal Effects of Aerosols on Clouds

This repository contains my work for my Master Thesis, where I studied ML approaches for studying aerosol cloud interactions (ACI)

| **[Abstract](#abstract)**
| **[Citation](#citation)**
| **[Installation](#installation)**
| **[Data](#data)**
| **[Runs](#runs)**

## Abstract

## Citation

My work is based on the following paper: [Scalable Sensitivity and Uncertainty Analyses for Causal-Effect Estimates of Continuous-Valued Interventions](https://arxiv.org/abs/2204.10022). 

The original code base can be found here: [overcast](https://github.com/anndvision/overcast). 

## Installation

```.sh
git clone git@github.com:msolal/MT-MLforACI.git
cd MLforACI
conda env create -f environment.yml
conda activate overcast
pip install -e .
```

## Data

We suggest that the data is stored in MT-MLforACI/data.

To download the low resolution Pacific dataset:

```.sh
cd data
wget -P data/ "https://github.com/anndvision/data/raw/main/jasmin/four_outputs_liqcf_pacific.csv"
```

## Runs

### Neural Network 

Example of command to train the neural network on the low resolution Pacific dataset:

```.sh
overcast \
    train \
        --job-dir output/ \
        --gpu-per-model 1 \
    jasmin \
        --data-dir data \
        --dataset four_outputs_liqcf_pacific \
        -c RH900 \
        -c RH850 \
        -c RH700 \
        -c LTS \
        -c EIS \
        -c W500 \
        -c SST \
        -t AOD \
        -o re \
        -o COD \
        -o CWP \
        -o LPC \
    appended-treatment-nn \
        --batch-size 224 \
        --beta 0.0 \
        --depth 2 \
        --dim-hidden 256 \
        --dropout-rate 0.09 \
        --ensemble-size 10 \
        --epochs 9 \
        --layer-norm false \
        --learning-rate 0.0002 \
        --negative-slope 0.1 \
        --num-components-outcome 5 \
        --num-components-treatment 2 \
        --spectral-norm 0.0
```

### Transformer 

Example of command to train the transformer on the low resolution Pacific dataset:

```.sh
overcast \
    train \
        --job-dir output/ \
        --gpu-per-model 1 \
    jasmin \
        --data-dir data \
        --dataset four_outputs_liqcf_pacific \
        -c RH900 \
        -c RH850 \
        -c RH700 \
        -c LTS \
        -c EIS \
        -c W500 \
        -c SST \
        -t AOD \
        -o re \
        -o COD \
        -o CWP \
        -o LPC \
    appended-treatment-nn \
        --batch-size 224 \
        --beta 0.0 \
        --depth 3 \
        --dim-hidden 8 \
        --dropout-rate 0.42 \
        --ensemble-size 10 \
        --epochs 500 \
        --layer-norm false \
        --learning-rate 0.0001 \
        --negative-slope 0.28 \
        --num-components-outcome 22 \
        --num-components-treatment 27 \
        --spectral-norm 0.0
```
