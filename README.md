# Analyze A/B Test Results
This project investigates mock datasets from Udacity on an e-commerce company's A/B test results. This company had developed a new web page to increase the number of users who decide on paying for the company's product. The analytical methods which leverage concepts from a span of topics including probability, hypothesis testing and regression are used in this project to understand the A/B test results and provide the company with insights into whether the company should implement the new page, keep the current page, or perform additional tests before making a final decision.

## Requirements
* Software
  * conda 4.6.3 or similar versions
  * python 3.7.2 (or python 3)
  * Packages
    - pandas
    - numpy
    - random
    - matplotlib.pyplot
    - statsmodels.stats.proportion
    - statsmodels.api
* Raw Data
  - All `.csv` files of the raw data were provided in the Data Analyst Nanodegree program at Udacity. Because the results of this project cannot be reproduced and verified without these data, the `.csv` files are provided in the remote repository.
  - The name of each file and the name of the python object which correspond to each data are provided below.
  - A/B Test Results
      * _ab\_data.csv_ (`df`)
      * tabulates which page the user accessed and whether the user paid
  - Country
      * _countries.csv_ (`countries_df`)
      * tabulates the country where each user lives

## Organization of the Investigation
1. Introduction
  * provides a motivation for the e-commerce company's A/B test and the analysis of the results from this A/B test.
2. Part I - Probability
  * identifies several general properties of the `ab_data.csv` file.
  * builds on these general properties to define and execute the operations for cleaning the raw data.
  * computes and discusses descriptive statistics for
      - the conversion rate for all users.
      - the conversion rate for the users from only the treatment group.
      - the conversion rate for the users from only the control group.
3. Part II - A/B Test
  * defines null and alternative hypotheses regarding the difference in the conversion rates of both groups.
  * performs sampling distribution of differences in conversion rates based on the null hypothesis.
  * performs two-sample Z-test.
  * compares results from both approaches including the p-values.
4. Part III - Regression
  * performs a logistic regression to predict whether a user converts based on the page the user is seeing.
  * updates the regression with another predictor variable, the country where the user lives.
  * updates the regression with interaction terms between the two predictor variables.
5. Conclusions
  * re-iterates the statistics obtained from each section of the analysis.
  * summarizes the statistical and practical implications of these statistics.

## Version Update from v1.0 to v2.0
1. Code Performance
    * Problem
        - Simulation of binomial outcomes over 10,000 iterations with a **for-loop** takes considerable amount of time.
    * Resolution
        - **for-loop** was removed.
        - The built-in Numpy method, `numpy.random.binomial()`, which was originally used in the **for-loop** was improved to perform silumations over 10,000 iterations.
            * **n**: changed from 1 (outcomes 0 or 1) to objects `n_new` and `n_old`, the sample sizes for the two groups, one with the new page and the other with the old page.
            * **size**: changed from objects `n_new` and `n_old` to the number of iterations, 10,000.
        - Total number of successes from each iteration was divided by the sample size to compute the proportion of successes from each iteration.
2. Two-tail and One-tail Test Results
    * p-value obtained from the logistic regression (two-tail test) was used to reproduce the p-value obtained from sampling estimated values from the null (one-tail test).
    * Consistency in observations was mentioned after the conversion of p-values and re-visited in __Conclusions__
3. Calculation and Terminology
    * In section 2 of __Part II__, the difference in the convert rates from the single simulation was corrected from 0.13% to 0.02%.
    * An instance of the term _linear_ in _linear regression_ was changed to _logistic_. This project does not cover _linear_ regression.

## Author
Jong Min (Jay) Lee [jmlee5629@gmail.com]

## Acknowledgement
* This project was completed as one of the mandatory requirements for the Data Analyst Nanodegree at Udacity.
* Online resources including discussions in [Stack Overflow](https://stackoverflow.com/) and technical documentations for packages and methods were referenced throughout the data wrangling and analysis processes.
* Online documentation from `statsmodels` for `stats.proportion.proportions_ztest()` [link](https://www.statsmodels.org/dev/generated/statsmodels.stats.proportion.proportions_ztest.html) was referenced during two-sample Z-test from __Part II__.
* First improvement from v1.0 was motivated by the discussion in [Stack Overflow](https://softwareengineering.stackexchange.com/questions/254475/how-do-i-move-away-from-the-for-loop-school-of-thought).
* Comparison of the results from two-tail and one-tail tests was motivated by a [documentation](https://stats.idre.ucla.edu/other/mult-pkg/faq/pvalue-htm/) available online.
