---
layout: post
usehighlight: false
tags: [machine-learning, artificial-intelligence]
title: The machine learning landscape
---
Machine learning is the science that learns what actions to take from data without explicitly programming the computer. In the words of the pioneer name of  the artificial intelligence:

> Machine learning is the field of study that gives computers the ability to learn without being explicitly programmed - Arthur Samuel, 1959

# 1. Types of Machine Learning Systems?
{: style="color: #e03c31!important;" }
We can classify machine learning systems into roughly 4 main categories, as outlined below, according to their learning styles and approaches:
1. [Supervised Learning](#11-supervised-learning)
2. [Unsupervised Learning](#12-unsupervised-learning)
3. [Semi-supervised Learning](#13-semi-supervised-learning)
4. [Reinforcement Learning](#14-reinforcement-learning)

## 1.1 Supervised Learning
{: style="color: #e03c31;" }
As its name suggests, supervised learning is based on supervision. Basically supervised learning technique involves traning the machine with the input and corresponding output. Subsequently, we ask the machine to predict the output using the test dataset.

Let's explain an example to make it more understandable. Imagine there are dogs and cats images. There are some differences between dogs and cats that we can use to classify them, such as shape&size of the eyes and ears, size of the tail, color, height. We train the machine with pictures where one shape of ears belongs to a dog, one shape of eyes belongs to a dog, and the dimensions resemble a dog. This is called labeling. After training, machine can classify a cat or a dog when we provide a image of either.

The main aim of the supervised learning technique is the map the input variable with output variable.
We can divide supervised learning into to two types of problems: classification and regression.

### 1.1.1 Classification
{: style="color: #e03c31;"}

Classification algorithms are solve classification problems, which is output variable is categorical such as "Yes or No", "Male or Female", "Spam or Ham", etc. The classification algoritms predict the categories present in the dataset. If we give an example: spam detection, email filtering.

Some popular classification algorithms are: 
- Random Forest Algorithm
- Decision Tree Algorithm
- Logistic Regression Algorithm
- Support Vector Machine Algorithm

### 1.1.2 Regression
{: style="color: #e03c31;"}

Regression algorithms are used to solve regression problems which there is a linear relationship between input and output variables. As known regression means model the relationship between a dependent variable (also called target or outcome) and one or more independent variables( also called predictors or features).

Some popular regression algorithms are: 
- Simple Linear Regression Algorithm
- Multivariate Regression Algorithm
- Decision Tree Algorithm
- Lasso Regression

### 1.1.3 Real-world Applications:
{: style="color: #e03c31;"}
- Image Segmentation
- Risk Assessment 
- Fraud Detection
- Spam Detection
- Speech Recognation

## 1.2 Unsupervised Learning
{: style="color: #e03c31;"}
Unlike supervised learning, in the unsupervised learning the traning data is unlabeled. The machine can predict output without any supervision. The models are trained with the data that is neither classified nor labelled, and the model acts on that data without supervision.

It seems a bit more confused. Let's give an example to undertand more preciously; suppose you have images that consist of dog and cats datasets, we input it to machine learning models.The images are totally unknown to the model, and the task of machine is to find the patterns and categories of the objects. So, now the machine will discover patterns, similarites and differences, such as colour difference, shape difference, and predict the output when it is tested with the test dataset.

The main aim of the unsupervised learning technique is to group or categories the unsorted dataset according to the similarities, patterns and differences. 
We can divide unsupervised learning into two categories; clustering, association

### 1.2.1 Clustering 
{: style="color: #e03c31;"}

The clustering technique involves grouping objects based on their similarities, forming one group with high similarity and having fewer or no similarities with objects in other groups.

If its need to explain with example; grouping the customers by their purchasing behaviors.
Some popular clustering algorithms are:
- K-means Clustering Algorithm
- Mean-shift Algorithm
- DBSCAN(Density-Based Spatial Clustering of Applications with Noise) Algorithm
- Princibal Component Analysis
- Independent Component Analysis

### 1.2.2 Association
{: style="color: #e03c31;"}

The association technique typically refers to identifying interesting relationships, patterns, or association among variables in a large dataset. The main goal of this learning algorithm to find dependency of one data item on another data item and map those variables accordingly so that it can generate maximum profit. As can understood from its purpose this learning technique is often used in market basket analysis, where the goal is discover association between items that are frequently purchased together. 
Some popular association algorithms are:
- Apriori
- FP growth (Frequent pattern growth)
- Eclat (Equivalence class transformation)

### 1.2.3 Real-world Applications:
{: style="color: #e03c31;"}
* **Recommendation Systems:** Unsupervised learning technique is used by recommendation systems such as, amazon purchase suggestion, netflix movie matches, etc.
* **Anomaly Detection:** This technique is used by anomaly detection system such as, detect bot activity in instagram or twitter.
* **Singular Value Decomposition:** SVD is a dimensionality reduction algorithm used for exploratory and interpreting purposes.For example making a consumer suggestion, such as which color t-shirt fit best with blue jeans, to extract certain types of information from the dataset(take out info on every user located in İstanbul, Ankara).

## 1.3 Semi-supervised Learning
{: style="color: #e03c31;"}
Semi-supervised learning technique combines both supervised(labelled) and unsupervised(unlabelled) techniques. In semi-supervised learning, the algorithm is trained on a dataset that contains both labeled and unlabeled examples. It is particularly useful in situations where obtaining labeled data is expensive or time-consuming.

Let's explain an example to make it clear.Imagine a photo gallery application on an Iphone. The iphone clusters photos based on their similarities. For example photos 1,5 and 11 in the gallery include member of your family and photos 2,3 and 8 include your best friend.The algorithm can clustered those photos seperatly and if you label them as family or bff(best friend for ever), the algorithm will cluster new photos according to this labeling.

## 1.4 Reinforcement Learning
{: style="color: #e03c31;"}

Reinforcement learning is a feedback-based learning technique. It is quite similar to the human learning technique, which involves learning from experience. A child learns various things through experiences in their day-to-day life. For example, if they touches fire, they will get hurt and be punished. In same way, ai agent gets rewarded for each correct action and is penalized for each incorrect action; hence the goal of reinforcement learning agent is to maximize the rewards.

Due to its learning technique, RL is employed different fields such as Game theory, Operation research, Information theory, multi-agent system, etc.

### 1.4.1 Real-world Applications
{: style="color: #e03c31;"}
- Video Games
- Robotics
- Text Mining
- Resource Management









