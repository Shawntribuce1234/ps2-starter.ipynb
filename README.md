# Survey Bias and Statistical Inference: When More Data Doesn't Mean Better Results

## Objective

In this lab, I explored how selection bias can make survey results misleading even when we have a large sample size. I used simulated satisfaction data to compare the true population average with survey responses and tested whether statistical methods could correct the difference.

## Methodology

- Simulated 50,000 users before and after a product redesign, using engagement, support tickets, and satisfaction scores.
- Created a response mechanism where happier users were more likely to answer the survey.
- Calculated survey response rates and compared observed satisfaction with the true population mean.
- Used bootstrap resampling to calculate percentile and BCa confidence intervals for the mean and median.
- Ran a coverage simulation across 200 surveys to check whether confidence intervals captured the true population mean.
- Performed a Welch's t-test and calculated Cohen's d to measure the observed difference in satisfaction.
- Used power analysis to determine the sample size needed to detect a 0.10-point improvement.
- Applied inverse-probability weighting using logistic regression to see whether adjusting for engagement and support tickets could reduce selection bias.

## Key Findings

### Selection Bias

The observed satisfaction score increased from 3.60 to 4.30 after the redesign, suggesting an improvement of about 0.70 points. However, the true improvement was designed to be approximately 0.10 points.

Response rates also dropped from 27.54% to 15.19%, meaning fewer users responded after the redesign and those who did were more likely to be satisfied.

### Bootstrap Confidence Intervals

The handwritten and SciPy percentile confidence intervals were very similar, both around [4.29, 4.32].

The median percentile interval was [4, 4], while the BCa method returned NaN because the median had too little variation across samples.

Both percentile and BCa intervals had 0% coverage across 200 repeated surveys, showing that confidence intervals can still miss the truth when the underlying sample is biased.

### Hypothesis Testing

The two-sample t-test showed a statistically significant difference in satisfaction, with a mean difference of 0.7041 and Cohen's d of 0.8637.

However, statistical significance didn't mean the redesign actually caused such a large improvement because happier users were more likely to respond.

### Power Analysis

The power analysis showed that 972 responses per group were needed to detect a true improvement of 0.10 points with 80% power.

At the available sample size, the smallest detectable difference was 0.0315 points.

Increasing the simulated population from 5,000 to 200,000 users did not eliminate the bias, which stayed around 0.61 points.

### Inverse-Probability Weighting

I used logistic regression to estimate response probabilities based on engagement and support tickets, then gave more weight to users who were less likely to respond.

The observed post-redesign satisfaction mean was 4.3041, while the weighted mean decreased to 4.1432.

However, the true population mean was 3.3860, leaving a bias of 0.7572. The weighted estimate's 95% confidence interval was [4.1236, 4.1653], which still did not contain the true mean.

This showed that weighting couldn't fully correct the problem because satisfaction itself influenced who responded.

## Conclusion

This lab helped me understand that having more data doesn't always mean having better results. Even though the survey showed a statistically significant improvement, most of that difference came from selection bias rather than actual changes in satisfaction.

My biggest takeaway is that statistical methods like bootstrapping, hypothesis testing, and weighting can help us understand uncertainty, but they cannot automatically fix problems with how data is collected. Before trusting the results, we need to understand who is represented in the sample and who is missing.
