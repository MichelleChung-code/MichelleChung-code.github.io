---
layout: post
title: Crystallization Regression
subtitle: Regression Analysis on Crystallization Experimental Data 
gh-repo: MichelleChung-code/MultipleOutputRegressions
thumbnail-img: /assets/img/crystallization_setup.jpg
readtime: true
tags: [Regression, Analysis, Chemical Engineering]
---
Github Repository: [MultipleOutputRegressions](https://github.com/MichelleChung-code/MultipleOutputRegressions)

Skills Used: [Python](https://www.python.org/){:target="_blank"}

## Project Objective

This project involved running a regression analysis on experimental data obtained from a crystallization lab. This was completed as part of the ENCH 551 course.  The experiment cooled an aqueous solution of supersaturated potassium chloride (KCl) to induce crystal formation. Data from nine experiments was collected to investigate the effects of agitation rate and seed crystal mass (independent variables) on crystal yield, growth rate, and mean diameter (dependent variables). The objective of the regression analysis was to determine the optimal experimental conditions that would maximize these attributes.

## Experimental Results

Experimental results obtained and used to run the regression analysis are tabulated below:

| Agitator Speed \(rpm) | Seed Crystal Mass \(g) | Yield \(g) | Growth Rate \(m/s) | Mean Diameter \(μm) |
| :------------------: |:--------------------: | :-------: | :---------------: | :---------------: |
| 214 | 0 | 170.54 | 6.75E-08 | 218.58 |
| 214	| 1	| 231.22 | 7.22E-08	| 225.34 | 
| 214	| 2	| 171.36 | 5.83E-08	| 178.28 | 
| 464	| 0	| 183.25 | 8.27E-08	| 248.94 |
| 464	| 1	| 123.44 | 6.94E-08	| 208.13 |
| 464	| 2	| 204.51 | 4.21E-08	| 208.42 |
| 665	| 0	| 254.69 | 7.60E-08	| 237.13 |
| 665	| 1	| 203.95 | 8.31E-08	| 257.26 |
| 665	| 2	| 164.65 | 6.98E-08	| 259.71 |

## Approach Summary

Three regression models were considered and run: linear regression considering interactions between independent variables, linear regression considering interactions between dependent variables, and a non-linear random forest regression.  The coefficient of determination (R<sup>2</sup>) was used to evaluate the fit of the models.  

In the models, three independent variables (yield, growth rate, and mean diameter) and two dependent variables were considered.

The multiple linear regression considering interactions between independent variables follows:
\\[ y_i=\beta_{i0}+ \beta_{i1} x_1+\beta_{i2} x_2+\beta_{i3} x_1 x_2 \\]

Where, 
- $ i $ is the dependent variable number of the given dependent variable. 
- $ y_i $ is the dependent variable.
- $ x_1 $  and $ x_2 $ are the independent variables, agitation rate (rpm) and seed crystal mass (g), respectively.  
- $ β_{i0} $  is the constant term.
- $ β_{i1} $, $ β_{i2} $, and $ β_{i3} $ are the coefficients associated with each independent variable, with $ β_{i3} $ being associated with the interaction term.

The challenge with this first model is that the regression problem has been divided into a separate problem for each dependent variable to be predicted.  This assumes that the outputs are independent of each other.  The next linear model attempted to address this limitation.

The multiple linear regression considering interactions between dependent variables considers a linear sequence of models to produce outputs where the first model in the sequence uses independent variables only.  The second model then uses the independent variables, as well as, the output of the first model to make its prediction, and so on.

For the current three dependent and two independent variable case, the models are defined as:
\\[ y_1=\beta_{10}+ \beta_{11} x_1+\beta_{12} x_2 \\]
\\[ y_2=\beta_{20}+ \beta_{21} x_1+\beta_{22} x_2+\alpha_{21} y_1 \\]
\\[ y_3=\beta_{30}+ \beta_{31} x_1+\beta_{32} x_2+\alpha_{31} y_1+\alpha_{32} y_2 \\]

Where,
- $ i $ is the dependent variable number of the given dependent variable. 
- $ y_i $ is the dependent variable.
- $ x_1 $ and $ x_2 $ are the independent variables, agitation rate (rpm) and seed crystal mass (g), respectively.  
- $ \beta_{i0} $ is the constant term.
- $ \beta_{i1} $ and $ \beta_{i2} $ are the coefficients associated with each independent variable.
- $ \alpha_{ij} $ are the coefficients associated with the $ j $th dependent variable.

A non-linear approach was also taken.  This was a random forest regression model.   Random forest models consist of numerous decision tree models, using an ensemble approach.  Each individual decision tree makes a model prediction, the random forest then chooses the most common model prediction as the final value.  Default parameters from the sklearn ensemble RandomForestRegressor were used.

Based on resulting  R<sup>2</sup> values, the non-linear random forest regression model was determined to be the model that best fit the experimental data and was used to select optimal conditions.  The optimization problem dealt with finding the conditions that would produce the maximum crystal yield, growth rate, and mean diameter.  Using the bounds defined by the experiment, 214 rpm to 665 rpm and 0 g to 2 g seed crystal mass, input values were produced using step sizes of 5 rpm and 0.2 g within these ranges. The random forest model was then run to predict corresponding output values.  The maximum of which was chosen as the optimization solution.  

## Results

For the linear regression models: $ x_1 $ represents agitation rate, $ x_2 $ represents seed crystal mass, $ y_1 $ represents crystal yield, $ y_2 $ represents crystal growth rate, and $ y_3 $ represents the mean crystal diameter.  

The linear regression with interactions between independent variables, resulted in the following relationships:
\\[ y_1=144.05+ 0.13x_1+31.23x_2-0.10x_1 x_2 \\]
\\[ y_2=6.89×10^{-8}+ 2.11×10^{-11} x_1-9.64×10^{-9} x_2+6.97×10^{-13} x_1 x_2 \\]
\\[ y_3=223.59+ 0.03x_1-39.66x_2+0.07x_1 x_2 \\]

The linear regression with interactions between dependent variables, resulted in the following relationships:
\\[ y_1=186.61+ 0.03x_1-11.33x_2 \\]
\\[ y_2=7.47×10^{-8}+ 2.29×10^{-11} x_1-9.70×10^{-9} x_2-3.30×10^{-11} y_1 \\]
\\[ y_3=101.71+ 6.89×10^{-2} x_1+1.66x_2+8.06×10^{-2} y_1+1.12×10^9 y_2 \\]

Unlike linear methods, random forest regression models do not have a simple equation for expressing the relationship between the dependent and independent variables as the individual decision trees, contributing to the ensemble random forest follow a nodal tree structure.

Summarizing the R<sup>2</sup> scores for the three separate models:

| Model Type | R<sup>2</sup> for $ y_1 $ \(Yield) | R<sup>2</sup> for $ y_1 $ \(Growth Rate) | R<sup>2</sup> for $ y_1 $ \(Mean Diameter) | 
| :---: |:---: | :---: | :---: | 
| Linear with independent variable interactions | 0.242 | 0.519 | 0.751 | 
| Linear with dependent variable interactions	| 0.090	| 0.519 | 0.592	| 
| Random forest	| 0.730	| 0.906	| 0.905	| 

Due to the higher R<sup>2</sup> scores observed for the random forest regression model, this model was chosen to solve the optimization problem.  

Optimization results for the random forest model:

| Case | Agitation Rate \(rpm) | Seed Crystal Mass \(g) | Maximum Value | 
| :---: |:---: | :---: | :---: | 
| Yield | 565 rpm | 0 g |  238.89 g  | 
| Growth Rate	| 565 rpm	| 0.6 g | 8.05E-8 m/s	| 
| Mean Diameter	| 565 rpm | 1.2 g	| 253.97 μm	| 

The final optimal seed crystal mass at 565 rpm agitation rate was found graphically. 

<p align="center">
<img style="width:80%;" src="../assets/img/565rpm_optimization_seed_crystal_mass.png">
</p>

## Results Summary

Of the three attempted regression models, the non-linear method proved to better fit the experimental data (based on R<sup>2</sup> scores) and was chosen to determine optimal conditions.  The optimal conditions found using the non-linear random forest regression model were an agitation rate of 565 rpm with 0.5643 g of seed crystals. 


