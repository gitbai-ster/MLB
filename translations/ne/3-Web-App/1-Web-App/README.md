<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2680c691fbdb6367f350761a275e2508",
  "translation_date": "2025-08-29T17:45:40+00:00",
  "source_file": "3-Web-App/1-Web-App/README.md",
  "language_code": "ne"
}
-->
# ML मोडेल प्रयोग गर्न वेब एप बनाउनुहोस्

यस पाठमा, तपाईंले एक डाटासेटमा ML मोडेल प्रशिक्षण गर्नुहुनेछ जुन पृथ्वीभन्दा बाहिरको छ: _पछिल्लो शताब्दीभरिका UFO देखाइहरू_, जुन NUFORC को डाटाबेसबाट लिइएको हो।

तपाईंले सिक्नुहुनेछ:

- कसरी प्रशिक्षित मोडेललाई 'pickle' गर्ने
- कसरी त्यो मोडेललाई Flask एपमा प्रयोग गर्ने

हामीले डाटा सफा गर्न र मोडेल प्रशिक्षण गर्न नोटबुकहरूको प्रयोग जारी राख्नेछौं, तर तपाईं यस प्रक्रियालाई अझ अगाडि लैजान सक्नुहुन्छ र मोडेललाई 'जंगली' मा, अर्थात् वेब एपमा प्रयोग गरेर अन्वेषण गर्न सक्नुहुन्छ।

यसका लागि, तपाईंले Flask प्रयोग गरेर वेब एप निर्माण गर्न आवश्यक छ।

## [पाठपूर्व प्रश्नोत्तरी](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/17/)

## एप निर्माण गर्दै

मेसिन लर्निङ मोडेलहरू उपभोग गर्नका लागि वेब एपहरू निर्माण गर्ने धेरै तरिकाहरू छन्। तपाईंको वेब आर्किटेक्चरले तपाईंको मोडेल कसरी प्रशिक्षण गरिन्छ भन्नेमा प्रभाव पार्न सक्छ। कल्पना गर्नुहोस् कि तपाईं यस्तो व्यवसायमा काम गर्दै हुनुहुन्छ जहाँ डाटा विज्ञान समूहले मोडेल प्रशिक्षण गरेको छ, जुन उनीहरूले तपाईंलाई एपमा प्रयोग गर्न चाहन्छन्।

### विचार गर्नुपर्ने कुराहरू

तपाईंले धेरै प्रश्नहरू सोध्नुपर्नेछ:

- **यो वेब एप हो कि मोबाइल एप?** यदि तपाईं मोबाइल एप निर्माण गर्दै हुनुहुन्छ वा IoT सन्दर्भमा मोडेल प्रयोग गर्न आवश्यक छ भने, तपाईं [TensorFlow Lite](https://www.tensorflow.org/lite/) प्रयोग गर्न सक्नुहुन्छ र मोडेललाई Android वा iOS एपमा प्रयोग गर्न सक्नुहुन्छ।
- **मोडेल कहाँ रहनेछ?** क्लाउडमा कि स्थानीय रूपमा?
- **अफलाइन समर्थन।** के एपले अफलाइन काम गर्नुपर्नेछ?
- **मोडेल प्रशिक्षण गर्न कुन प्रविधि प्रयोग गरिएको थियो?** चयन गरिएको प्रविधिले तपाईंले प्रयोग गर्नुपर्ने उपकरणहरूमा प्रभाव पार्न सक्छ।
    - **TensorFlow प्रयोग गर्दै।** उदाहरणका लागि, यदि तपाईं TensorFlow प्रयोग गरेर मोडेल प्रशिक्षण गर्दै हुनुहुन्छ भने, त्यो इकोसिस्टमले [TensorFlow.js](https://www.tensorflow.org/js/) प्रयोग गरेर वेब एपमा प्रयोग गर्नका लागि TensorFlow मोडेल रूपान्तरण गर्ने क्षमता प्रदान गर्दछ।
    - **PyTorch प्रयोग गर्दै।** यदि तपाईं [PyTorch](https://pytorch.org/) जस्तो पुस्तकालय प्रयोग गरेर मोडेल निर्माण गर्दै हुनुहुन्छ भने, तपाईंले यसलाई [ONNX](https://onnx.ai/) (Open Neural Network Exchange) ढाँचामा निर्यात गर्ने विकल्प पाउनुहुन्छ, जसले [Onnx Runtime](https://www.onnxruntime.ai/) प्रयोग गर्ने JavaScript वेब एपहरूमा प्रयोग गर्न सकिन्छ। यो विकल्पलाई भविष्यको पाठमा Scikit-learn-प्रशिक्षित मोडेलका लागि अन्वेषण गरिनेछ।
    - **Lobe.ai वा Azure Custom Vision प्रयोग गर्दै।** यदि तपाईं [Lobe.ai](https://lobe.ai/) वा [Azure Custom Vision](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/?WT.mc_id=academic-77952-leestott) जस्ता ML SaaS (Software as a Service) प्रणाली प्रयोग गरेर मोडेल प्रशिक्षण गर्दै हुनुहुन्छ भने, यस प्रकारको सफ्टवेयरले धेरै प्लेटफर्महरूको लागि मोडेल निर्यात गर्ने तरिकाहरू प्रदान गर्दछ, जसमा क्लाउडमा तपाईंको अनलाइन एपद्वारा सोधिने API निर्माण गर्ने विकल्प पनि समावेश छ।

तपाईंले ब्राउजरमै मोडेल प्रशिक्षण गर्न सक्ने सम्पूर्ण Flask वेब एप निर्माण गर्ने अवसर पनि पाउनुहुन्छ। यो TensorFlow.js प्रयोग गरेर JavaScript सन्दर्भमा पनि गर्न सकिन्छ।

हाम्रो उद्देश्यका लागि, किनभने हामी Python-आधारित नोटबुकहरूसँग काम गर्दैछौं, आउनुहोस्, प्रशिक्षित मोडेललाई Python-निर्मित वेब एपले पढ्न मिल्ने ढाँचामा निर्यात गर्नका लागि आवश्यक चरणहरूको अन्वेषण गरौं।

## उपकरण

यस कार्यका लागि तपाईंलाई दुई उपकरणहरू चाहिन्छ: Flask र Pickle, दुवै Python मा चल्छन्।

✅ [Flask](https://palletsprojects.com/p/flask/) के हो? यसको सिर्जनाकर्ताहरूले 'माइक्रो-फ्रेमवर्क' भनेर परिभाषित गरेको Flask ले Python प्रयोग गरेर वेब फ्रेमवर्कहरूको आधारभूत सुविधाहरू र वेब पृष्ठहरू निर्माण गर्न टेम्प्लेटिङ इन्जिन प्रदान गर्दछ। Flask प्रयोग गरेर निर्माण अभ्यास गर्न [यो सिकाइ मोड्युल](https://docs.microsoft.com/learn/modules/python-flask-build-ai-web-app?WT.mc_id=academic-77952-leestott) हेर्नुहोस्।

✅ [Pickle](https://docs.python.org/3/library/pickle.html) के हो? Pickle 🥒 एउटा Python मोड्युल हो जसले Python वस्तु संरचनालाई सिरियलाइज र डी-सिरियलाइज गर्दछ। जब तपाईं मोडेललाई 'pickle' गर्नुहुन्छ, तपाईं यसको संरचनालाई वेबमा प्रयोग गर्नका लागि सिरियलाइज वा समतल बनाउनुहुन्छ। सावधान रहनुहोस्: pickle स्वाभाविक रूपमा सुरक्षित छैन, त्यसैले यदि तपाईंलाई कुनै फाइल 'un-pickle' गर्न भनिएको छ भने सावधान रहनुहोस्। Pickled फाइलको उपसर्ग `.pkl` हुन्छ।

## अभ्यास - तपाईंको डाटा सफा गर्नुहोस्

यस पाठमा तपाईंले [NUFORC](https://nuforc.org) (The National UFO Reporting Center) द्वारा सङ्कलित ८०,००० UFO देखाइहरूको डाटाको प्रयोग गर्नुहुनेछ। यस डाटामा UFO देखाइहरूको केही रोचक विवरणहरू छन्, जस्तै:

- **लामो विवरणको उदाहरण।** "रातको समयमा घाँसे मैदानमा प्रकाशको किरणबाट एक व्यक्ति बाहिर निस्कन्छ र टेक्सास इन्स्ट्रुमेन्ट्सको पार्किङ क्षेत्रमा दौडन्छ।"
- **छोटो विवरणको उदाहरण।** "प्रकाशहरूले हामीलाई पछ्यायो।"

[ufos.csv](../../../../3-Web-App/1-Web-App/data/ufos.csv) स्प्रेडशीटमा `city`, `state` र `country` जहाँ देखाइ भएको थियो, वस्तुको `shape` र यसको `latitude` र `longitude` बारेका स्तम्भहरू समावेश छन्।

यस पाठमा समावेश गरिएको खाली [notebook](notebook.ipynb) मा:

1. `pandas`, `matplotlib`, र `numpy` लाई आयात गर्नुहोस्, जस्तै तपाईंले अघिल्ला पाठहरूमा गर्नुभएको थियो, र ufos स्प्रेडशीट आयात गर्नुहोस्। तपाईं डाटासेटको नमूना हेर्न सक्नुहुन्छ:

    ```python
    import pandas as pd
    import numpy as np
    
    ufos = pd.read_csv('./data/ufos.csv')
    ufos.head()
    ```

1. ufos डाटालाई नयाँ शीर्षकहरूसहित सानो डाटाफ्रेममा रूपान्तरण गर्नुहोस्। `Country` फिल्डका अद्वितीय मानहरू जाँच गर्नुहोस्।

    ```python
    ufos = pd.DataFrame({'Seconds': ufos['duration (seconds)'], 'Country': ufos['country'],'Latitude': ufos['latitude'],'Longitude': ufos['longitude']})
    
    ufos.Country.unique()
    ```

1. अब, हामीले सामना गर्नुपर्ने डाटाको मात्रा घटाउन, कुनै पनि null मानहरू हटाएर र १-६० सेकेन्डको बीचका देखाइहरू मात्र आयात गरेर डाटा घटाउन सक्नुहुन्छ:

    ```python
    ufos.dropna(inplace=True)
    
    ufos = ufos[(ufos['Seconds'] >= 1) & (ufos['Seconds'] <= 60)]
    
    ufos.info()
    ```

1. Scikit-learn को `LabelEncoder` पुस्तकालय आयात गर्नुहोस्, जसले देशहरूको पाठ मानहरूलाई सङ्ख्यामा रूपान्तरण गर्दछ:

    ✅ LabelEncoder ले डाटालाई वर्णानुक्रममा कोड गर्दछ

    ```python
    from sklearn.preprocessing import LabelEncoder
    
    ufos['Country'] = LabelEncoder().fit_transform(ufos['Country'])
    
    ufos.head()
    ```

    तपाईंको डाटा यसरी देखिनुपर्छ:

    ```output
    	Seconds	Country	Latitude	Longitude
    2	20.0	3		53.200000	-2.916667
    3	20.0	4		28.978333	-96.645833
    14	30.0	4		35.823889	-80.253611
    23	60.0	4		45.582778	-122.352222
    24	3.0		3		51.783333	-0.783333
    ```

## अभ्यास - तपाईंको मोडेल निर्माण गर्नुहोस्

अब तपाईंले डाटालाई प्रशिक्षण र परीक्षण समूहमा विभाजन गरेर मोडेल प्रशिक्षण गर्न तयार हुन सक्नुहुन्छ।

1. तपाईंले प्रशिक्षण गर्न चाहनुभएको तीन विशेषताहरूलाई X भेक्टरको रूपमा चयन गर्नुहोस्, र y भेक्टर `Country` हुनेछ। तपाईंले `Seconds`, `Latitude` र `Longitude` इनपुट गर्न चाहनुहुन्छ र देशको id फिर्ता प्राप्त गर्न चाहनुहुन्छ।

    ```python
    from sklearn.model_selection import train_test_split
    
    Selected_features = ['Seconds','Latitude','Longitude']
    
    X = ufos[Selected_features]
    y = ufos['Country']
    
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
    ```

1. Logistic regression प्रयोग गरेर तपाईंको मोडेल प्रशिक्षण गर्नुहोस्:

    ```python
    from sklearn.metrics import accuracy_score, classification_report
    from sklearn.linear_model import LogisticRegression
    model = LogisticRegression()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    
    print(classification_report(y_test, predictions))
    print('Predicted labels: ', predictions)
    print('Accuracy: ', accuracy_score(y_test, predictions))
    ```

सटीकता नराम्रो छैन **(करिब ९५%)**, जुन आश्चर्यजनक होइन, किनभने `Country` र `Latitude/Longitude` सम्बन्धित छन्।

तपाईंले निर्माण गर्नुभएको मोडेल धेरै क्रान्तिकारी छैन, किनभने तपाईंले `Latitude` र `Longitude` बाट `Country` अनुमान गर्न सक्नुहुन्छ, तर यो कच्चा डाटाबाट प्रशिक्षण गर्ने, निर्यात गर्ने, र त्यसपछि यो मोडेललाई वेब एपमा प्रयोग गर्ने अभ्यास गर्न राम्रो हो।

## अभ्यास - तपाईंको मोडेललाई 'pickle' गर्नुहोस्

अब, तपाईंको मोडेललाई _pickle_ गर्ने समय हो! तपाईंले यो केही लाइनको कोडमा गर्न सक्नुहुन्छ। एक पटक यो _pickled_ भएपछि, तपाईंको pickled मोडेल लोड गर्नुहोस् र सेकेन्ड, अक्षांश र देशान्तरका मानहरू समावेश भएको नमूना डाटा एरेमा परीक्षण गर्नुहोस्,

```python
import pickle
model_filename = 'ufo-model.pkl'
pickle.dump(model, open(model_filename,'wb'))

model = pickle.load(open('ufo-model.pkl','rb'))
print(model.predict([[50,44,-12]]))
```

मोडेलले **'3'** फिर्ता गर्दछ, जुन UK को देश कोड हो। अचम्मको! 👽

## अभ्यास - Flask एप निर्माण गर्नुहोस्

अब तपाईंले मोडेललाई कल गर्न र यस्तै परिणामहरू फिर्ता गर्न Flask एप निर्माण गर्न सक्नुहुन्छ, तर अझ दृश्यात्मक रूपमा आकर्षक तरिकामा।

1. _notebook.ipynb_ फाइलको छेउमा **web-app** नामक फोल्डर सिर्जना गर्नुहोस्, जहाँ तपाईंको _ufo-model.pkl_ फाइल अवस्थित छ।

1. त्यस फोल्डरमा तीन थप फोल्डरहरू सिर्जना गर्नुहोस्: **static**, जसको भित्र **css** नामक फोल्डर छ, र **templates**। अब तपाईंले निम्न फाइलहरू र डाइरेक्टरीहरू पाउनुहुनेछ:

    ```output
    web-app/
      static/
        css/
      templates/
    notebook.ipynb
    ufo-model.pkl
    ```

    ✅ समाप्त एपको दृश्यका लागि समाधान फोल्डरलाई हेर्नुहोस्

1. _web-app_ फोल्डरमा सिर्जना गर्नुपर्ने पहिलो फाइल **requirements.txt** हो। JavaScript एपमा _package.json_ जस्तै, यो फाइलले एपले आवश्यक पर्ने निर्भरताहरू सूचीबद्ध गर्दछ। **requirements.txt** मा निम्न लाइनहरू थप्नुहोस्:

    ```text
    scikit-learn
    pandas
    numpy
    flask
    ```

1. अब, यो फाइल चलाउन _web-app_ मा जानुहोस्:

    ```bash
    cd web-app
    ```

1. तपाईंको टर्मिनलमा `pip install` टाइप गर्नुहोस्, _requirements.txt_ मा सूचीबद्ध पुस्तकालयहरू स्थापना गर्न:

    ```bash
    pip install -r requirements.txt
    ```

1. अब, एप समाप्त गर्न तीन थप फाइलहरू सिर्जना गर्न तयार हुनुहोस्:

    1. _web-app_ को रुटमा **app.py** सिर्जना गर्नुहोस्।
    2. _templates_ डाइरेक्टरीमा **index.html** सिर्जना गर्नुहोस्।
    3. _static/css_ डाइरेक्टरीमा **styles.css** सिर्जना गर्नुहोस्।

1. _styles.css_ फाइलमा केही शैलीहरू थप्नुहोस्:

    ```css
    body {
    	width: 100%;
    	height: 100%;
    	font-family: 'Helvetica';
    	background: black;
    	color: #fff;
    	text-align: center;
    	letter-spacing: 1.4px;
    	font-size: 30px;
    }
    
    input {
    	min-width: 150px;
    }
    
    .grid {
    	width: 300px;
    	border: 1px solid #2d2d2d;
    	display: grid;
    	justify-content: center;
    	margin: 20px auto;
    }
    
    .box {
    	color: #fff;
    	background: #2d2d2d;
    	padding: 12px;
    	display: inline-block;
    }
    ```

1. त्यसपछि, _index.html_ फाइल निर्माण गर्नुहोस्:

    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8">
        <title>🛸 UFO Appearance Prediction! 👽</title>
        <link rel="stylesheet" href="{{ url_for('static', filename='css/styles.css') }}">
      </head>
    
      <body>
        <div class="grid">
    
          <div class="box">
    
            <p>According to the number of seconds, latitude and longitude, which country is likely to have reported seeing a UFO?</p>
    
            <form action="{{ url_for('predict')}}" method="post">
              <input type="number" name="seconds" placeholder="Seconds" required="required" min="0" max="60" />
              <input type="text" name="latitude" placeholder="Latitude" required="required" />
              <input type="text" name="longitude" placeholder="Longitude" required="required" />
              <button type="submit" class="btn">Predict country where the UFO is seen</button>
            </form>
    
            <p>{{ prediction_text }}</p>
    
          </div>
    
        </div>
    
      </body>
    </html>
    ```

    यस फाइलमा टेम्प्लेटिङलाई हेर्नुहोस्। ध्यान दिनुहोस्, यसमा एपले प्रदान गर्ने भेरिएबलहरू वरिपरि 'mustache' सिन्ट्याक्स छ, जस्तै भविष्यवाणी पाठ: `{{}}`। त्यहाँ एउटा फारम पनि छ, जसले `/predict` रूटमा भविष्यवाणी पोस्ट गर्दछ।

    अन्ततः, तपाईंले Python फाइल निर्माण गर्न तयार हुनुहुन्छ, जसले मोडेलको उपभोग र भविष्यवाणीहरूको प्रदर्शनलाई चलाउँछ:

1. `app.py` मा निम्न थप्नुहोस्:

    ```python
    import numpy as np
    from flask import Flask, request, render_template
    import pickle
    
    app = Flask(__name__)
    
    model = pickle.load(open("./ufo-model.pkl", "rb"))
    
    
    @app.route("/")
    def home():
        return render_template("index.html")
    
    
    @app.route("/predict", methods=["POST"])
    def predict():
    
        int_features = [int(x) for x in request.form.values()]
        final_features = [np.array(int_features)]
        prediction = model.predict(final_features)
    
        output = prediction[0]
    
        countries = ["Australia", "Canada", "Germany", "UK", "US"]
    
        return render_template(
            "index.html", prediction_text="Likely country: {}".format(countries[output])
        )
    
    
    if __name__ == "__main__":
        app.run(debug=True)
    ```

    > 💡 सुझाव: जब तपाईं Flask प्रयोग गरेर वेब एप चलाउँदा [`debug=True`](https://www.askpython.com/python-modules/flask/flask-debug-mode) थप्नुहुन्छ, तपाईंको एपमा गरिएका कुनै पनि परिवर्तनहरू तुरुन्तै प्रतिबिम्बित हुन्छन्, सर्भर पुनः सुरु गर्न आवश्यक पर्दैन। सावधान रहनुहोस्! उत्पादन एपमा यो मोड सक्षम नगर्नुहोस्।

यदि तपाईं `python app.py` वा `python3 app.py` चलाउनुहुन्छ भने - तपाईंको वेब सर्भर स्थानीय रूपमा सुरु हुन्छ, र तपाईं एउटा छोटो फारम भर्न सक्नुहुन्छ, जसले तपाईंको UFO देखाइहरूको स्थानबारेको जलिरहेको प्रश्नको उत्तर दिन्छ!

त्यसअघि, `app.py` का भागहरू हेर्नुहोस्:

1. पहिलो, निर्भरताहरू लोड गरिन्छ र एप सुरु हुन्छ।
1. त्यसपछि, मोडेल आयात गरिन्छ।
1. त्यसपछि, होम रूटमा index.html प्रस्तुत गरिन्छ।

`/predict` रूटमा, फारम पोस्ट हुँदा केही चीजहरू हुन्छन्:

1. फारम भेरिएबलहरू सङ्कलन गरिन्छ र numpy एरेमा रूपान्तरण गरिन्छ। त्यसपछि तिनीहरूलाई मोडेलमा पठाइन्छ र भविष्यवाणी फिर्ता गरिन्छ।
2. हामीले प्रदर्शन गर्न चाहेका देशहरूलाई भविष्यवाणी गरिएको देश कोडबाट पठनीय पाठको रूपमा पुनः प्रस्तुत गरिन्छ, र त्यो मान index.html मा पठाइन्छ, जसले टेम्प्लेटमा प्रस्तुत गर्दछ।

Flask र pickled मोडेलको साथमा मोडेल प्रयोग गर्नु तुलनात्मक रूपमा सरल छ। सबैभन्दा गाह्रो कुरा भनेको मोडेललाई भविष्यवाणी प्राप्त गर्न पठाउनुपर्ने डाटाको स्वरूप बुझ्नु हो। यो सबै मोडेल कसरी प्रशिक्षण गरियो भन्नेमा निर्भर गर्दछ। यसमा भविष्यवाणी प्राप्त गर्न तीनवटा डाटा पोइन्टहरू इनपुट गर्नुपर्छ।

पेशागत सेटिङमा, तपाईंले मोडेल प्रशिक्षण गर्ने व्यक्तिहरू र वेब वा मोबाइल एपमा यसलाई उपभोग गर्ने व्यक्तिहरूबीच राम्रो सञ्चार आवश्यक छ भन्ने देख्न सक्नुहुन्छ। हाम्रो मामिलामा, यो केवल एक व्यक्ति, तपाईं हो!

---

## 🚀 चुनौती

नोटबुकमा काम गरेर मोडेललाई Flask एपमा आयात गर्नुको सट्टा, तपाईंले Flask एपभित्रै मोडेल प्रशिक्षण गर्न सक्नुहुन्छ! तपाईंको नोटबुकमा रहेको Python कोडलाई रूपान्तरण गरेर, सम्भवतः तपाईंको डाटा सफा भएपछि, एपभित्रै `train` नामक रूटमा मोडेल प्रशिक्षण गर्न प्रयास गर्नुहोस्। यो विधि अपनाउँदा के फाइदा र बेफाइदा छन्?

## [पाठपछिको प्रश्नोत्तरी](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/18/)

## समीक्षा र आत्म अध्ययन

ML मोडेलहरू उपभोग गर्न वेब एप निर्माण गर्ने धेरै तरिकाहरू छन्। JavaScript वा Python प्रयोग गरेर वेब एप निर्माण गर्न सकिने तरिकाहरूको सूची बनाउनुहोस्। आर्किटेक्चर विचार गर्नुहोस्: के मोडेल एपमै रहनुपर्छ कि क्लाउडमा? यदि पछिल्लो हो भने, तपाईं यसलाई कसरी पहुँच गर्नुहुन्छ? लागू गरिएको ML वेब समाधानको लागि आर्किटेक्चरल मोडेल बनाउनुहोस्।

## असाइनमेन्ट

[अर्को मोडेल प्रयास गर्नुहोस्](assignment.md)

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटि वा अशुद्धता हुन सक्छ। यसको मूल भाषामा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।