<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ad2cf19d7490247558d20a6a59650d13",
  "translation_date": "2025-08-29T17:52:30+00:00",
  "source_file": "4-Classification/4-Applied/README.md",
  "language_code": "mr"
}
-->
# क्युझिन शिफारस वेब अ‍ॅप तयार करा

या धड्यात, तुम्ही मागील धड्यांमध्ये शिकलेल्या तंत्रांचा वापर करून आणि या मालिकेत वापरलेल्या स्वादिष्ट क्युझिन डेटासेटसह वर्गीकरण मॉडेल तयार कराल. याशिवाय, तुम्ही जतन केलेल्या मॉडेलचा वापर करण्यासाठी एक छोटासा वेब अ‍ॅप तयार कराल, ज्यामध्ये Onnx च्या वेब रनटाइमचा उपयोग केला जाईल.

यंत्रमानव शिक्षणाचा सर्वात उपयुक्त व्यावहारिक उपयोग म्हणजे शिफारस प्रणाली तयार करणे, आणि तुम्ही आज त्या दिशेने पहिले पाऊल उचलू शकता!

[![या वेब अ‍ॅपचे सादरीकरण](https://img.youtube.com/vi/17wdM9AHMfg/0.jpg)](https://youtu.be/17wdM9AHMfg "Applied ML")

> 🎥 वरील प्रतिमेवर क्लिक करा व्हिडिओसाठी: जेन लूपर वर्गीकृत क्युझिन डेटाचा वापर करून वेब अ‍ॅप तयार करतात

## [पूर्व-व्याख्यान प्रश्नमंजुषा](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/25/)

या धड्यात तुम्ही शिकाल:

- मॉडेल कसे तयार करायचे आणि ते Onnx मॉडेल म्हणून कसे जतन करायचे
- Netron चा वापर करून मॉडेल कसे तपासायचे
- तुमच्या वेब अ‍ॅपमध्ये अंदाजासाठी मॉडेलचा वापर कसा करायचा

## तुमचे मॉडेल तयार करा

व्यवसाय प्रणालींसाठी या तंत्रज्ञानाचा उपयोग करण्यासाठी लागू ML प्रणाली तयार करणे महत्त्वाचे आहे. तुम्ही तुमच्या वेब अ‍ॅप्लिकेशनमध्ये मॉडेल्स वापरू शकता (आणि आवश्यक असल्यास ऑफलाइन संदर्भात देखील वापरू शकता) Onnx चा वापर करून.

[मागील धड्यात](../../3-Web-App/1-Web-App/README.md), तुम्ही UFO sightings वर आधारित एक Regression मॉडेल तयार केले होते, "pickle" केले होते, आणि Flask अ‍ॅपमध्ये वापरले होते. ही आर्किटेक्चर जाणून घेणे खूप उपयुक्त आहे, परंतु हे पूर्ण-स्टॅक Python अ‍ॅप आहे, आणि तुमच्या गरजा JavaScript अ‍ॅप्लिकेशनचा वापर समाविष्ट करू शकतात.

या धड्यात, तुम्ही अंदाजासाठी JavaScript-आधारित प्रणाली तयार करू शकता. परंतु, प्रथम तुम्हाला मॉडेल प्रशिक्षण द्यावे लागेल आणि ते Onnx सह वापरण्यासाठी रूपांतरित करावे लागेल.

## व्यायाम - वर्गीकरण मॉडेल प्रशिक्षण द्या

प्रथम, आपण वापरलेल्या स्वच्छ क्युझिन डेटासेटचा वापर करून वर्गीकरण मॉडेल प्रशिक्षण द्या.

1. उपयुक्त लायब्ररी आयात करून सुरुवात करा:

    ```python
    !pip install skl2onnx
    import pandas as pd 
    ```

    तुम्हाला '[skl2onnx](https://onnx.ai/sklearn-onnx/)' ची आवश्यकता आहे जे Scikit-learn मॉडेलला Onnx स्वरूपात रूपांतरित करण्यात मदत करते.

1. नंतर, तुमच्या डेटासह काम करा जसे तुम्ही मागील धड्यांमध्ये केले होते, `read_csv()` वापरून CSV फाइल वाचा:

    ```python
    data = pd.read_csv('../data/cleaned_cuisines.csv')
    data.head()
    ```

1. पहिल्या दोन अनावश्यक स्तंभ काढा आणि उर्वरित डेटा 'X' म्हणून जतन करा:

    ```python
    X = data.iloc[:,2:]
    X.head()
    ```

1. लेबल्स 'y' म्हणून जतन करा:

    ```python
    y = data[['cuisine']]
    y.head()
    
    ```

### प्रशिक्षण प्रक्रिया सुरू करा

आम्ही 'SVC' लायब्ररी वापरू जी चांगली अचूकता देते.

1. Scikit-learn मधून योग्य लायब्ररी आयात करा:

    ```python
    from sklearn.model_selection import train_test_split
    from sklearn.svm import SVC
    from sklearn.model_selection import cross_val_score
    from sklearn.metrics import accuracy_score,precision_score,confusion_matrix,classification_report
    ```

1. प्रशिक्षण आणि चाचणी संच वेगळे करा:

    ```python
    X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.3)
    ```

1. मागील धड्यात जसे केले होते तसे SVC वर्गीकरण मॉडेल तयार करा:

    ```python
    model = SVC(kernel='linear', C=10, probability=True,random_state=0)
    model.fit(X_train,y_train.values.ravel())
    ```

1. आता, तुमच्या मॉडेलची चाचणी करा, `predict()` कॉल करा:

    ```python
    y_pred = model.predict(X_test)
    ```

1. मॉडेलची गुणवत्ता तपासण्यासाठी वर्गीकरण अहवाल प्रिंट करा:

    ```python
    print(classification_report(y_test,y_pred))
    ```

    जसे आपण पूर्वी पाहिले होते, अचूकता चांगली आहे:

    ```output
                    precision    recall  f1-score   support
    
         chinese       0.72      0.69      0.70       257
          indian       0.91      0.87      0.89       243
        japanese       0.79      0.77      0.78       239
          korean       0.83      0.79      0.81       236
            thai       0.72      0.84      0.78       224
    
        accuracy                           0.79      1199
       macro avg       0.79      0.79      0.79      1199
    weighted avg       0.79      0.79      0.79      1199
    ```

### तुमचे मॉडेल Onnx मध्ये रूपांतरित करा

योग्य Tensor क्रमांकासह रूपांतर सुनिश्चित करा. या डेटासेटमध्ये 380 घटक सूचीबद्ध आहेत, त्यामुळे तुम्हाला `FloatTensorType` मध्ये तो क्रमांक नमूद करणे आवश्यक आहे:

1. 380 Tensor क्रमांक वापरून रूपांतरित करा.

    ```python
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
    
    initial_type = [('float_input', FloatTensorType([None, 380]))]
    options = {id(model): {'nocl': True, 'zipmap': False}}
    ```

1. onx तयार करा आणि **model.onnx** नावाच्या फाइलमध्ये जतन करा:

    ```python
    onx = convert_sklearn(model, initial_types=initial_type, options=options)
    with open("./model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
    ```

    > लक्षात ठेवा, तुम्ही तुमच्या रूपांतरण स्क्रिप्टमध्ये [options](https://onnx.ai/sklearn-onnx/parameterized.html) पास करू शकता. या प्रकरणात, आम्ही 'nocl' True आणि 'zipmap' False पास केला. कारण हे वर्गीकरण मॉडेल आहे, तुम्हाला ZipMap काढण्याचा पर्याय आहे जो डिक्शनरींची यादी तयार करतो (आवश्यक नाही). `nocl` वर्ग माहिती मॉडेलमध्ये समाविष्ट केली जात आहे याचा संदर्भ देते. `nocl` True सेट करून तुमच्या मॉडेलचा आकार कमी करा.

संपूर्ण नोटबुक चालवल्यानंतर आता Onnx मॉडेल तयार होईल आणि या फोल्डरमध्ये जतन होईल.

## तुमचे मॉडेल पहा

Onnx मॉडेल्स Visual Studio Code मध्ये फारसे दृश्यमान नाहीत, परंतु एक अतिशय चांगले विनामूल्य सॉफ्टवेअर आहे जे अनेक संशोधक मॉडेल योग्य प्रकारे तयार झाले आहे याची खात्री करण्यासाठी वापरतात. [Netron](https://github.com/lutzroeder/Netron) डाउनलोड करा आणि तुमची model.onnx फाइल उघडा. तुम्ही तुमचे साधे मॉडेल 380 इनपुट्स आणि वर्गीकरणासह व्हिज्युअलाइज केलेले पाहू शकता:

![Netron दृश्य](../../../../translated_images/netron.a05f39410211915e0f95e2c0e8b88f41e7d13d725faf660188f3802ba5c9e831.mr.png)

Netron तुमचे मॉडेल पाहण्यासाठी एक उपयुक्त साधन आहे.

आता तुम्ही हे छान मॉडेल वेब अ‍ॅपमध्ये वापरण्यास तयार आहात. चला एक अ‍ॅप तयार करूया जे तुमच्या फ्रिजमध्ये पाहताना आणि तुमच्या उरलेल्या घटकांच्या कोणत्या संयोजनाचा उपयोग करून दिलेल्या क्युझिन तयार करता येईल हे ठरवताना उपयुक्त ठरेल.

## शिफारस वेब अ‍ॅप्लिकेशन तयार करा

तुम्ही तुमचे मॉडेल थेट वेब अ‍ॅपमध्ये वापरू शकता. ही आर्किटेक्चर तुम्हाला ते स्थानिक पातळीवर आणि आवश्यक असल्यास ऑफलाइन चालवण्याची परवानगी देते. जिथे तुमची `model.onnx` फाइल जतन केली आहे त्या फोल्डरमध्ये `index.html` फाइल तयार करून सुरुवात करा.

1. या फाइलमध्ये _index.html_, खालील मार्कअप जोडा:

    ```html
    <!DOCTYPE html>
    <html>
        <header>
            <title>Cuisine Matcher</title>
        </header>
        <body>
            ...
        </body>
    </html>
    ```

1. आता, `body` टॅगमध्ये काम करताना, काही घटक दर्शविण्यासाठी चेकबॉक्सची यादी दाखवण्यासाठी थोडासा मार्कअप जोडा:

    ```html
    <h1>Check your refrigerator. What can you create?</h1>
            <div id="wrapper">
                <div class="boxCont">
                    <input type="checkbox" value="4" class="checkbox">
                    <label>apple</label>
                </div>
            
                <div class="boxCont">
                    <input type="checkbox" value="247" class="checkbox">
                    <label>pear</label>
                </div>
            
                <div class="boxCont">
                    <input type="checkbox" value="77" class="checkbox">
                    <label>cherry</label>
                </div>
    
                <div class="boxCont">
                    <input type="checkbox" value="126" class="checkbox">
                    <label>fenugreek</label>
                </div>
    
                <div class="boxCont">
                    <input type="checkbox" value="302" class="checkbox">
                    <label>sake</label>
                </div>
    
                <div class="boxCont">
                    <input type="checkbox" value="327" class="checkbox">
                    <label>soy sauce</label>
                </div>
    
                <div class="boxCont">
                    <input type="checkbox" value="112" class="checkbox">
                    <label>cumin</label>
                </div>
            </div>
            <div style="padding-top:10px">
                <button onClick="startInference()">What kind of cuisine can you make?</button>
            </div> 
    ```

    लक्षात घ्या की प्रत्येक चेकबॉक्सला एक मूल्य दिले आहे. हे डेटासेटनुसार घटक जिथे सापडतो त्या अनुक्रमणिकेचे प्रतिबिंबित करते. उदाहरणार्थ, Apple या वर्णमालिक यादीमध्ये पाचव्या स्तंभात आहे, त्यामुळे त्याचे मूल्य '4' आहे कारण आपण 0 पासून मोजायला सुरुवात करतो. [ingredients spreadsheet](../../../../4-Classification/data/ingredient_indexes.csv) सल्ला घ्या जेणेकरून दिलेल्या घटकाची अनुक्रमणिका शोधता येईल.

    index.html फाइलमध्ये तुमचे काम सुरू ठेवत, अंतिम बंद `</div>` नंतर स्क्रिप्ट ब्लॉक जोडा जिथे मॉडेल कॉल केले जाते.

1. प्रथम, [Onnx Runtime](https://www.onnxruntime.ai/) आयात करा:

    ```html
    <script src="https://cdn.jsdelivr.net/npm/onnxruntime-web@1.9.0/dist/ort.min.js"></script> 
    ```

    > Onnx Runtime तुमचे Onnx मॉडेल्स विविध हार्डवेअर प्लॅटफॉर्मवर चालवण्यासाठी सक्षम करण्यासाठी वापरले जाते, ज्यामध्ये ऑप्टिमायझेशन आणि वापरण्यासाठी API समाविष्ट आहे.

1. Runtime ठेवल्यानंतर, तुम्ही ते कॉल करू शकता:

    ```html
    <script>
        const ingredients = Array(380).fill(0);
        
        const checks = [...document.querySelectorAll('.checkbox')];
        
        checks.forEach(check => {
            check.addEventListener('change', function() {
                // toggle the state of the ingredient
                // based on the checkbox's value (1 or 0)
                ingredients[check.value] = check.checked ? 1 : 0;
            });
        });

        function testCheckboxes() {
            // validate if at least one checkbox is checked
            return checks.some(check => check.checked);
        }

        async function startInference() {

            let atLeastOneChecked = testCheckboxes()

            if (!atLeastOneChecked) {
                alert('Please select at least one ingredient.');
                return;
            }
            try {
                // create a new session and load the model.
                
                const session = await ort.InferenceSession.create('./model.onnx');

                const input = new ort.Tensor(new Float32Array(ingredients), [1, 380]);
                const feeds = { float_input: input };

                // feed inputs and run
                const results = await session.run(feeds);

                // read from results
                alert('You can enjoy ' + results.label.data[0] + ' cuisine today!')

            } catch (e) {
                console.log(`failed to inference ONNX model`);
                console.error(e);
            }
        }
               
    </script>
    ```

या कोडमध्ये, अनेक गोष्टी घडत आहेत:

1. तुम्ही 380 संभाव्य मूल्ये (1 किंवा 0) सेट करण्यासाठी आणि मॉडेलला अंदाजासाठी पाठवण्यासाठी एक array तयार केली आहे, घटक चेकबॉक्स तपासले गेले आहेत की नाही यावर अवलंबून.
2. तुम्ही चेकबॉक्सेसची array तयार केली आणि अ‍ॅप्लिकेशन सुरू झाल्यावर `init` फंक्शनमध्ये तपासले गेले आहेत की नाही हे ठरवण्याचा मार्ग तयार केला. जेव्हा चेकबॉक्स तपासले जाते, तेव्हा `ingredients` array निवडलेल्या घटकाचे प्रतिबिंबित करण्यासाठी बदलले जाते.
3. तुम्ही `testCheckboxes` फंक्शन तयार केले जे तपासते की कोणताही चेकबॉक्स तपासला गेला आहे का.
4. तुम्ही बटण दाबले असता `startInference` फंक्शन वापरता आणि, जर कोणताही चेकबॉक्स तपासला गेला असेल, तर तुम्ही अंदाज सुरू करता.
5. अंदाज दिनचर्या समाविष्ट करते:
   1. मॉडेलचे असिंक्रोनस लोड सेट करणे
   2. मॉडेलला पाठवण्यासाठी Tensor संरचना तयार करणे
   3. 'feeds' तयार करणे जे तुम्ही तुमचे मॉडेल प्रशिक्षण देताना तयार केलेल्या `float_input` इनपुटचे प्रतिबिंबित करते (तुम्ही Netron वापरून ते नाव सत्यापित करू शकता)
   4. हे 'feeds' मॉडेलला पाठवणे आणि प्रतिसादाची वाट पाहणे

## तुमचे अ‍ॅप्लिकेशन तपासा

Visual Studio Code मध्ये टर्मिनल सत्र उघडा जिथे तुमची index.html फाइल आहे. सुनिश्चित करा की तुमच्याकडे [http-server](https://www.npmjs.com/package/http-server) जागतिक स्तरावर स्थापित आहे, आणि प्रॉम्प्टवर `http-server` टाइप करा. एक localhost उघडेल आणि तुम्ही तुमचे वेब अ‍ॅप पाहू शकता. विविध घटकांवर आधारित कोणते क्युझिन शिफारस केले जाते ते तपासा:

![घटक वेब अ‍ॅप](../../../../translated_images/web-app.4c76450cabe20036f8ec6d5e05ccc0c1c064f0d8f2fe3304d3bcc0198f7dc139.mr.png)

अभिनंदन, तुम्ही काही फील्डसह 'शिफारस' वेब अ‍ॅप तयार केले आहे. या प्रणालीला तयार करण्यात थोडा वेळ घ्या!

## 🚀चॅलेंज

तुमचे वेब अ‍ॅप खूपच साधे आहे, त्यामुळे [ingredient_indexes](../../../../4-Classification/data/ingredient_indexes.csv) डेटामधील घटक आणि त्यांची अनुक्रमणिका वापरून ते तयार करत रहा. कोणते स्वाद संयोजन दिलेल्या राष्ट्रीय पदार्थ तयार करण्यासाठी कार्य करते?

## [व्याख्यानानंतरची प्रश्नमंजुषा](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/26/)

## पुनरावलोकन आणि स्व-अभ्यास

या धड्यात फक्त अन्न घटकांसाठी शिफारस प्रणाली तयार करण्याच्या उपयुक्ततेचा उल्लेख केला आहे, परंतु ML अनुप्रयोगांच्या या क्षेत्रात अनेक उदाहरणे आहेत. या प्रणाली कशा तयार केल्या जातात याबद्दल अधिक वाचा:

- https://www.sciencedirect.com/topics/computer-science/recommendation-engine
- https://www.technologyreview.com/2014/08/25/171547/the-ultimate-challenge-for-recommendation-engines/
- https://www.technologyreview.com/2015/03/23/168831/everything-is-a-recommendation/

## असाइनमेंट 

[नवीन शिफारस प्रणाली तयार करा](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून निर्माण होणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.