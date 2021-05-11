---
layout: post
title: Crystallization Regression
subtitle: Regression Analysis on Crystallization Experimental Data 
gh-repo: MichelleChung-code/MultipleOutputRegressions
tags: [Regression, Analysis, Chemical Engineering]
---
Github Repository: [MultipleOutputRegressions](https://github.com/MichelleChung-code/MultipleOutputRegressions)

Skills Used: [Python](https://www.python.org/){:target="_blank"}

## Project Objective

This project involved running a regression analysis on experimental data obtained from a crystallization lab. This was completed as part of the ENCH 551 course.  The experiment cooled an aqueous solution of supersaturated potassium chloride (KCl) to induce crystal formation. Data from nine experiments was collected to investigate the effects of agitation rate and seed crystal mass (independent variables) on crystal yield, growth rate, and mean diameter (dependent variables). The objective of the regression analysis was to determine the optimal experimental conditions that would maximize these attributes.

## Experimental Results

Experimental results obtained and used to run the regression analysis are tabulated below:

| Agitator Speed (rpm) | Seed Crystal Mass (g) | Yield (g) | Growth Rate (m/s) | Mean Diameter (g) |
| :------------------: |:--------------------: | :-------: | :---------------: | :---------------: |
| 214 | 0 | 170.5448 | 6.7462E-08 | 218.577 |
| 214	| 1	| 231.2165 | 7.22231E-08	| 225.336 | 
| 214	| 2	| 171.36	| 5.82614E-08	| 178.28 | 
| 464	| 0	| 183.25	| 8.27043E-08	| 248.94 |
| 464	| 1	| 123.44	| 6.9377E-08	| 208.131 |
| 464	| 2	| 204.51	| 4.21397E-08	| 208.423 |
| 665	| 0	| 254.69	| 7.60032E-08	| 237.13 |
| 665	| 1	| 203.9458	| 8.31225E-08	| 257.264 |
| 665	| 2	| 164.6471	| 6.98147E-08	| 259.7106667 |

## Approach

Three regression models were considered and run: linear regression considering interactions between independent variables, linear regression considering interactions between dependent variables, and a non-linear random forest regression.  The coefficient of determination (R<sup>2</sup>) was used to evaluate the fit of the models.  

In the models, three independent variables (yield, growth rate, and mean diameter) and two dependent variables were considered.

The multiple linear regression considering interactions between independent variables follows:
\\[ y_i=\beta_(i0)+ \beta_(i1) x_1+\beta_(i2) x_2+\beta_(i3) x_1 x_2 \\]

Where, 
- \\[ i \\] is the dependent variable number of the given dependent variable. 
- \\[ y_i \\] is the dependent variable 
- \\[ x_1 \\]  and \\[ x_2 \\] are the independent variables, agitation rate (rpm) and seed crystal mass (g), respectively.  
- \\[ β_(i0) \\]  is the constant term
- \\[ β_(i1) \\], \\[ β_(i2) \\], and \\[ β_(i3) \\] are the coefficients associated with each independent variable, with \\[ β_(i3) \\] being associated with the interaction term.

It can also be centered!

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .mx-auto.d-block :}

Here's a code chunk:

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
