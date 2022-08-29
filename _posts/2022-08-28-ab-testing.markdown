---
layout: post
title:  "Benefits of Bayesian A/B test analysis"
date:   2022-08-26 13:06:13 +0100
categories: analytics 
---

You have an idea to improve your website to push your conversion rates higher.  The improved site's been built and its 
ready to go.  But, how do you know that the improvement is really an improvement?  A surprising amount of "improvements"
end up having the opposite effect.  The principled approach to answering this question is to run a split test, and 
gather some experimental data before making the decision.

## The Frequentist approach 

The usual approach to setting up and analysing a split-test is based on frequentist hypothesis testing, which is the 
most widely used (and misused) method of answering questions in scientific research papers.  Because of the prevalence 
of this approach in academic research, it's often adopted in business, without real consideration of whether it's really 
appropriate. 

With this approach, the starting assumption (called the null hypothesis) is that the new variant is not sufficiently 
better than the existing one.  Once data is collected, the probability of the data given this assumption is calculated 
(called the p-value).  If this probability is small, it's concluded that the starting assumption is probably false, and 
that the new variant is sufficiently better.

Four related quantities: effect size, significance level, statistical power, and sample size, need to be set in advance 
of running the test.  (Three are set, determining the fourth.)

The expected effect size is typically an educated guess based on the nature of the change, the conversion rates on the 
existing site, and the minimum required effect for the change to be commercially worthwhile.  

The significance level and statistical power determine the probabilities of the test leading to an incorrect conclusion.
This can happen in one of two ways:
- Type I error: False positive.  Incorrectly reject null hypothesis.  Switch to B when A is really better.  The significance level 
is the probability of making a Type I error. 
- Type II error: False negative.  Incorrectly fail to reject null hypothesis.  Stick to A, but B is really better. The statistical 
power is related to the probability of making a type II error.

The values that are typically used are borrowed from scientific research, and probably aren't very good choices 
for many business decisions.  The usual choices are a significance level of 5%, and a statistical power of 80%.  

In research, the "cost" of a false positive is high.  Incorrectly claiming that a new relationship has been discovered 
in an academic journal has high reputational risk for the journal and the authors (in an industry where reputation is 
everything).  Furthermore, the decision to publish is not reversible.

There's less risk related to false negatives.  The researchers just keep researching, so a 20% chance is deemed 
acceptable.  (Lower would mean you'd need to collect more data, higher means this will happen more often, and 20%
is often an seemingly reasonable middle ground.)

## Problems

This approach is not intuitively interpretable, and obstructs learning.  It's quite natural to ask, is my new site 
better?  And how sure am I, i.e. what's the probability that it's better?  But frequentist hypothesis testing estimates 
the probability of the data if the sites are not different.  That's difficult to naturally incorporate into our thinking.  

In fact, the intuitive statement "what's the probabilty that B is better than A" is nonsensical within the frequentist 
framework, since the "true conversion rates" are real numbers, and speaking about the probability of a real number is 
meaningless.  It's either 0.3742, or it isn't.  The probabilities are 100% or 0%.

The interpretation of the p-value, and the statistical power of a test, is only valid if the test is completed. 
Continuous monitoring is more likely to be detrimental than helpful.  But monitoring is usually essential in business 
settings, and priorities change (so early stopping may occur for other reasons).

Business is more like greedy optimisation than scientific research.  The risk related to a decision to switch to a new 
site is quite different (and probably much lower) than falsely reporting a new scientific discovery.  The decision is 
usually easily revertible, and often only relevant for a limited period of time as the business will continue to evolve
and the site will be updated again in the future. 

## The Bayesian approach 

By assigning probabilities to degrees of belief, we can sensibly talk about the probability that B is better than A, 
or x% better than A.  The intuitive formulation becomes mathematically possible. 

With the Bayesian approach, the starting point is a prior belief, that expresses "what are my beliefs about the
conversion rates, before seeing any data", and a method for updating those belies based on observed data.  

This use of priors is the main point of criticism of the Bayesian approach.  

Facilitates continual monitoring, learning, and trade-off decision making in business. 

[![calculator](/JC/calculator.JPG){: width="65%" }][split-test-calculator]

[bokeh]: https://docs.bokeh.org/en/latest/
[split-test-calculator]: https://bayesian-test-calculator.herokuapp.com/calculator_app
[mlm-power-analysis-python]: https://machinelearningmastery.com/statistical-power-and-power-analysis-in-python/