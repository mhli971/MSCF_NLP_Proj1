# MSCF NLP Project 1: Replication of the Liability Paper

## README

This repo contains notebooks and a MD report (see below) for MSCF NLP course project 1.

Authors: Lin Cui, Yuchen Rui, and Mohan Li. Responsibility: Lin Cui (pulling down 10Q/10K files), Yuchen Rui (parsing and calculating scores based on weights and dictionaries), Mohan Li (calculating access returns on S&P500 companies and matching those with company filing reports, yielding the final plot). We worked on our parts independently and reconvene after we finished to cross check and understand each other's part.

Notebooks:
- `dump_data_lin.ipynb`: pulling down 10Q/10K files from EDGAR
- `process_data_yuchen.ipynb`: parsing and calculating scores based on weights and dictionaries
- `data_ret_mohan.ipynb`: downloading individual stock return data from `yfinance`
- `plot_mohan.ipynb`: calculating access returns on S&P500 companies and matching those with company filing reports, yielding the final plot

## Report

Cuilin goes here, set up your own section name

Yuchen goes here, set up your own section name

### Return calculation, data match, and plot generation

#### Data
I download the S&P500 daily return data from WRDS:

<img width="279" alt="Screen Shot 2022-09-27 at 01 07 06" src="https://user-images.githubusercontent.com/50337211/192436760-71bc234e-c3c5-490e-b0f8-0b4cf02f0b32.png">

I download the individual stock return data using `yfinance`

<img width="183" alt="Screen Shot 2022-09-27 at 01 12 10" src="https://user-images.githubusercontent.com/50337211/192437555-05e1179d-b7cd-4b7e-bb1a-1fc4d2ff7b08.png">

#### Calculation
For each filing date, I calculate the close price return between 3 days later and the day before the filing date. For the market return, I just sum the daily returns. Then, access return across the 4 days = stock return - market return. A typical access return distribution is:

![image](https://user-images.githubusercontent.com/50337211/192438238-fa1a1d4e-54b5-40cf-b7e4-734e7e95a65b.png)

After the access returns are obtained, I find those with the filing date and split them in terms of score quantiles.

#### Plots
Then I can plot the median return within each quintile, based on whether the score is unweighted or tf.idf weighted.

Here is our final plot:

![image](https://user-images.githubusercontent.com/50337211/192438295-c07d5080-9345-4854-b5d0-6d651faa563f.png)

![image](https://user-images.githubusercontent.com/50337211/192438323-3149714b-cfa5-46d8-811f-153e92de09b4.png)

### Conclusion

There is a slight difference between using proportional weights and tf.idf weights. The H4N dictionary does not perform well, as expected. However, we are not able to reproduce a decreasing line for the FinNeg dictionary. In addition, if we use more quantiles, the plot does not show a clear pattern:

![image](https://user-images.githubusercontent.com/50337211/192439231-f2baa78f-5926-4a22-8a55-13b83f8b0f09.png)

We went through our code and did not find errors that could be related to this problem.

Our guess is that we need more subtle handling of filing filtration and parsing. For example, we cannot include all filings which would otherwise lead to artifacts in returns (small price and big returns); we need to be more careful while parsing and matching the words in the text file. In additional to removing stop words, we may want to remove some other meaningless words to get a more accurate estimation of negative proportions.

Overall, we got a hands-on experience of dealing with real-world data. We didn't manage to reproduce the perfect plot as stated in the paper. Apologies!
