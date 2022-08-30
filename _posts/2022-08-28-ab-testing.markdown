---
layout: post
title:  "Benefits of Bayesian A/B test analysis"
date:   2022-08-26 13:06:13 +0100
categories: analytics 
---

You have an idea to improve your website to push your conversion rates higher.  The improved site's been built and its 
ready to go.  But, how do you know that the improvement is really an improvement?  A surprising amount of "improvements"
end up having the opposite effect.  The principled approach to answering this question is to run a split test, and 
gather some experimental data before making the decision.  Once the data's been collected, you want to know if your 
new site was an improvement, you want some measure of whether the improvement is sufficiently large to justify the 
changes, and you want to know the level of certainty, or the probability that you might be wrong.  

Stated exactly, you want to know the probability that website B (the new alternative) is at least x% better than 
website A (the old version).  For x=0, you'll get the probability that B is better.  

A Bayesian approach allows us to answer this question.  

# A Bayesian split-test calculator

The following calculator takes care of the calculations:

[![calculator](/JC/calculator.JPG){: width="65%" }][split-test-calculator]

It allows you to enter the number of visitors and positive outcomes for each site, as well as a desired out-performance 
margin x.  If you'd like to incorporate the value of a positive outcome, for example if your pricing is different on 
the two sites, you can select to include the conversion value in the calculations.  Once the data's been entered, 
hit `Update`, and viola, you have your answer.

The calculator assumes a uniform prior, which means we're assuming that all rates are equally likely before any data 
is observed.  The relative importance of the prior diminishes as more data is collected, and it's effect is washed out. 

[bokeh]: https://docs.bokeh.org/en/latest/
[split-test-calculator]: https://bayesian-test-calculator.herokuapp.com/calculator_app
[mlm-power-analysis-python]: https://machinelearningmastery.com/statistical-power-and-power-analysis-in-python/