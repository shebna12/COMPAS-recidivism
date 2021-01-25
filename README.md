# COMPAS-recidivism
Auditing the predictions made by a machine learning model trained on historical data of  Correctional Offender Management Profiling for Alternative Sanctions (COMPAS) for bias and fairness. Definitions below are made simple and easy to grasp for the sake of understanding the application of fairness algorithms in this use case.
## AI Bias and Fairness Short  Primer
### What is bias?

Bias is the act of discriminating or favoring an individual or group based on their inherent characteristics. Since data used in training machine learning algorithms are made by humans, the bias that these humans have can influence the predictions a model makes.

### What is fairness?

Fairness is creating similar decisions regardless of what demoraphic and invidiual or group belongs to. 

### How can we identify bias?
In this implementation, I used the [Parity-fairness package](https://github.com/xmpuspus/parity-fairness) which serves as a toolkit containing multiple open source tools for bias checking(fairness metrics), bias mitigation, and model explainability. 

### In a nutshell, how does this work?
 1. Check dataset bias using the fairness metrics indicated in the Parity-fairness package.
 2. Train a machine learning model on the dataset.
 3. Check model bias using fairness metrics that require predictions.
 4. Mitigate the found biases. There are three kinds of bias mitigation techniques:
	 * Pre-processing algorithms : they are used before training the model
	 * In-processing algorithms : they are used during the training process of the model
	 * Post-processing algorithms : they are used after training the model
5. Find the best bias mitigation technique that suits your needs. There will be times that a certain bias mitigation algorithm can solve all of the biases found in all of the fairness metrics. However, there are also cases which it cannot. Thus, being able to understand which fairness metric is best suited for your problem matters. Check out the [AIF360](http://aif360.mybluemix.net/resources#guidance) guidelines on choosing the proper metric and mitigation algorithm. 

# Getting Started
The notebook provided in this repo already contains all of the necessary details on how the whole process was conducted. For compatibility, kindly use Google Colab to run the notebook.

# Goal
The goal of this project is to audit or check the COMPAS dataset for possible biases using the fairness metrics and mitigate these biases through the use of different bias mitigation algorithms. 

# Dataset
The dataset used for this is a cleaned and compressed version of the *ProPublica COMPAS* dataset which can be found at [Kaggle](https://www.kaggle.com/danofer/compass). A copy of the cleaned and compressed version is provided in this repository inside the `data` directory

## Target Demographic Attributes
The protected attributes investigated in this project are *sex*, *age category*, and *race*.
# Findings
Upon checking the three protected attributes for biases, it has been determined that there are *two biases* found on all protected attributes, namely *statistical parity difference* and *average absolute odds difference* metrics.  After applying the different bias mitigation techniques for the `race` attribute, the best performing algorithm is the Reweighing technique. It assigns weight combinations differently on each race group (Caucasian,African-American,Hispanic, etc) to ensure fairness before classification.

### Note:
The *age category* and *sex* attributes are left to the reader to further explore. 

Special thanks to the Parity-fairness developers, [Xavier](https://github.com/xmpuspus) and [Nam](https://github.com/namsvd), for the easy to follow Parity-fairness implementation notebook.
