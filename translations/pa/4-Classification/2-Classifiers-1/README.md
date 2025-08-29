<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9579f42e3ff5114c58379cc9e186a828",
  "translation_date": "2025-08-29T17:50:54+00:00",
  "source_file": "4-Classification/2-Classifiers-1/README.md",
  "language_code": "pa"
}
-->
# ਖਾਣੇ ਦੇ ਵਰਗ 1

ਇਸ ਪਾਠ ਵਿੱਚ, ਤੁਸੀਂ ਪਿਛਲੇ ਪਾਠ ਵਿੱਚ ਸੇਵ ਕੀਤੇ ਡਾਟਾਸੈਟ ਨੂੰ ਵਰਤੋਂਗੇ, ਜੋ ਖਾਣੇ ਬਾਰੇ ਸੰਤੁਲਿਤ ਅਤੇ ਸਾਫ ਡਾਟਾ ਨਾਲ ਭਰਿਆ ਹੋਇਆ ਹੈ।

ਤੁਸੀਂ ਇਸ ਡਾਟਾਸੈਟ ਨੂੰ ਵੱਖ-ਵੱਖ ਵਰਗਬੱਧ ਕਰਨ ਵਾਲੇ ਤਰੀਕਿਆਂ ਨਾਲ ਵਰਤੋਂਗੇ ਤਾਂ ਜੋ _ਸਮੂਹ ਦੇ ਸਮੱਗਰੀ ਦੇ ਆਧਾਰ 'ਤੇ ਦਿੱਤੇ ਗਏ ਰਾਸ਼ਟਰੀ ਖਾਣੇ ਦੀ ਪੇਸ਼ਗੂਈ ਕੀਤੀ ਜਾ ਸਕੇ_। ਇਸ ਦੌਰਾਨ, ਤੁਸੀਂ ਇਹ ਵੀ ਸਿੱਖੋਗੇ ਕਿ ਕਿਵੇਂ ਅਲਗੋਰਿਥਮ ਵਰਗਬੱਧ ਕਰਨ ਵਾਲੇ ਕੰਮਾਂ ਲਈ ਵਰਤੇ ਜਾ ਸਕਦੇ ਹਨ।

## [ਪਾਠ ਤੋਂ ਪਹਿਲਾਂ ਕਵੀਜ਼](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/21/)
# ਤਿਆਰੀ

ਜੇਕਰ ਤੁਸੀਂ [ਪਾਠ 1](../1-Introduction/README.md) ਪੂਰਾ ਕੀਤਾ ਹੈ, ਤਾਂ ਯਕੀਨੀ ਬਣਾਓ ਕਿ _cleaned_cuisines.csv_ ਫਾਈਲ `/data` ਫੋਲਡਰ ਦੇ ਮੁੱਖ ਸਥਾਨ ਵਿੱਚ ਮੌਜੂਦ ਹੈ, ਜੋ ਕਿ ਇਹਨਾਂ ਚਾਰ ਪਾਠਾਂ ਲਈ ਹੈ।

## ਅਭਿਆਸ - ਰਾਸ਼ਟਰੀ ਖਾਣੇ ਦੀ ਪੇਸ਼ਗੂਈ ਕਰੋ

1. ਇਸ ਪਾਠ ਦੇ _notebook.ipynb_ ਫੋਲਡਰ ਵਿੱਚ ਕੰਮ ਕਰਦੇ ਹੋਏ, ਉਸ ਫਾਈਲ ਨੂੰ Pandas ਲਾਇਬ੍ਰੇਰੀ ਦੇ ਨਾਲ ਇੰਪੋਰਟ ਕਰੋ:

    ```python
    import pandas as pd
    cuisines_df = pd.read_csv("../data/cleaned_cuisines.csv")
    cuisines_df.head()
    ```

    ਡਾਟਾ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦਾ ਹੈ:

|     | Unnamed: 0 | cuisine | almond | angelica | anise | anise_seed | apple | apple_brandy | apricot | armagnac | ... | whiskey | white_bread | white_wine | whole_grain_wheat_flour | wine | wood | yam | yeast | yogurt | zucchini |
| --- | ---------- | ------- | ------ | -------- | ----- | ---------- | ----- | ------------ | ------- | -------- | --- | ------- | ----------- | ---------- | ----------------------- | ---- | ---- | --- | ----- | ------ | -------- |
| 0   | 0          | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
| 1   | 1          | indian  | 1      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
| 2   | 2          | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
| 3   | 3          | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
| 4   | 4          | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 1      | 0        |
  

1. ਹੁਣ, ਕੁਝ ਹੋਰ ਲਾਇਬ੍ਰੇਰੀਆਂ ਇੰਪੋਰਟ ਕਰੋ:

    ```python
    from sklearn.linear_model import LogisticRegression
    from sklearn.model_selection import train_test_split, cross_val_score
    from sklearn.metrics import accuracy_score,precision_score,confusion_matrix,classification_report, precision_recall_curve
    from sklearn.svm import SVC
    import numpy as np
    ```

1. X ਅਤੇ y ਕੋਆਰਡੀਨੇਟ ਨੂੰ ਦੋ ਡਾਟਾਫ੍ਰੇਮ ਵਿੱਚ ਵੰਡੋ। `cuisine` ਲੇਬਲ ਡਾਟਾਫ੍ਰੇਮ ਹੋ ਸਕਦਾ ਹੈ:

    ```python
    cuisines_label_df = cuisines_df['cuisine']
    cuisines_label_df.head()
    ```

    ਇਹ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦੇਵੇਗਾ:

    ```output
    0    indian
    1    indian
    2    indian
    3    indian
    4    indian
    Name: cuisine, dtype: object
    ```

1. `Unnamed: 0` ਕਾਲਮ ਅਤੇ `cuisine` ਕਾਲਮ ਨੂੰ `drop()` ਕਾਲ ਕਰਕੇ ਹਟਾਓ। ਬਾਕੀ ਡਾਟਾ ਨੂੰ ਟ੍ਰੇਨਿੰਗ ਫੀਚਰ ਵਜੋਂ ਸੇਵ ਕਰੋ:

    ```python
    cuisines_feature_df = cuisines_df.drop(['Unnamed: 0', 'cuisine'], axis=1)
    cuisines_feature_df.head()
    ```

    ਤੁਹਾਡੇ ਫੀਚਰ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦੇ ਹਨ:

|      | almond | angelica | anise | anise_seed | apple | apple_brandy | apricot | armagnac | artemisia | artichoke |  ... | whiskey | white_bread | white_wine | whole_grain_wheat_flour | wine | wood |  yam | yeast | yogurt | zucchini |
| ---: | -----: | -------: | ----: | ---------: | ----: | -----------: | ------: | -------: | --------: | --------: | ---: | ------: | ----------: | ---------: | ----------------------: | ---: | ---: | ---: | ----: | -----: | -------: |
|    0 |      0 |        0 |     0 |          0 |     0 |            0 |       0 |        0 |         0 |         0 |  ... |       0 |           0 |          0 |                       0 |    0 |    0 |    0 |     0 |      0 |        0 | 0 |
|    1 |      1 |        0 |     0 |          0 |     0 |            0 |       0 |        0 |         0 |         0 |  ... |       0 |           0 |          0 |                       0 |    0 |    0 |    0 |     0 |      0 |        0 | 0 |
|    2 |      0 |        0 |     0 |          0 |     0 |            0 |       0 |        0 |         0 |         0 |  ... |       0 |           0 |          0 |                       0 |    0 |    0 |    0 |     0 |      0 |        0 | 0 |
|    3 |      0 |        0 |     0 |          0 |     0 |            0 |       0 |        0 |         0 |         0 |  ... |       0 |           0 |          0 |                       0 |    0 |    0 |    0 |     0 |      0 |        0 | 0 |
|    4 |      0 |        0 |     0 |          0 |     0 |            0 |       0 |        0 |         0 |         0 |  ... |       0 |           0 |          0 |                       0 |    0 |    0 |    0 |     0 |      1 |        0 | 0 |

ਹੁਣ ਤੁਸੀਂ ਆਪਣੇ ਮਾਡਲ ਨੂੰ ਟ੍ਰੇਨ ਕਰਨ ਲਈ ਤਿਆਰ ਹੋ!

## ਆਪਣੇ ਵਰਗਬੱਧ ਕਰਨ ਵਾਲੇ ਤਰੀਕੇ ਦੀ ਚੋਣ

ਹੁਣ ਜਦੋਂ ਤੁਹਾਡਾ ਡਾਟਾ ਸਾਫ ਅਤੇ ਟ੍ਰੇਨਿੰਗ ਲਈ ਤਿਆਰ ਹੈ, ਤੁਹਾਨੂੰ ਇਹ ਫੈਸਲਾ ਕਰਨਾ ਪਵੇਗਾ ਕਿ ਇਸ ਕੰਮ ਲਈ ਕਿਹੜਾ ਅਲਗੋਰਿਥਮ ਵਰਤਣਾ ਹੈ।

Scikit-learn ਵਰਗਬੱਧ ਕਰਨ ਨੂੰ Supervised Learning ਦੇ ਅਧੀਨ ਰੱਖਦਾ ਹੈ, ਅਤੇ ਇਸ ਸ਼੍ਰੇਣੀ ਵਿੱਚ ਤੁਹਾਨੂੰ ਵਰਗਬੱਧ ਕਰਨ ਦੇ ਕਈ ਤਰੀਕੇ ਮਿਲਣਗੇ। [ਵੱਖ-ਵੱਖ ਤਰੀਕੇ](https://scikit-learn.org/stable/supervised_learning.html) ਪਹਿਲਾਂ ਦ੍ਰਿਸ਼ਟੀ ਵਿੱਚ ਕਾਫ਼ੀ ਹੈਰਾਨ ਕਰਨ ਵਾਲੇ ਲੱਗਦੇ ਹਨ। ਹੇਠਾਂ ਦਿੱਤੇ ਤਰੀਕੇ ਸਾਰੇ ਵਰਗਬੱਧ ਕਰਨ ਦੇ ਤਕਨੀਕੀ ਤਰੀਕੇ ਸ਼ਾਮਲ ਕਰਦੇ ਹਨ:

- ਲੀਨੀਅਰ ਮਾਡਲ
- Support Vector Machines
- Stochastic Gradient Descent
- Nearest Neighbors
- Gaussian Processes
- Decision Trees
- Ensemble methods (voting Classifier)
- Multiclass ਅਤੇ multioutput algorithms (multiclass ਅਤੇ multilabel classification, multiclass-multioutput classification)

> ਤੁਸੀਂ [neural networks ਨੂੰ ਵਰਗਬੱਧ ਕਰਨ ਲਈ](https://scikit-learn.org/stable/modules/neural_networks_supervised.html#classification) ਵੀ ਵਰਤ ਸਕਦੇ ਹੋ, ਪਰ ਇਹ ਪਾਠ ਦੇ ਦਾਇਰੇ ਤੋਂ ਬਾਹਰ ਹੈ।

### ਕਿਹੜਾ ਵਰਗਬੱਧ ਕਰਨ ਵਾਲਾ ਤਰੀਕਾ ਚੁਣਨਾ ਹੈ?

ਤਾਂ, ਤੁਹਾਨੂੰ ਕਿਹੜਾ ਵਰਗਬੱਧ ਕਰਨ ਵਾਲਾ ਤਰੀਕਾ ਚੁਣਨਾ ਚਾਹੀਦਾ ਹੈ? ਅਕਸਰ, ਕਈ ਤਰੀਕਿਆਂ ਨੂੰ ਅਜ਼ਮਾਉਣਾ ਅਤੇ ਚੰਗੇ ਨਤੀਜੇ ਦੀ ਭਾਲ ਕਰਨਾ ਇੱਕ ਤਰੀਕਾ ਹੁੰਦਾ ਹੈ। Scikit-learn ਇੱਕ [ਸਾਈਡ-ਬਾਈ-ਸਾਈਡ ਤੁਲਨਾ](https://scikit-learn.org/stable/auto_examples/classification/plot_classifier_comparison.html) ਪੇਸ਼ ਕਰਦਾ ਹੈ, ਜੋ KNeighbors, SVC ਦੋ ਤਰੀਕੇ, GaussianProcessClassifier, DecisionTreeClassifier, RandomForestClassifier, MLPClassifier, AdaBoostClassifier, GaussianNB ਅਤੇ QuadraticDiscrinationAnalysis ਦੀ ਤੁਲਨਾ ਦਿਖਾਉਂਦਾ ਹੈ:

![ਵਰਗਬੱਧ ਕਰਨ ਵਾਲਿਆਂ ਦੀ ਤੁਲਨਾ](../../../../translated_images/comparison.edfab56193a85e7fdecbeaa1b1f8c99e94adbf7178bed0de902090cf93d6734f.pa.png)
> Plots Scikit-learn ਦੇ ਦਸਤਾਵੇਜ਼ਾਂ 'ਤੇ ਬਣਾਏ ਗਏ

> AutoML ਇਸ ਸਮੱਸਿਆ ਨੂੰ ਬਹੁਤ ਹੀ ਸੌਖੇ ਤਰੀਕੇ ਨਾਲ ਹੱਲ ਕਰਦਾ ਹੈ, ਇਹ ਤੁਲਨਾਵਾਂ ਕਲਾਉਡ ਵਿੱਚ ਚਲਾਉਂਦਾ ਹੈ, ਅਤੇ ਤੁਹਾਨੂੰ ਆਪਣੇ ਡਾਟਾ ਲਈ ਸਭ ਤੋਂ ਵਧੀਆ ਅਲਗੋਰਿਥਮ ਚੁਣਨ ਦੀ ਆਗਿਆ ਦਿੰਦਾ ਹੈ। ਇਸਨੂੰ [ਇੱਥੇ ਅਜ਼ਮਾਓ](https://docs.microsoft.com/learn/modules/automate-model-selection-with-azure-automl/?WT.mc_id=academic-77952-leestott)

### ਇੱਕ ਵਧੀਆ ਤਰੀਕਾ

ਅੰਧੇਵਾਹੀ ਅਨੁਮਾਨ ਲਗਾਉਣ ਦੇ ਬਦਲੇ, ਇੱਕ ਵਧੀਆ ਤਰੀਕਾ ਇਹ ਹੈ ਕਿ ਇਸ ਡਾਊਨਲੋਡ ਕਰਨ ਯੋਗ [ML Cheat sheet](https://docs.microsoft.com/azure/machine-learning/algorithm-cheat-sheet?WT.mc_id=academic-77952-leestott) ਦੇ ਵਿਚਾਰਾਂ ਦੀ ਪਾਲਣਾ ਕਰੋ। ਇੱਥੇ, ਅਸੀਂ ਪਤਾ ਲਗਾਉਂਦੇ ਹਾਂ ਕਿ ਸਾਡੇ multiclass ਸਮੱਸਿਆ ਲਈ, ਸਾਡੇ ਕੋਲ ਕੁਝ ਚੋਣਾਂ ਹਨ:

![multiclass ਸਮੱਸਿਆਵਾਂ ਲਈ cheatsheet](../../../../translated_images/cheatsheet.07a475ea444d22234cb8907a3826df5bdd1953efec94bd18e4496f36ff60624a.pa.png)
> Microsoft's Algorithm Cheat Sheet ਦਾ ਇੱਕ ਹਿੱਸਾ, ਜੋ multiclass ਵਰਗਬੱਧ ਕਰਨ ਦੇ ਵਿਕਲਪਾਂ ਨੂੰ ਵੇਖਾਉਂਦਾ ਹੈ

✅ ਇਸ cheat sheet ਨੂੰ ਡਾਊਨਲੋਡ ਕਰੋ, ਪ੍ਰਿੰਟ ਕਰੋ, ਅਤੇ ਇਸਨੂੰ ਆਪਣੀ ਕੰਮ ਕਰਨ ਵਾਲੀ ਜਗ੍ਹਾ 'ਤੇ ਲਟਕਾਓ!

### ਤਰਕ

ਆਓ ਵੇਖੀਏ ਕਿ ਕੀ ਅਸੀਂ ਆਪਣੇ ਪਾਬੰਦੀਆਂ ਦੇ ਆਧਾਰ 'ਤੇ ਵੱਖ-ਵੱਖ ਤਰੀਕਿਆਂ ਨੂੰ ਸਮਝ ਸਕਦੇ ਹਾਂ:

- **Neural networks ਬਹੁਤ ਭਾਰੀ ਹਨ**। ਸਾਡੇ ਸਾਫ, ਪਰ ਘੱਟ ਡਾਟਾਸੈਟ ਨੂੰ ਦੇਖਦੇ ਹੋਏ, ਅਤੇ ਇਹ ਹਕੀਕਤ ਕਿ ਅਸੀਂ ਟ੍ਰੇਨਿੰਗ ਨੂੰ notebooks ਦੇ ਜ਼ਰੀਏ ਸਥਾਨਕ ਤੌਰ 'ਤੇ ਚਲਾ ਰਹੇ ਹਾਂ, neural networks ਇਸ ਕੰਮ ਲਈ ਬਹੁਤ ਭਾਰੀ ਹਨ।
- **ਕੋਈ ਦੋ-ਵਰਗ ਵਰਗਬੱਧ ਕਰਨ ਵਾਲਾ ਤਰੀਕਾ ਨਹੀਂ**। ਅਸੀਂ ਦੋ-ਵਰਗ ਵਰਗਬੱਧ ਕਰਨ ਵਾਲਾ ਤਰੀਕਾ ਨਹੀਂ ਵਰਤਦੇ, ਇਸ ਲਈ ਇਹ one-vs-all ਨੂੰ ਰੱਦ ਕਰਦਾ ਹੈ।
- **Decision tree ਜਾਂ logistic regression ਕੰਮ ਕਰ ਸਕਦੇ ਹਨ**। ਇੱਕ decision tree ਕੰਮ ਕਰ ਸਕਦਾ ਹੈ, ਜਾਂ multiclass ਡਾਟਾ ਲਈ logistic regression।
- **Multiclass Boosted Decision Trees ਵੱਖਰੀ ਸਮੱਸਿਆ ਹੱਲ ਕਰਦੇ ਹਨ**। Multiclass Boosted Decision Trees ਜ਼ਿਆਦਾਤਰ nonparametric ਕੰਮਾਂ ਲਈ ਉਚਿਤ ਹਨ, ਜਿਵੇਂ ਕਿ ਰੈਂਕਿੰਗ ਬਣਾਉਣ ਵਾਲੇ ਕੰਮ, ਇਸ ਲਈ ਇਹ ਸਾਡੇ ਲਈ ਲਾਭਕਾਰੀ ਨਹੀਂ ਹੈ।

### Scikit-learn ਦੀ ਵਰਤੋਂ

ਅਸੀਂ Scikit-learn ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਆਪਣੇ ਡਾਟਾ ਦਾ ਵਿਸ਼ਲੇਸ਼ਣ ਕਰਾਂਗੇ। ਹਾਲਾਂਕਿ, Scikit-learn ਵਿੱਚ logistic regression ਦੀ ਵਰਤੋਂ ਕਰਨ ਦੇ ਕਈ ਤਰੀਕੇ ਹਨ। [ਪਾਸ ਕਰਨ ਲਈ ਪੈਰਾਮੀਟਰਾਂ](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html?highlight=logistic%20regressio#sklearn.linear_model.LogisticRegression) 'ਤੇ ਇੱਕ ਨਜ਼ਰ ਮਾਰੋ।

ਅਸਲ ਵਿੱਚ, ਦੋ ਮਹੱਤਵਪੂਰਨ ਪੈਰਾਮੀਟਰ ਹਨ - `multi_class` ਅਤੇ `solver` - ਜੋ ਸਾਨੂੰ ਨਿਰਧਾਰਤ ਕਰਨ ਦੀ ਲੋੜ ਹੈ, ਜਦੋਂ ਅਸੀਂ Scikit-learn ਨੂੰ logistic regression ਕਰਨ ਲਈ ਕਹਿੰਦੇ ਹਾਂ। `multi_class` ਦਾ ਮੁੱਲ ਇੱਕ ਨਿਰਧਾਰਤ ਵਿਹਾਰ ਲਾਗੂ ਕਰਦਾ ਹੈ। solver ਦਾ ਮੁੱਲ ਇਹ ਹੈ ਕਿ ਕਿਹੜਾ algorithm ਵਰਤਣਾ ਹੈ। ਸਾਰੇ solvers ਨੂੰ ਸਾਰੇ `multi_class` ਮੁੱਲਾਂ ਨਾਲ ਜੋੜਿਆ ਨਹੀਂ ਜਾ ਸਕਦਾ।

ਦਸਤਾਵੇਜ਼ਾਂ ਦੇ ਅਨੁਸਾਰ, multiclass ਕੇਸ ਵਿੱਚ, ਟ੍ਰੇਨਿੰਗ algorithm:

- **Uses the one-vs-rest (OvR) scheme**, ਜੇ `multi_class` ਵਿਕਲਪ `ovr` 'ਤੇ ਸੈਟ ਕੀਤਾ ਗਿਆ ਹੈ
- **Uses the cross-entropy loss**, ਜੇ `multi_class` ਵਿਕਲਪ `multinomial` 'ਤੇ ਸੈਟ ਕੀਤਾ ਗਿਆ ਹੈ। (ਵਰਤਮਾਨ ਵਿੱਚ `multinomial` ਵਿਕਲਪ ਸਿਰਫ ‘lbfgs’, ‘sag’, ‘saga’ ਅਤੇ ‘newton-cg’ solvers ਦੁਆਰਾ ਸਮਰਥਿਤ ਹੈ।)

> 🎓 'scheme' ਇੱਥੇ 'ovr' (one-vs-rest) ਜਾਂ 'multinomial' ਹੋ ਸਕਦਾ ਹੈ। ਕਿਉਂਕਿ logistic regression ਅਸਲ ਵਿੱਚ binary classification ਨੂੰ ਸਮਰਥਨ ਕਰਨ ਲਈ ਡਿਜ਼ਾਈਨ ਕੀਤਾ ਗਿਆ ਹੈ, ਇਹ schemes ਇਸਨੂੰ multiclass classification ਕੰਮਾਂ ਨੂੰ ਬਿਹਤਰ ਢੰਗ ਨਾਲ ਹੱਲ ਕਰਨ ਵਿੱਚ ਮਦਦ ਕਰਦੇ ਹਨ। [source](https://machinelearningmastery.com/one-vs-rest-and-one-vs-one-for-multi-class-classification/)

> 🎓 'solver' ਨੂੰ "optimization ਸਮੱਸਿਆ ਵਿੱਚ ਵਰਤਣ ਲਈ algorithm" ਵਜੋਂ ਪਰਿਭਾਸ਼ਿਤ ਕੀਤਾ ਗਿਆ ਹੈ। [source](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html?highlight=logistic%20regressio#sklearn.linear_model.LogisticRegression).

Scikit-learn ਇਹ ਟੇਬਲ ਪੇਸ਼ ਕਰਦਾ ਹੈ ਜੋ ਵੱਖ-ਵੱਖ data structures ਦੁਆਰਾ ਪੇਸ਼ ਕੀਤੀਆਂ ਚੁਣੌਤੀਆਂ ਨੂੰ ਹੱਲ ਕਰਨ ਦੇ ਤਰੀਕਿਆਂ ਨੂੰ ਸਮਝਾਉਂਦਾ ਹੈ:

![solvers](../../../../translated_images/solvers.5fc648618529e627dfac29b917b3ccabda4b45ee8ed41b0acb1ce1441e8d1ef1.pa.png)

## ਅਭਿਆਸ - ਡਾਟਾ ਨੂੰ ਵੰਡੋ

ਅਸੀਂ ਆਪਣੀ ਪਹਿਲੀ ਟ੍ਰੇਨਿੰਗ ਟ੍ਰਾਇਲ ਲਈ logistic regression 'ਤੇ ਧਿਆਨ ਦੇ ਸਕਦੇ ਹਾਂ ਕਿਉਂਕਿ ਤੁਸੀਂ ਪਿਛਲੇ ਪਾਠ ਵਿੱਚ ਇਸ ਬਾਰੇ ਸਿੱਖਿਆ ਹੈ।
ਆਪਣੇ ਡਾਟਾ ਨੂੰ `train_test_split()` ਕਾਲ ਕਰਕੇ ਟ੍ਰੇਨਿੰਗ ਅਤੇ ਟੈਸਟਿੰਗ ਸਮੂਹਾਂ ਵਿੱਚ ਵੰਡੋ:

```python
X_train, X_test, y_train, y_test = train_test_split(cuisines_feature_df, cuisines_label_df, test_size=0.3)
```

## ਅਭਿਆਸ - logistic regression ਲਾਗੂ ਕਰੋ

ਕਿਉਂਕਿ ਤੁਸੀਂ multiclass ਕੇਸ ਦੀ ਵਰਤੋਂ ਕਰ ਰਹੇ ਹੋ, ਤੁਹਾਨੂੰ ਇਹ ਚੁਣਨ ਦੀ ਲੋੜ ਹੈ ਕਿ ਕਿਹੜਾ _scheme_ ਵਰਤਣਾ ਹੈ ਅਤੇ ਕਿਹੜਾ _solver_ ਸੈਟ ਕਰਨਾ ਹੈ। LogisticRegression ਦੀ ਵਰਤੋਂ ਕਰੋ ਜਿਸ ਵਿੱਚ multi_class `ovr` 'ਤੇ ਸੈਟ ਹੈ ਅਤੇ solver `liblinear` 'ਤੇ ਸੈਟ ਹੈ।

1. multi_class ਨੂੰ `ovr` 'ਤੇ ਸੈਟ ਕਰਕੇ ਅਤੇ solver ਨੂੰ `liblinear` 'ਤੇ ਸੈਟ ਕਰਕੇ ਇੱਕ logistic regression ਬਣਾਓ:

    ```python
    lr = LogisticRegression(multi_class='ovr',solver='liblinear')
    model = lr.fit(X_train, np.ravel(y_train))
    
    accuracy = model.score(X_test, y_test)
    print ("Accuracy is {}".format(accuracy))
    ```

    ✅ `lbfgs` ਵਰਗੇ ਇੱਕ ਵੱਖਰੇ solver ਨੂੰ ਅਜ਼ਮਾਓ, ਜੋ ਅਕਸਰ default ਵਜੋਂ ਸੈਟ ਕੀਤਾ ਜਾਂਦਾ ਹੈ
ਨੋਟ: ਜਦੋਂ ਲੋੜ ਹੋਵੇ, ਆਪਣੇ ਡਾਟਾ ਨੂੰ ਸਮਤਲ ਕਰਨ ਲਈ Pandas [`ravel`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.ravel.html) ਫੰਕਸ਼ਨ ਦੀ ਵਰਤੋਂ ਕਰੋ।
ਸਹੀਤਾ ਦੀ ਸ਼ੁੱਧਤਾ **80% ਤੋਂ ਵੱਧ** ਹੈ!

1. ਤੁਸੀਂ ਇਸ ਮਾਡਲ ਨੂੰ ਇੱਕ ਡਾਟਾ ਦੀ ਇੱਕ ਕਤਾਰ (#50) ਦੀ ਜਾਂਚ ਕਰਕੇ ਕਿਰਿਆਸ਼ੀਲਤਾ ਵਿੱਚ ਦੇਖ ਸਕਦੇ ਹੋ:

    ```python
    print(f'ingredients: {X_test.iloc[50][X_test.iloc[50]!=0].keys()}')
    print(f'cuisine: {y_test.iloc[50]}')
    ```

    ਨਤੀਜਾ ਪ੍ਰਿੰਟ ਕੀਤਾ ਗਿਆ ਹੈ:

   ```output
   ingredients: Index(['cilantro', 'onion', 'pea', 'potato', 'tomato', 'vegetable_oil'], dtype='object')
   cuisine: indian
   ```

   ✅ ਇੱਕ ਵੱਖਰਾ ਕਤਾਰ ਨੰਬਰ ਅਜ਼ਮਾਓ ਅਤੇ ਨਤੀਜੇ ਚੈੱਕ ਕਰੋ

1. ਹੋਰ ਗਹਿਰਾਈ ਨਾਲ ਜਾਂਚ ਕਰਨ ਲਈ, ਤੁਸੀਂ ਇਸ ਅਨੁਮਾਨ ਦੀ ਸ਼ੁੱਧਤਾ ਦੀ ਜਾਂਚ ਕਰ ਸਕਦੇ ਹੋ:

    ```python
    test= X_test.iloc[50].values.reshape(-1, 1).T
    proba = model.predict_proba(test)
    classes = model.classes_
    resultdf = pd.DataFrame(data=proba, columns=classes)
    
    topPrediction = resultdf.T.sort_values(by=[0], ascending = [False])
    topPrediction.head()
    ```

    ਨਤੀਜਾ ਪ੍ਰਿੰਟ ਕੀਤੀ ਗਈ ਹੈ - ਭਾਰਤੀ ਖਾਣਾ ਇਸ ਦਾ ਸਭ ਤੋਂ ਵਧੀਆ ਅਨੁਮਾਨ ਹੈ, ਚੰਗੀ ਸੰਭਾਵਨਾ ਨਾਲ:

    |          |        0 |
    | -------: | -------: |
    |   indian | 0.715851 |
    |  chinese | 0.229475 |
    | japanese | 0.029763 |
    |   korean | 0.017277 |
    |     thai | 0.007634 |

    ✅ ਕੀ ਤੁਸੀਂ ਸਮਝਾ ਸਕਦੇ ਹੋ ਕਿ ਮਾਡਲ ਨੂੰ ਇਹ ਭਾਰਤੀ ਖਾਣਾ ਕਿਉਂ ਲੱਗਦਾ ਹੈ?

1. ਹੋਰ ਵਿਸਥਾਰ ਪ੍ਰਾਪਤ ਕਰਨ ਲਈ, ਜਿਵੇਂ ਤੁਸੀਂ ਰਿਗ੍ਰੈਸ਼ਨ ਪਾਠਾਂ ਵਿੱਚ ਕੀਤਾ ਸੀ, ਇੱਕ ਵਰਗੀਕਰਨ ਰਿਪੋਰਟ ਪ੍ਰਿੰਟ ਕਰੋ:

    ```python
    y_pred = model.predict(X_test)
    print(classification_report(y_test,y_pred))
    ```

    |              | precision | recall | f1-score | support |
    | ------------ | --------- | ------ | -------- | ------- |
    | chinese      | 0.73      | 0.71   | 0.72     | 229     |
    | indian       | 0.91      | 0.93   | 0.92     | 254     |
    | japanese     | 0.70      | 0.75   | 0.72     | 220     |
    | korean       | 0.86      | 0.76   | 0.81     | 242     |
    | thai         | 0.79      | 0.85   | 0.82     | 254     |
    | accuracy     | 0.80      | 1199   |          |         |
    | macro avg    | 0.80      | 0.80   | 0.80     | 1199    |
    | weighted avg | 0.80      | 0.80   | 0.80     | 1199    |

## 🚀ਚੁਣੌਤੀ

ਇਸ ਪਾਠ ਵਿੱਚ, ਤੁਸੀਂ ਆਪਣੇ ਸਾਫ ਕੀਤੇ ਡਾਟਾ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਇੱਕ ਮਸ਼ੀਨ ਲਰਨਿੰਗ ਮਾਡਲ ਬਣਾਇਆ ਜੋ ਸਮੱਗਰੀਆਂ ਦੀ ਇੱਕ ਲੜੀ ਦੇ ਆਧਾਰ 'ਤੇ ਰਾਸ਼ਟਰੀ ਖਾਣੇ ਦੀ ਪੇਸ਼ਗੋਈ ਕਰ ਸਕਦਾ ਹੈ। ਸਮੇਂ ਕੱਢੋ ਅਤੇ ਸਕਾਈਟ-ਲਰਨ ਦੁਆਰਾ ਡਾਟਾ ਵਰਗਬੱਧ ਕਰਨ ਲਈ ਦਿੱਤੇ ਗਏ ਕਈ ਵਿਕਲਪਾਂ ਨੂੰ ਪੜ੍ਹੋ। 'solver' ਦੇ ਸੰਕਲਪ ਵਿੱਚ ਹੋਰ ਡੂੰਘਾਈ ਨਾਲ ਜਾਓ ਤਾਂ ਜੋ ਸਮਝ ਸਕੋ ਕਿ ਪਿੱਛੇ ਕੀ ਚਲ ਰਿਹਾ ਹੈ।

## [ਪਾਠ-ਬਾਅਦ ਪ੍ਰਸ਼ਨੋਤਰੀ](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/22/)

## ਸਮੀਖਿਆ ਅਤੇ ਖੁਦ ਅਧਿਐਨ

ਲੌਜਿਸਟਿਕ ਰਿਗ੍ਰੈਸ਼ਨ ਦੇ ਗਣਿਤ ਵਿੱਚ ਹੋਰ ਡੂੰਘਾਈ ਨਾਲ ਜਾਓ ਇਸ [ਪਾਠ](https://people.eecs.berkeley.edu/~russell/classes/cs194/f11/lectures/CS194%20Fall%202011%20Lecture%2006.pdf) ਵਿੱਚ।
## ਅਸਾਈਨਮੈਂਟ 

[ਸੋਲਵਰਜ਼ ਦਾ ਅਧਿਐਨ ਕਰੋ](assignment.md)

---

**ਅਸਵੀਕਾਰਨਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੀਤਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।