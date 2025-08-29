<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "72b5bae0879baddf6aafc82bb07b8776",
  "translation_date": "2025-08-29T16:43:33+00:00",
  "source_file": "2-Regression/4-Logistic/README.md",
  "language_code": "ne"
}
-->
# वर्गहरू भविष्यवाणी गर्नका लागि Logistic Regression

![Logistic vs. linear regression infographic](../../../../translated_images/linear-vs-logistic.ba180bf95e7ee66721ba10ebf2dac2666acbd64a88b003c83928712433a13c7d.ne.png)

## [पाठ अघि क्विज](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/15/)

> ### [यो पाठ R मा उपलब्ध छ!](../../../../2-Regression/4-Logistic/solution/R/lesson_4.html)

## परिचय

Regression को अन्तिम पाठमा, जो एक आधारभूत _क्लासिक_ ML प्रविधि हो, हामी Logistic Regression को अध्ययन गर्नेछौं। यो प्रविधि प्रयोग गरेर तपाईंले binary वर्गहरू भविष्यवाणी गर्नका लागि ढाँचाहरू पत्ता लगाउन सक्नुहुन्छ। यो क्यान्डी चकलेट हो कि होइन? यो रोग संक्रामक हो कि होइन? यो ग्राहकले यो उत्पादन रोज्नेछ कि छैन?

यस पाठमा, तपाईंले सिक्नुहुनेछ:

- डेटा visualization को लागि नयाँ पुस्तकालय
- Logistic Regression को प्रविधिहरू

✅ यस प्रकारको regression मा काम गर्ने आफ्नो समझलाई गहिरो बनाउनुहोस् यस [Learn module](https://docs.microsoft.com/learn/modules/train-evaluate-classification-models?WT.mc_id=academic-77952-leestott) मा।

## पूर्व-आवश्यकता

Pumpkin डेटा संग काम गरेपछि, हामी यसमा पर्याप्त परिचित छौं कि एउटा binary वर्ग छ जसमा हामी काम गर्न सक्छौं: `Color`।

आउनुहोस्, Logistic Regression मोडेल निर्माण गरौं जसले केही चरहरू दिएर _कुन रंगको pumpkin सम्भावित छ_ (orange 🎃 वा white 👻) भविष्यवाणी गर्न सक्छ।

> किन हामी regression को पाठ समूहमा binary classification को कुरा गर्दैछौं? केवल भाषिक सुविधा को लागि, किनकि Logistic Regression [वास्तवमा एक classification विधि हो](https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression), यद्यपि यो linear आधारित छ। डेटा वर्गीकरणका अन्य तरिकाहरूको बारेमा अर्को पाठ समूहमा जान्नुहोस्।

## प्रश्न परिभाषित गर्नुहोस्

हाम्रो उद्देश्यका लागि, हामी यसलाई binary रूपमा व्यक्त गर्नेछौं: 'White' वा 'Not White'। हाम्रो dataset मा 'striped' नामक अर्को वर्ग पनि छ तर यसको उदाहरणहरू कम छन्, त्यसैले हामी यसलाई प्रयोग गर्नेछैनौं। यो dataset बाट null मानहरू हटाएपछि हराउँछ।

> 🎃 रमाइलो तथ्य, हामी कहिलेकाहीं सेतो pumpkins लाई 'ghost' pumpkins भन्छौं। तिनीहरू carving गर्न धेरै सजिलो छैनन्, त्यसैले तिनीहरू orange भन्दा कम लोकप्रिय छन् तर तिनीहरू आकर्षक देखिन्छन्! त्यसैले हामी हाम्रो प्रश्नलाई यसरी पनि पुनःव्यक्त गर्न सक्छौं: 'Ghost' वा 'Not Ghost'। 👻

## Logistic Regression को बारेमा

Logistic Regression linear regression भन्दा केही महत्त्वपूर्ण तरिकामा फरक छ, जुन तपाईंले पहिले सिक्नुभएको थियो।

[![ML for beginners - Understanding Logistic Regression for Machine Learning Classification](https://img.youtube.com/vi/KpeCT6nEpBY/0.jpg)](https://youtu.be/KpeCT6nEpBY "ML for beginners - Understanding Logistic Regression for Machine Learning Classification")

> 🎥 माथिको छवि क्लिक गरेर Logistic Regression को छोटो भिडियो अवलोकन हेर्नुहोस्।

### Binary Classification

Logistic Regression ले linear regression जस्तै सुविधाहरू प्रदान गर्दैन। पूर्वले binary वर्ग ("white or not white") को बारेमा भविष्यवाणी प्रदान गर्दछ जबकि पछिल्लोले निरन्तर मानहरू भविष्यवाणी गर्न सक्षम छ, उदाहरणका लागि pumpkin को उत्पत्ति र harvesting को समय दिएर, _कसरी यसको मूल्य बढ्नेछ_।

![Pumpkin classification Model](../../../../translated_images/pumpkin-classifier.562771f104ad5436b87d1c67bca02a42a17841133556559325c0a0e348e5b774.ne.png)
> Infographic by [Dasani Madipalli](https://twitter.com/dasani_decoded)

### अन्य वर्गीकरणहरू

Logistic Regression का अन्य प्रकारहरू पनि छन्, जस्तै multinomial र ordinal:

- **Multinomial**, जसमा एकभन्दा बढी वर्गहरू हुन्छन् - "Orange, White, and Striped"।
- **Ordinal**, जसमा ordered वर्गहरू हुन्छन्, उपयोगी यदि हामीले हाम्रो परिणामहरूलाई तार्किक रूपमा क्रमबद्ध गर्न चाह्यौं, जस्तै हाम्रो pumpkins जसलाई सीमित संख्याका आकारहरू (mini, sm, med, lg, xl, xxl) द्वारा क्रमबद्ध गरिएको छ।

![Multinomial vs ordinal regression](../../../../translated_images/multinomial-vs-ordinal.36701b4850e37d86c9dd49f7bef93a2f94dbdb8fe03443eb68f0542f97f28f29.ne.png)

### चरहरू अनिवार्य रूपमा सम्बन्धित हुनु पर्दैन

Linear regression सम्बन्धित चरहरूसँग राम्रोसँग काम गर्थ्यो भन्ने कुरा सम्झनुहोस्? Logistic Regression विपरीत छ - चरहरू अनिवार्य रूपमा सम्बन्धित हुनु पर्दैन। यो डेटा संग काम गर्दछ जसको सम्बन्ध केही कमजोर छ।

### तपाईंलाई धेरै सफा डेटा चाहिन्छ

Logistic Regression ले धेरै डेटा प्रयोग गर्दा अधिक सटीक परिणाम दिन्छ; हाम्रो सानो dataset यस कार्यका लागि उपयुक्त छैन, त्यसैले यो ध्यानमा राख्नुहोस्।

[![ML for beginners - Data Analysis and Preparation for Logistic Regression](https://img.youtube.com/vi/B2X4H9vcXTs/0.jpg)](https://youtu.be/B2X4H9vcXTs "ML for beginners - Data Analysis and Preparation for Logistic Regression")

> 🎥 माथिको छवि क्लिक गरेर linear regression को लागि डेटा तयार गर्ने छोटो भिडियो अवलोकन हेर्नुहोस्।

✅ Logistic Regression को लागि उपयुक्त डेटा प्रकारहरूको बारेमा सोच्नुहोस्।

## अभ्यास - डेटा सफा गर्नुहोस्

पहिले, डेटा अलिकति सफा गर्नुहोस्, null मानहरू हटाएर र केही स्तम्भहरू चयन गरेर:

1. निम्न कोड थप्नुहोस्:

    ```python
  
    columns_to_select = ['City Name','Package','Variety', 'Origin','Item Size', 'Color']
    pumpkins = full_pumpkins.loc[:, columns_to_select]

    pumpkins.dropna(inplace=True)
    ```

    तपाईं आफ्नो नयाँ dataframe हेर्न सक्नुहुन्छ:

    ```python
    pumpkins.info
    ```

### Visualization - categorical plot

अब सम्म तपाईंले [starter notebook](./notebook.ipynb) मा pumpkin डेटा लोड गर्नुभएको छ र यसलाई सफा गर्नुभएको छ ताकि केही चरहरू सहितको dataset सुरक्षित रहोस्, जस्तै `Color`। आउनुहोस्, notebook मा नयाँ पुस्तकालय [Seaborn](https://seaborn.pydata.org/index.html) प्रयोग गरेर dataframe visualization गरौं, जुन पहिले प्रयोग गरिएको Matplotlib मा आधारित छ।

Seaborn ले तपाईंको डेटा visualization गर्न केही आकर्षक तरिकाहरू प्रदान गर्दछ। उदाहरणका लागि, तपाईं `Variety` र `Color` को डेटा वितरण तुलना गर्न सक्नुहुन्छ।

1. `catplot` function प्रयोग गरेर, हाम्रो pumpkin डेटा `pumpkins` प्रयोग गर्दै, र प्रत्येक pumpkin वर्गको लागि रंग mapping निर्दिष्ट गर्दै यस्तो plot बनाउनुहोस्:

    ```python
    import seaborn as sns
    
    palette = {
    'ORANGE': 'orange',
    'WHITE': 'wheat',
    }

    sns.catplot(
    data=pumpkins, y="Variety", hue="Color", kind="count",
    palette=palette, 
    )
    ```

    ![A grid of visualized data](../../../../translated_images/pumpkins_catplot_1.c55c409b71fea2ecc01921e64b91970542101f90bcccfa4aa3a205db8936f48b.ne.png)

    डेटा अवलोकन गरेर, तपाईं देख्न सक्नुहुन्छ कि Color डेटा Variety संग कसरी सम्बन्धित छ।

    ✅ यस categorical plot लाई हेरेर, केहि रोचक अन्वेषणहरू के हुन् भनेर कल्पना गर्नुहोस्।

### डेटा पूर्व-प्रक्रिया: feature र label encoding
हाम्रो pumpkins dataset मा सबै स्तम्भहरूको लागि string मानहरू छन्। मानवीय दृष्टिकोणबाट categorical डेटा संग काम गर्न सहज छ तर मेसिनहरूको लागि होइन। Machine learning algorithms संख्याहरू संग राम्रोसँग काम गर्छन्। त्यसैले encoding डेटा पूर्व-प्रक्रिया चरणमा एक महत्त्वपूर्ण कदम हो, किनकि यसले categorical डेटा लाई संख्यात्मक डेटा मा बदल्न सक्षम बनाउँछ, कुनै पनि जानकारी गुमाउनु बिना। राम्रो encoding ले राम्रो मोडेल निर्माण गर्न मद्दत गर्दछ।

Feature encoding को लागि दुई मुख्य प्रकारका encoders छन्:

1. Ordinal encoder: यो ordinal variables का लागि उपयुक्त छ, जुन categorical variables हुन् जहाँ तिनीहरूको डेटा तार्किक क्रम अनुसरण गर्दछ, जस्तै हाम्रो dataset मा `Item Size` स्तम्भ। यसले एक mapping सिर्जना गर्दछ जसले प्रत्येक वर्गलाई एक संख्याले प्रतिनिधित्व गर्दछ, जुन स्तम्भमा वर्गको क्रम हो।

    ```python
    from sklearn.preprocessing import OrdinalEncoder

    item_size_categories = [['sml', 'med', 'med-lge', 'lge', 'xlge', 'jbo', 'exjbo']]
    ordinal_features = ['Item Size']
    ordinal_encoder = OrdinalEncoder(categories=item_size_categories)
    ```

2. Categorical encoder: यो nominal variables का लागि उपयुक्त छ, जुन categorical variables हुन् जहाँ तिनीहरूको डेटा तार्किक क्रम अनुसरण गर्दैन, जस्तै `Item Size` बाहेकका सबै features। यो एक one-hot encoding हो, जसको मतलब प्रत्येक वर्गलाई एक binary स्तम्भले प्रतिनिधित्व गर्दछ: encoded variable बराबर 1 हुन्छ यदि pumpkin त्यो Variety मा पर्छ र अन्यथा 0।

    ```python
    from sklearn.preprocessing import OneHotEncoder

    categorical_features = ['City Name', 'Package', 'Variety', 'Origin']
    categorical_encoder = OneHotEncoder(sparse_output=False)
    ```
त्यसपछि, `ColumnTransformer` प्रयोग गरेर धेरै encoders लाई एकल चरणमा संयोजन गरिन्छ र तिनीहरूलाई उपयुक्त स्तम्भहरूमा लागू गरिन्छ।

```python
    from sklearn.compose import ColumnTransformer
    
    ct = ColumnTransformer(transformers=[
        ('ord', ordinal_encoder, ordinal_features),
        ('cat', categorical_encoder, categorical_features)
        ])
    
    ct.set_output(transform='pandas')
    encoded_features = ct.fit_transform(pumpkins)
```
अर्कोतर्फ, label लाई encode गर्न, हामी scikit-learn को `LabelEncoder` class प्रयोग गर्छौं, जुन एक utility class हो जसले labels लाई सामान्य बनाउन मद्दत गर्दछ ताकि तिनीहरू केवल 0 देखि n_classes-1 (यहाँ, 0 र 1) सम्मका मानहरू समावेश गर्छन्।

```python
    from sklearn.preprocessing import LabelEncoder

    label_encoder = LabelEncoder()
    encoded_label = label_encoder.fit_transform(pumpkins['Color'])
```
Features र label लाई encode गरेपछि, हामी तिनीहरूलाई नयाँ dataframe `encoded_pumpkins` मा merge गर्न सक्छौं।

```python
    encoded_pumpkins = encoded_features.assign(Color=encoded_label)
```
✅ `Item Size` स्तम्भको लागि ordinal encoder प्रयोग गर्ने के फाइदाहरू छन्?

### चरहरू बीचको सम्बन्ध विश्लेषण गर्नुहोस्

अब हामीले हाम्रो डेटा पूर्व-प्रक्रिया गरिसकेपछि, हामी features र label बीचको सम्बन्ध विश्लेषण गर्न सक्छौं ताकि मोडेलले features दिएर label कत्तिको राम्रोसँग भविष्यवाणी गर्न सक्नेछ भन्ने कुरा बुझ्न सकौं।
यस प्रकारको विश्लेषण गर्नको लागि डेटा plot गर्नु सबैभन्दा राम्रो तरिका हो। हामी फेरि Seaborn को `catplot` function प्रयोग गर्नेछौं, `Item Size`, `Variety` र `Color` बीचको सम्बन्धलाई categorical plot मा visualization गर्न। डेटा राम्रोसँग plot गर्नको लागि हामी encoded `Item Size` स्तम्भ र unencoded `Variety` स्तम्भ प्रयोग गर्नेछौं।

```python
    palette = {
    'ORANGE': 'orange',
    'WHITE': 'wheat',
    }
    pumpkins['Item Size'] = encoded_pumpkins['ord__Item Size']

    g = sns.catplot(
        data=pumpkins,
        x="Item Size", y="Color", row='Variety',
        kind="box", orient="h",
        sharex=False, margin_titles=True,
        height=1.8, aspect=4, palette=palette,
    )
    g.set(xlabel="Item Size", ylabel="").set(xlim=(0,6))
    g.set_titles(row_template="{row_name}")
```
![A catplot of visualized data](../../../../translated_images/pumpkins_catplot_2.87a354447880b3889278155957f8f60dd63db4598de5a6d0fda91c334d31f9f1.ne.png)

### Swarm plot प्रयोग गर्नुहोस्

किनकि Color एक binary वर्ग हो (White वा Not), यसलाई visualization को लागि 'एक [विशेष विधि](https://seaborn.pydata.org/tutorial/categorical.html?highlight=bar)' चाहिन्छ। यो वर्गको अन्य चरहरूसँगको सम्बन्ध visualization गर्न अन्य तरिकाहरू छन्।

तपाईं Seaborn plots प्रयोग गरेर चरहरूलाई सँगसँगै visualization गर्न सक्नुहुन्छ।

1. 'Swarm' plot प्रयोग गरेर मानहरूको वितरण देखाउनुहोस्:

    ```python
    palette = {
    0: 'orange',
    1: 'wheat'
    }
    sns.swarmplot(x="Color", y="ord__Item Size", data=encoded_pumpkins, palette=palette)
    ```

    ![A swarm of visualized data](../../../../translated_images/swarm_2.efeacfca536c2b577dc7b5f8891f28926663fbf62d893ab5e1278ae734ca104e.ne.png)

**ध्यान दिनुहोस्**: माथिको कोडले warning उत्पन्न गर्न सक्छ, किनकि seaborn ले यति धेरै datapoints लाई swarm plot मा प्रतिनिधित्व गर्न असफल हुन्छ। सम्भावित समाधान भनेको marker को आकार घटाउनु हो, 'size' parameter प्रयोग गरेर। तर, ध्यान दिनुहोस् कि यसले plot को readability मा असर गर्छ।

> **🧮 गणित देखाउनुहोस्**
>
> Logistic Regression 'maximum likelihood' को अवधारणामा आधारित छ [sigmoid functions](https://wikipedia.org/wiki/Sigmoid_function) प्रयोग गरेर। 'Sigmoid Function' को plot 'S' आकारको देखिन्छ। यसले मानलाई 0 र 1 बीचमा map गर्छ। यसको curve लाई 'logistic curve' पनि भनिन्छ। यसको formula यस्तो देखिन्छ:
>
> ![logistic function](../../../../translated_images/sigmoid.8b7ba9d095c789cf72780675d0d1d44980c3736617329abfc392dfc859799704.ne.png)
>
> जहाँ sigmoid को midpoint x को 0 बिन्दुमा हुन्छ, L curve को अधिकतम मान हो, र k curve को steepness हो। यदि function को परिणाम 0.5 भन्दा बढी छ भने, सो label लाई binary choice को '1' वर्ग दिइनेछ। यदि होइन भने, यसलाई '0' वर्गमा वर्गीकृत गरिनेछ।

## आफ्नो मोडेल निर्माण गर्नुहोस्

Scikit-learn मा binary classification पत्ता लगाउन मोडेल निर्माण गर्नु आश्चर्यजनक रूपमा सरल छ।

[![ML for beginners - Logistic Regression for classification of data](https://img.youtube.com/vi/MmZS2otPrQ8/0.jpg)](https://youtu.be/MmZS2otPrQ8 "ML for beginners - Logistic Regression for classification of data")

> 🎥 माथिको छवि क्लिक गरेर linear regression मोडेल निर्माण गर्ने छोटो भिडियो अवलोकन हेर्नुहोस्।

1. तपाईं आफ्नो classification मोडेलमा प्रयोग गर्न चाहनुभएको चरहरू चयन गर्नुहोस् र `train_test_split()` बोलाएर training र test sets विभाजन गर्नुहोस्:

    ```python
    from sklearn.model_selection import train_test_split
    
    X = encoded_pumpkins[encoded_pumpkins.columns.difference(['Color'])]
    y = encoded_pumpkins['Color']

    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
    
    ```

2. अब तपाईं आफ्नो मोडेललाई training डेटा प्रयोग गरेर `fit()` बोलाएर train गर्न सक्नुहुन्छ, र यसको परिणाम print गर्न सक्नुहुन्छ:

    ```python
    from sklearn.metrics import f1_score, classification_report 
    from sklearn.linear_model import LogisticRegression

    model = LogisticRegression()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)

    print(classification_report(y_test, predictions))
    print('Predicted labels: ', predictions)
    print('F1-score: ', f1_score(y_test, predictions))
    ```

    आफ्नो मोडेलको स्कोरबोर्ड हेर्नुहोस्। यो खराब छैन, तपाईंको dataset मा केवल लगभग 1000 पङ्क्तिहरू छन् भनेर विचार गर्दा:

    ```output
                       precision    recall  f1-score   support
    
                    0       0.94      0.98      0.96       166
                    1       0.85      0.67      0.75        33
    
        accuracy                                0.92       199
        macro avg           0.89      0.82      0.85       199
        weighted avg        0.92      0.92      0.92       199
    
        Predicted labels:  [0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0
        0 0 0 0 0 1 0 1 0 0 1 0 0 0 0 0 1 0 1 0 1 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0
        1 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 1 0 0 0 0 0 0 0 1 0
        0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 1 1 0
        0 0 0 0 1 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1
        0 0 0 1 0 0 0 0 0 0 0 0 1 1]
        F1-score:  0.7457627118644068
    ```

## Confusion Matrix मार्फत राम्रो समझ

जब तपाईं माथिका वस्तुहरू print गरेर स्कोरबोर्ड रिपोर्ट [terms](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html?highlight=classification_report#sklearn.metrics.classification_report) प्राप्त गर्न सक्नुहुन्छ, तपाईं आफ्नो मोडेललाई [confusion matrix](https://scikit-learn.org/stable/modules/model_evaluation.html#confusion-matrix) प्रयोग गरेर अझ सजिलै बुझ्न सक्नुहुन्छ।

> 🎓 '[Confusion matrix](https://wikipedia.org/wiki/Confusion_matrix)' (वा 'error matrix') एक तालिका हो जसले तपाईंको मोडेलको true vs. false positives र negatives व्यक्त गर्दछ, यसरी predictions को accuracy मापन गर्दछ।

1. Confusion matrix प्रयोग गर्न `confusion_matrix()` बोलाउनुहोस्:

    ```python
    from sklearn.metrics import confusion_matrix
    confusion_matrix(y_test, predictions)
    ```

    आफ्नो मोडेलको confusion matrix हेर्नुहोस्:

    ```output
    array([[162,   4],
           [ 11,  22]])
    ```

Scikit-learn मा confusion matrices Rows (axis 0) actual labels हुन् र columns (axis 1) predicted labels हुन्।

|       |   0   |   1   |
| :---: | :---: | :---: |
|   0   |  TN   |  FP   |
|   1   |  FN   |  TP   |

यहाँ के भइरहेको छ? मानौं हाम्रो मोडेललाई pumpkins लाई दुई binary वर्गहरू बीच वर्गीकृत गर्न भनिएको छ, वर्ग 'white' र वर्ग 'not-white'।

- यदि तपाईंको मोडेलले pumpkin लाई not white भनेर भविष्यवाणी गर्छ र यो वास्तवमा 'not-white' वर्गमा पर्छ भने हामी यसलाई true negative भन्छौं, जुन माथिको बायाँ नम्बरले देखाउँछ।
- यदि तपाईंको मोडेलले pumpkin लाई white भनेर भविष्यवाणी गर्छ र यो वास्तवमा 'not-white' वर्गमा पर्छ भने हामी यसलाई false negative भन्छौं, जुन तलको बायाँ नम्बरले देखाउँछ।
- यदि तपाईंको मोडेलले pumpkin लाई not white भनेर भविष्यवाणी गर्छ र यो वास्तवमा 'white' वर्गमा पर्छ भने हामी यसलाई false positive भन्छौं, जुन माथिको दायाँ नम्बरले देखाउँछ।
- यदि तपाईंको मोडेलले pumpkin लाई white भनेर भविष्यवाणी गर्छ र यो वास्तवमा 'white' वर्गमा पर्छ भने हामी यसलाई true positive भन्छौं, जुन तलको दायाँ नम्बरले देखाउँछ।

जसरी तपाईंले अनुमान गर्नुभएको छ, true positives र true negatives को संख्या बढी हुनु र false positives र false negatives को संख्या कम हुनु राम्रो हो, जसले मोडेल राम्रो प्रदर्शन गरेको संकेत गर्दछ।
कन्फ्युजन म्याट्रिक्सले प्रिसिजन र रिकलसँग कसरी सम्बन्ध राख्छ? याद गर्नुहोस्, माथि प्रिन्ट गरिएको क्लासिफिकेसन रिपोर्टले प्रिसिजन (0.85) र रिकल (0.67) देखाएको थियो।

प्रिसिजन = tp / (tp + fp) = 22 / (22 + 4) = 0.8461538461538461

रिकल = tp / (tp + fn) = 22 / (22 + 11) = 0.6666666666666666

✅ प्रश्न: कन्फ्युजन म्याट्रिक्स अनुसार, मोडेलले कस्तो प्रदर्शन गर्‍यो? उत्तर: नराम्रो होइन; धेरै साँचो नेगेटिभ्स छन्, तर केही गलत नेगेटिभ्स पनि छन्।

अब हामी कन्फ्युजन म्याट्रिक्सको TP/TN र FP/FN म्यापिङको मद्दतले पहिले देखिएका शब्दहरूलाई फेरि हेर्छौं:

🎓 प्रिसिजन: TP/(TP + FP) पुनःप्राप्त गरिएका उदाहरणहरूमा सान्दर्भिक उदाहरणहरूको अंश (जस्तै, कुन लेबलहरू राम्रोसँग लेबल गरिएका थिए)

🎓 रिकल: TP/(TP + FN) सान्दर्भिक उदाहरणहरूको अंश जुन पुनःप्राप्त गरियो, चाहे राम्रोसँग लेबल गरिएको होस् वा नभएको होस्

🎓 f1-स्कोर: (2 * प्रिसिजन * रिकल)/(प्रिसिजन + रिकल) प्रिसिजन र रिकलको भारित औसत, जसको उच्चतम मान 1 र न्यूनतम मान 0 हुन्छ

🎓 सपोर्ट: प्रत्येक लेबल पुनःप्राप्त भएको घटनाहरूको संख्या

🎓 एक्युरेसी: (TP + TN)/(TP + TN + FP + FN) कुनै नमुनाका लागि सही रूपमा भविष्यवाणी गरिएका लेबलहरूको प्रतिशत।

🎓 म्याक्रो औसत: प्रत्येक लेबलको लागि तौल नलिई गणना गरिएको औसत मेट्रिक्स।

🎓 तौलित औसत: प्रत्येक लेबलको लागि तौलको आधारमा गणना गरिएको औसत मेट्रिक्स, जसमा तौल सपोर्ट (प्रत्येक लेबलको साँचो घटनाहरूको संख्या) द्वारा निर्धारण गरिन्छ।

✅ के तपाईं अनुमान गर्न सक्नुहुन्छ कि यदि तपाईं आफ्नो मोडेलले गलत नेगेटिभ्सको संख्या घटाओस् भन्ने चाहनुहुन्छ भने कुन मेट्रिकलाई ध्यान दिनुपर्छ?

## यो मोडेलको ROC कर्भलाई भिजुअलाइज गर्नुहोस्

[![ML for beginners - Analyzing Logistic Regression Performance with ROC Curves](https://img.youtube.com/vi/GApO575jTA0/0.jpg)](https://youtu.be/GApO575jTA0 "ML for beginners - Analyzing Logistic Regression Performance with ROC Curves")

> 🎥 माथिको तस्बिरमा क्लिक गरेर ROC कर्भहरूको छोटो भिडियो अवलोकन हेर्नुहोस्

अब, तथाकथित 'ROC' कर्भ हेर्नको लागि अर्को भिजुअलाइजेसन गरौं:

```python
from sklearn.metrics import roc_curve, roc_auc_score
import matplotlib
import matplotlib.pyplot as plt
%matplotlib inline

y_scores = model.predict_proba(X_test)
fpr, tpr, thresholds = roc_curve(y_test, y_scores[:,1])

fig = plt.figure(figsize=(6, 6))
plt.plot([0, 1], [0, 1], 'k--')
plt.plot(fpr, tpr)
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve')
plt.show()
```

Matplotlib प्रयोग गरेर, मोडेलको [Receiving Operating Characteristic](https://scikit-learn.org/stable/auto_examples/model_selection/plot_roc.html?highlight=roc) वा ROC प्लट गर्नुहोस्। ROC कर्भहरू प्रायः क्लासिफायरको आउटपुटलाई यसको साँचो र गलत पोजिटिभ्सको सन्दर्भमा हेर्न प्रयोग गरिन्छ। "ROC कर्भहरूमा प्रायः Y अक्षमा साँचो पोजिटिभ दर र X अक्षमा गलत पोजिटिभ दर हुन्छ।" त्यसैले, कर्भको उचाइ र मध्यरेखा र कर्भको बीचको स्थान महत्त्वपूर्ण हुन्छ: तपाईं चाहनुहुन्छ कि कर्भ छिट्टै माथि र रेखा पार गरेर जाओस्। हाम्रो केसमा, सुरुमा केही गलत पोजिटिभ्स छन्, र त्यसपछि रेखा सही रूपमा माथि र पार जान्छ:

![ROC](../../../../translated_images/ROC_2.777f20cdfc4988ca683ade6850ac832cb70c96c12f1b910d294f270ef36e1a1c.ne.png)

अन्तमा, Scikit-learn को [`roc_auc_score` API](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_auc_score.html?highlight=roc_auc#sklearn.metrics.roc_auc_score) प्रयोग गरेर वास्तविक 'Area Under the Curve' (AUC) गणना गर्नुहोस्:

```python
auc = roc_auc_score(y_test,y_scores[:,1])
print(auc)
```  
नतिजा `0.9749908725812341` हो। AUC 0 देखि 1 सम्मको दायरामा हुन्छ, र तपाईं ठूलो स्कोर चाहनुहुन्छ, किनभने 100% सही भविष्यवाणी गर्ने मोडेलको AUC 1 हुनेछ; यस अवस्थामा, मोडेल _धेरै राम्रो_ छ।

भविष्यका क्लासिफिकेसन पाठहरूमा, तपाईं आफ्नो मोडेलको स्कोर सुधार गर्न कसरी पुनरावृत्ति गर्ने भनेर सिक्नुहुनेछ। तर अहिलेका लागि, बधाई छ! तपाईंले यी रिग्रेसन पाठहरू पूरा गर्नुभयो!

---
## 🚀 चुनौती

लजिस्टिक रिग्रेसनको बारेमा अझ धेरै कुरा बुझ्न बाँकी छ! तर सिक्ने सबैभन्दा राम्रो तरिका भनेको प्रयोग गर्नु हो। यस्तो प्रकारको विश्लेषणका लागि उपयुक्त डेटासेट खोज्नुहोस् र त्यसमा आधारित मोडेल बनाउनुहोस्। तपाईंले के सिक्नुहुन्छ? सुझाव: [Kaggle](https://www.kaggle.com/search?q=logistic+regression+datasets) मा रोचक डेटासेटहरू खोज्नुहोस्।

## [पाठपछिको क्विज](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/16/)

## समीक्षा र आत्म-अध्ययन

[स्ट्यानफोर्डको यो पेपर](https://web.stanford.edu/~jurafsky/slp3/5.pdf) को पहिलो केही पृष्ठहरू पढ्नुहोस्, जसले लजिस्टिक रिग्रेसनका केही व्यावहारिक प्रयोगहरू देखाउँछ। अहिलेसम्म हामीले अध्ययन गरेका रिग्रेसनका प्रकारहरूमध्ये कुन कार्यका लागि कुन उपयुक्त हुन्छ भनेर सोच्नुहोस्। कुन विधि सबैभन्दा राम्रो काम गर्ला?

## असाइनमेन्ट

[यो रिग्रेसन पुन: प्रयास गर्नुहोस्](assignment.md)

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटि वा अशुद्धता हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।