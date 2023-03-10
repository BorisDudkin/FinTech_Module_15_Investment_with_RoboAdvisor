# Algorithmic Trading and Machine Learning Models.

### Algorithmic Trading powered by Machine Learning models enable investors to automatically trade assets in the highly dynamic and volatile environments. Machine learning systems can evaluate multiple factors that influence prices of financial instruments and efficiently generate accurate trading decisions.<br/> Algorithmic Trading and Machine Learning Models application takes you through the implementing and evaluating process of the Machine Learning driven Algorithmic Trading strategies.

---

![ecommerce](Images/robo.jpg)

---

## Table of contents

1. [Technologies](#technologies)
2. [Installation Guide](#installation-guide)
3. [Usage](#usage)
4. [Contributors](#contributors)
5. [License](#license)

---

## Technologies

`Python 3.9`

`Jupyter lab`

_Prerequisites_

1. `Pandas` is a Python package that provides fast, flexible, and expressive data structures designed to make working with large sets of data easy and intuitive.

   - [pandas](https://github.com/pandas-dev/pandas) - for the documentation, installation guide and dependencies.

1. `Matplotlib` is a comprehensive library for creating static, animated, and interactive visualizations in Python.

   - [matplotlib ](https://matplotlib.org/) - For guidance on how to start visualization, interactive visualization, styles and layouts customazation.

1. `Scikit-learn` is a simple and efficient tools for predictive data analysis. It is built on NumPy, SciPy, and matplotlib.

   - [scikit-learn ](https://scikit-learn.org/stable/) - for information on the library, its features and installation instructions.<br/>

---

## Installation Guide

Jupyter lab is a preferred software to work with Risk Return Analysis application.<br/> Jupyter lab is a part of the **[anaconda](https://www.anaconda.com/)** distribution package and therefore it is recommended to download **anaconda** first.<br/> Once dowloaded, run the following command in your terminal to lauch Jupyter lab:

```python
jupyter lab
```

Before using the application first install the following dependencies by using your terminal:

To install pandas run:

```python
#  PuPi
pip install pandas
```

```python
# or conda
conda install pandas
```

To install matplotlib run:

```python
#  PuPi
pip install matplotlib
```

```python
# or conda
conda install -c conda-forge matplotlib
```

To install scikit library, in Terminal run:

```python
# PuPi
pip install -U scikit-learn
```

---

## Usage

> Application summary<br/>

Algorithmic Trading and Machine Learning Models application consists of the following building blocks:<br/>

- Establishing a Baseline Performance
- Tuning the Baseline Trading Algorithm
- Evaluating a New Machine Learning Classifier

**Establish a Baseline Performance:**<br/>

1. Features and Target identification:<br/>

- Features:<br/>
  We identify the trading indicators that will serve as _features_ within our models:

  - Those trading indicators will be long and short simple moving avareages (SMV). For the base model the long window will be set to 100 days and thw hsort window - to 4 days.

- Target:<br/>
  The following trading signals will be used as a _target_ within the nachine learning models we will create later in the application:<br/>

  - When Actual Returns are greater than or equal to 0, generate signal to buy stock long
  - When Actual Returns are less than 0, generate signal to sell stock short<br/>
    Based on those signals and the actual returns, the strategy returns are calculated and displayed below together with the actual returns (the startegy returns are calculated by multiplyig the actual returns and the shifted trading signals: actual returns \* trading signals.shift()).
    The comparison of the actual and strategy returns are presented below:

  ![actual_strategy](Images/Original.JPG)<br/>

  As can be see from the chart, the actual returns outperform the startegy returns, which should be expected as our strategy assumes buy high and sell low (buy when the actual return is positive and sell, when negative).

2. Training and Testing datasets:<br/>

- The training dataset for the baseline model will be set to the first three months period of our data and the testing dataset will be the remaining period.
- We then apply the scaler model to fit the X-train data transform the X_train and X_test DataFrames using the scaler.

3. Model choice:<br/>

- We use the SVC classifier model from SKLearn's support vector machine (SVM) learning method to fit the scaled training data and make predictions based on the scaled testing data.

4.  Model evaluation<br/>

- We can review the classification report associated with the SVC model prediction:<br/>
  ![cl1](Images/svm_classification_report.JPG)<br/>
  The evaluation shows the model accuracy of 0.55. The most notable characteristic is the recall, showing 0.96 for 1.0 and 0.04 for -1.0. That indicates that model is more likely to generate the buy rather than sell signals. Also, since we calculate the strategy returns by multiplying
  actual returns and shifted predicted signals, it is of no surprise that the model's strategy returns are quite close to the actual returns, as it s more likely to produce 1.0 than -1.0:<br/>
  ![actual_strategy1](Images/SVC1.JPG)<br/>

**Tuning the Baseline Trading Algorithm**<br/>

- Tuning bu adjusting the trainign and testing window:

  - We first tune the baseline trading algorithm by adjusting the training and testing features: we change the length of the training data period from 3 months to 2 years (providing mode data for the model to learn). We then apply model-fit-predict steps to the new training and testing sets keeping the rest of the parameters unchanged.<br/>
  - The results are evaluated:<br/>

    ![cl2](Images/svm_classification_report2.JPG)<br/>

  - Although we managed to incease accuracy from 0.55 to 0.56, the recall indicator became even more biased towards 1.0 signal. As a result, the predicted strategy returns became more aligned with the actual returns:<br/>
    ![actual_strategy2](Images/SVC2.JPG)<br/>

- Tuning by adjusting the short and long windows of the Simple Moving Averages features (the length of the training and testing data are re-set back to the base case (3 month training data)):

  - We first set the short window to 5 days and the long window to 50 days vs the original 4 /100. We then apply model-fit-predict steps to the new training and testing sets keeping the rest of the parameters and the model unchanged.<br/>
  - The results are evaluated:<br/>
    ![cl3](Images/svm_classification_report3.JPG)<br/>
  - The accuracy of this model dropped to 0.54, however, the recall characteristic became more balanced, although still performing badly for -1.0 signal (0.18). Consequently, the predicted strategy returns are still aligned with the actual returns, although to a lesser extent:<br/>
    ![actual_strategy3](Images/SVC3.JPG)<br/>

  **Decision Tree Classifier model:**<br/>

  - We finally evaluate our algorithmic trading by applying a different classifier - Decision Tree model, to the original base features and target:<br/>
    ![cl4](Images/tree_classification_report.JPG)<br/>
  - The accuracy is inferior to the one produced by the SVM. Interestingly, this model generates much higher recall of 0.88 for -1.0 sell signal (SVM was more biased towards the buy signla of 1.0). As a consequence, the startegy returns are quite opposite and are mirroring the actual returns: <br/>
    ![actual_strategy4](Images/Tree.JPG)<br/>

**Summary and Conclusion**:<br/>
When selecting two different models and tuning some of the parameters we have not managed to achieve superior accuracy (with the maximum of 0.56 accuracy, we are just slightly better than the coin toos). Also, most of the attempts resulted in either one of the predicted signals perform very poorely on the re-call evaluation chriteria, which makes our model not as reliable as we would like it to be. We come to the same conclusion when comparing all the predicted strategy returns to the original strategy we generated.<br/>
Based on those finding it would be advisable to:

- get a larger dataset and train the model on a longer period of data;
- intoduce more trading indicators as features to our model;
- test more classifier models (logistic regression, KNN, Random Forest, Neural Networks).

> Getting started<br/>

- To use Portoflio Optimizer first clone the repository to your PC.<br/>
- Open `Jupyter lab` as per the instructions in the [Installation Guide](#installation-guide) to run the application.<br/>

---

## Contributors

Contact Details:

Boris Dudkin:

- [Email](boris.dudkin@gmail.com)
- [LinkedIn](www.linkedin.com/in/Boris-Dudkin)

---

## License

MIT

---
