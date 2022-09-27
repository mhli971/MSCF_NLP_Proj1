# MSCF NLP Project 1: Replication of the Liability Paper

## README

This repo contains notebooks and a MD report (see below) for MSCF NLP course project 1.

Authors: Lin Cui， Yuchen Rui, and Mohan Li. Responsibility: Lin Cui (pulling down 10Q/10K files), Yuchen Rui (parsing and calculating scores based on weights and dictionaries), Mohan Li (calculating access returns on S&P500 companies and matching those with company filing reports, yielding the final plot). We worked on our parts independently and reconvene after we finished to cross check and understand each other's part.

Notebooks:
- `dump_data_lin.ipynb`: pulling down 10Q/10K files from EDGAR
- `process_data_yuchen.ipynb`: parsing and calculating scores based on weights and dictionaries
- `plot_mohan.ipynb`: calculating access returns on S&P500 companies and matching those with company filing reports, yielding the final plot

## Report

Cuilin goes here, set up your own section name

Yuchen goes here, set up your own section name

### Return calculation, data match, and plot generation

#### Data
I download the S&P500 daily return data from WRDS:

<img width="279" alt="Screen Shot 2022-09-27 at 01 07 06" src="https://user-images.githubusercontent.com/50337211/192436760-71bc234e-c3c5-490e-b0f8-0b4cf02f0b32.png">

I download the individual stock return data using `yfinance`:
