---
layout: post
title:  "Benefits of Bayesian A/B test analysis"
date:   2022-08-26 13:06:13 +0100
categories: analytics 
---

## What is an A/B test?
You have an idea to improve your website to push your conversion rates higher.  The improved site's been built and it's 
ready to go.  But, how do you know that the improvement is really an improvement?  A surprising amount of "improvements"
end up having the opposite effect.  The principled approach to answering this question is to run a split test, and 
gather some experimental data before making the decision.  Using the collected data, you'd want to know if your 
new site was an improvement, some measure of whether the improvement is sufficiently large to justify the 
changes, and a level of certainty, or probability that you might be wrong.  

## A Bayesian split-test calculator
Stated exactly, you want to know the probability that website B (the new alternative) is at least $$x\%$$ better than 
website A (the old version).  For $$x=0$$, you'll get the probability that B is better.  

A Bayesian approach allows us to answer this question.  

The following [calculator][split-test-calculator] takes care of the calculations:

[![calculator](/JC/calculator.JPG){: width="65%" }][split-test-calculator]

The calculator allows you to enter the number of visitors and positive outcomes for each site, as well as a desired 
out-performance 
margin $$x$$.  If you'd like to incorporate the value of a positive outcome, for example if the pricing is different on 
the two sites, you can select to include the conversion value in the calculations.  Once the data's been entered, 
hit `Update`, and *viola*, you have your answer.  The plot displays the probability density functions over the conversion
rates (or values), showing the uncertainty of the estimates, and the overlap between the two.

The calculator assumes a uniform prior, which means we're assuming that all rates are equally likely before any data 
is observed.  The relative importance of the prior diminishes as more data is collected, and its effect is washed out.

## Frequentist *vs* Bayesian 
In practice, this approach to split-test analysis is less common than the Frequentist approach.  The two approaches each 
have their merits, but I'd argue that the Bayesian approach is often a superior choice for business decision makers.

# Intuitive interpretation 
The Bayesian formulation of the result: "the probability that B is at least $$x%$$ better than A is $$y$$", is fairly 
intuitive, and hardly requires further explanation.  But this statement is nonsensical within the Frequentist framework. 

In the Frequentist view, there exists a true conversion rate for each site.  Those rates are precise real numbers.  It
makes no sense to talk about the probability that the conversion rate of B is better than that of A.  It either is, or 
it isn't.  We can construct confidence intervals, where we can talk about the probability of the interval containing the 
true rate, but to the uninitiated that sounds like unnecessary mental gymnastics. 

The Bayesian says, sure, the rates may be exact real numbers, but since we don't know what they are, we can talk about 
probabilities as degrees of belief.  For example, say I have to guess my friend's height.  In my mind, I'd compare his 
height to the heights of others that I know more precisely.  I might say, he's taller than me and I'm $$1.7$$ meters tall, 
but he's shorter than Bobby who's $$1.8$$ meters tall.  So I'd say the probability that he's shorter than $$1.7$$ is $$0$$, and the 
probability that he's shorter than $$1.8$$ is $$100\%$$, and if I have no further information (I don't know if he's closer in 
height to either me or Bobby), I say the probability that he's shorter than $$1.75$$ meters is $$50\%$$.  Once I observe my friend 
standing next to Alice, who I know is $$1.75$$ meters tall, and Bobby, I'd update my estimate to something be more precise.  
All of this seems quite natural, especially compared to the Frequentist formulation.

# Flexibility and monitoring 
The Frequentist approach requires setting a sample size in advance, using an expected effect size, and desired levels 
of statistical significance and power.  The interpretation of the results is valid only if the full sample size is 
collected, and continuous monitoring is more likely to be harmful than helpful.  In contrast, the Bayesian approach 
is built on the notion that our beliefs update as we observe data.  At any point during the course of the test, the 
Bayesian formulation provides an answer to the most intuitive formulation of our original question.  

# Paramter choices 
The choice of significance and power in Frequentist tests are usually set at $$5\%$$ and $$80\%$$ without much further thought, 
corresponding to a $$5\%$$ chance of encountering a false positive, and a $$20\%$$ chance of a false negative.  These arbitrary 
choices stem from accepted norms in scientific publishing.  In academic research, the "cost" of a false positive is high. 
Incorrectly claiming that a new relationship has been discovered in an academic journal has high reputational risk for 
the journal and the authors (in an industry where reputation is everything).  Furthermore, the decision to publish is 
not reversible.  But business is very different from academic publishing.  Its much more like greedy optimisation, where
its often better to select the best alternative given available information.  

To illustrate the point, say you run a split-test using the Frequentist formulation.  After concluding the test, you 
don't find a significant improvement.  If you'd used academia's favourite parameters, this would mean that there's a 
more than $$5\%$$ chance that the 
new site is no better than the old.  You do a Bayesian analysis too, and find that there's a $$70\%$$ probability that the 
new site is better.  Due to other constraints you cannot continue running the test (e.g. another team has now launched a
test and continuing this one will interfere with theirs).  What should you do?  Clearly there are many other 
considerations that could influence our answer, but given that the changes have been made and the cost of switching is 
therefore close to $$0$$, the most rational action would often be to switch to B.  The Frequentist following academic norms
wouldn't have advised this.
 
The Bayesian is faced with the choice of prior, which is the most criticized aspect of this approach.  But, it's 
impossible to do inference without making assumptions.  Setting a prior forces decision makers to be explicit about 
theirs.  As more data is collected, the impact of the prior is washed out, and it's fairly straightforward to conduct a 
sensitivity analysis over different priors.

If you'd like like to point out any errors, please get in touch via email, and if you've found this useful, please 
consider sharing.  Thanks for reading!

[bokeh]: https://docs.bokeh.org/en/latest/
[split-test-calculator]: https://bayesian-test-calculator.herokuapp.com/calculator_app
[mlm-power-analysis-python]: https://machinelearningmastery.com/statistical-power-and-power-analysis-in-python/