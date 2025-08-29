<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "3c4738bb0836dd838c552ab9cab7e09d",
  "translation_date": "2025-08-29T18:22:42+00:00",
  "source_file": "6-NLP/4-Hotel-Reviews-1/README.md",
  "language_code": "mr"
}
-->
# हॉटेल पुनरावलोकनांसह भावना विश्लेषण - डेटाचे प्रक्रिया करणे

या विभागात तुम्ही मागील धड्यांमधील तंत्रांचा वापर करून मोठ्या डेटासेटचे अन्वेषणात्मक डेटा विश्लेषण कराल. विविध स्तंभांच्या उपयुक्ततेची चांगली समज मिळाल्यानंतर, तुम्ही शिकाल:

- अनावश्यक स्तंभ कसे काढून टाकायचे
- विद्यमान स्तंभांवर आधारित नवीन डेटा कसा मोजायचा
- अंतिम आव्हानासाठी परिणामी डेटासेट कसे जतन करायचे

## [पूर्व-व्याख्यान क्विझ](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/37/)

### परिचय

आतापर्यंत तुम्ही शिकले आहे की मजकूर डेटा संख्यात्मक डेटापेक्षा खूप वेगळा असतो. जर तो माणसाने लिहिलेला किंवा बोललेला मजकूर असेल, तर त्याचे विश्लेषण करून नमुने, वारंवारता, भावना आणि अर्थ शोधता येतो. हा धडा तुम्हाला एका वास्तविक डेटासेटमध्ये घेऊन जातो ज्यामध्ये एक वास्तविक आव्हान आहे: **[युरोपमधील 515K हॉटेल पुनरावलोकन डेटा](https://www.kaggle.com/jiashenliu/515k-hotel-reviews-data-in-europe)**, ज्यामध्ये [CC0: सार्वजनिक डोमेन परवाना](https://creativecommons.org/publicdomain/zero/1.0/) समाविष्ट आहे. हा डेटा Booking.com वरून सार्वजनिक स्त्रोतांमधून गोळा केला गेला आहे. या डेटासेटचे निर्माते जियाशेन लियू आहेत.

### तयारी

तुम्हाला आवश्यक असेल:

* Python 3 वापरून .ipynb नोटबुक चालवण्याची क्षमता
* pandas
* NLTK, [ज्याला तुम्ही स्थानिकरित्या स्थापित करावे](https://www.nltk.org/install.html)
* Kaggle वर उपलब्ध असलेला डेटासेट [युरोपमधील 515K हॉटेल पुनरावलोकन डेटा](https://www.kaggle.com/jiashenliu/515k-hotel-reviews-data-in-europe). हा डेटा अनझिप केल्यानंतर सुमारे 230 MB आहे. तो या NLP धड्यांशी संबंधित `/data` फोल्डरमध्ये डाउनलोड करा.

## अन्वेषणात्मक डेटा विश्लेषण

हे आव्हान गृहीत धरते की तुम्ही भावना विश्लेषण आणि पाहुण्यांच्या पुनरावलोकन गुणांचा वापर करून हॉटेल शिफारस करणारा बॉट तयार करत आहात. तुम्ही वापरणार असलेला डेटासेट 6 शहरांमधील 1493 वेगवेगळ्या हॉटेल्सची पुनरावलोकने समाविष्ट करतो.

Python, हॉटेल पुनरावलोकनांचा डेटासेट आणि NLTK च्या भावना विश्लेषणाचा वापर करून तुम्ही शोधू शकता:

* पुनरावलोकनांमध्ये सर्वाधिक वारंवार वापरले जाणारे शब्द आणि वाक्यांश कोणते आहेत?
* हॉटेलचे अधिकृत *टॅग्स* पुनरावलोकन गुणांशी संबंधित आहेत का (उदा. *लहान मुलांसह कुटुंब* या टॅगसाठी एखाद्या विशिष्ट हॉटेलसाठी अधिक नकारात्मक पुनरावलोकने आहेत का, जे कदाचित *एकट्या प्रवाशांसाठी* चांगले असल्याचे दर्शवते)?
* NLTK भावना गुण पुनरावलोकनकर्त्याच्या संख्यात्मक गुणांशी 'सहमत' आहेत का?

#### डेटासेट

तुम्ही डाउनलोड केलेला आणि स्थानिकरित्या जतन केलेला डेटासेट अन्वेषण करूया. फाईल VS Code किंवा Excel सारख्या संपादकात उघडा.

डेटासेटमधील हेडर्स खालीलप्रमाणे आहेत:

*Hotel_Address, Additional_Number_of_Scoring, Review_Date, Average_Score, Hotel_Name, Reviewer_Nationality, Negative_Review, Review_Total_Negative_Word_Counts, Total_Number_of_Reviews, Positive_Review, Review_Total_Positive_Word_Counts, Total_Number_of_Reviews_Reviewer_Has_Given, Reviewer_Score, Tags, days_since_review, lat, lng*

ते अशा प्रकारे गटबद्ध केले गेले आहेत जेणेकरून तपासणे सोपे होईल:
##### हॉटेल स्तंभ

* `Hotel_Name`, `Hotel_Address`, `lat` (अक्षांश), `lng` (रेखांश)
  * *lat* आणि *lng* चा वापर करून तुम्ही हॉटेल स्थानांचे नकाशे तयार करू शकता (कदाचित नकारात्मक आणि सकारात्मक पुनरावलोकनांसाठी रंग कोडिंगसह)
  * Hotel_Address आपल्यासाठी स्पष्टपणे उपयुक्त नाही आणि आम्ही सोप्या क्रमवारी आणि शोधासाठी देशाने ते बदलू शकतो

**हॉटेल मेटा-पुनरावलोकन स्तंभ**

* `Average_Score`
  * डेटासेट निर्मात्याच्या मते, हा स्तंभ *हॉटेलचा सरासरी गुण आहे, जो गेल्या वर्षातील नवीनतम टिप्पण्यांवर आधारित आहे*. हा गुण मोजण्याचा एक असामान्य मार्ग वाटतो, परंतु सध्या आपण तो जसा आहे तसा स्वीकारू शकतो.

  ✅ या डेटामधील इतर स्तंभांवर आधारित, सरासरी गुण मोजण्याचा आणखी कोणता मार्ग तुम्हाला सुचतो का?

* `Total_Number_of_Reviews`
  * या हॉटेलला मिळालेल्या पुनरावलोकनांची एकूण संख्या - हे स्पष्ट नाही (थोडा कोड लिहिल्याशिवाय) की हे डेटासेटमधील पुनरावलोकनांना संदर्भित करते का.
* `Additional_Number_of_Scoring`
  * याचा अर्थ पुनरावलोकन गुण दिला गेला आहे परंतु पुनरावलोकनकर्त्याने कोणतेही सकारात्मक किंवा नकारात्मक पुनरावलोकन लिहिलेले नाही

**पुनरावलोकन स्तंभ**

- `Reviewer_Score`
  - हा एक संख्यात्मक मूल्य आहे ज्यामध्ये किमान 1 दशांश स्थान आहे, ज्याची किमान आणि जास्तीत जास्त मूल्ये 2.5 आणि 10 आहेत
  - 2.5 हे किमान गुण का आहेत हे स्पष्ट केलेले नाही
- `Negative_Review`
  - जर पुनरावलोकनकर्त्याने काहीही लिहिले नाही, तर या फील्डमध्ये "**No Negative**" असेल
  - लक्षात घ्या की पुनरावलोकनकर्ता नकारात्मक पुनरावलोकन स्तंभात सकारात्मक पुनरावलोकन लिहू शकतो (उदा. "या हॉटेलबद्दल काहीही वाईट नाही")
- `Review_Total_Negative_Word_Counts`
  - जास्त नकारात्मक शब्द संख्या कमी गुण दर्शवते (भावनात्मकता तपासल्याशिवाय)
- `Positive_Review`
  - जर पुनरावलोकनकर्त्याने काहीही लिहिले नाही, तर या फील्डमध्ये "**No Positive**" असेल
  - लक्षात घ्या की पुनरावलोकनकर्ता सकारात्मक पुनरावलोकन स्तंभात नकारात्मक पुनरावलोकन लिहू शकतो (उदा. "या हॉटेलबद्दल काहीही चांगले नाही")
- `Review_Total_Positive_Word_Counts`
  - जास्त सकारात्मक शब्द संख्या जास्त गुण दर्शवते (भावनात्मकता तपासल्याशिवाय)
- `Review_Date` आणि `days_since_review`
  - पुनरावलोकनासाठी ताजेपणा किंवा जुनेपणा लागू केला जाऊ शकतो (जुनी पुनरावलोकने नवीन पुनरावलोकनांइतकी अचूक नसू शकतात कारण हॉटेल व्यवस्थापन बदलले आहे, नूतनीकरण केले गेले आहे किंवा पूल जोडला गेला आहे इ.)
- `Tags`
  - हे लहान वर्णन आहेत जे पुनरावलोकनकर्ता निवडू शकतो, जसे की ते कोणत्या प्रकारचे पाहुणे होते (उदा. एकटे किंवा कुटुंब), त्यांना कोणत्या प्रकारची खोली मिळाली, त्यांचा मुक्काम किती दिवसांचा होता आणि पुनरावलोकन कसे सबमिट केले गेले. 
  - दुर्दैवाने, या टॅग्सचा वापर करणे समस्याप्रधान आहे, खाली त्यांच्या उपयुक्ततेवर चर्चा करणारा विभाग तपासा

**पुनरावलोकनकर्ता स्तंभ**

- `Total_Number_of_Reviews_Reviewer_Has_Given`
  - हे शिफारस मॉडेलमध्ये एक घटक असू शकतो, उदाहरणार्थ, जर तुम्ही ठरवू शकला की शंभराहून अधिक पुनरावलोकने असलेले अधिक पुनरावलोकनकर्ते नकारात्मक होण्याची शक्यता जास्त आहे. तथापि, कोणत्याही विशिष्ट पुनरावलोकनाचा पुनरावलोकनकर्ता अद्वितीय कोडसह ओळखला जात नाही आणि म्हणूनच पुनरावलोकनांच्या संचाशी जोडला जाऊ शकत नाही. 30 पुनरावलोकनकर्त्यांकडे 100 किंवा अधिक पुनरावलोकने आहेत, परंतु हे शिफारस मॉडेलसाठी कसे उपयुक्त ठरू शकते हे पाहणे कठीण आहे.
- `Reviewer_Nationality`
  - काही लोकांना असे वाटू शकते की विशिष्ट राष्ट्रीयत्व सकारात्मक किंवा नकारात्मक पुनरावलोकन देण्याची अधिक शक्यता आहे. अशा अनुभवांवर आधारित मॉडेल तयार करताना सावधगिरी बाळगा. हे राष्ट्रीय (आणि कधीकधी वांशिक) रूढी आहेत, आणि प्रत्येक पुनरावलोकनकर्ता हा एक व्यक्ती होता ज्याने त्यांच्या अनुभवावर आधारित पुनरावलोकन लिहिले. त्यांचे पुनरावलोकन त्यांच्या मागील हॉटेल मुक्काम, प्रवासाचा अंतर, आणि त्यांच्या वैयक्तिक स्वभाव यासारख्या अनेक घटकांमधून फिल्टर केले गेले असू शकते. त्यांच्या राष्ट्रीयत्वामुळे पुनरावलोकन गुण मिळाले असे मानणे कठीण आहे.

##### उदाहरणे

| Average  Score | Total Number   Reviews | Reviewer   Score | Negative <br />Review                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Positive   Review                 | Tags                                                                                      |
| -------------- | ---------------------- | ---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- | ----------------------------------------------------------------------------------------- |
| 7.8            | 1945                   | 2.5              | हे सध्या हॉटेल नाही तर बांधकाम साइट आहे. मला सकाळी लवकर आणि दिवसभर असह्य बांधकामाच्या आवाजाने त्रास झाला. मी खोली बदलण्याची विनंती केली, परंतु शांत खोली उपलब्ध नव्हती. परिस्थिती आणखी वाईट करण्यासाठी, माझ्याकडून जास्त शुल्क आकारले गेले. मी संध्याकाळी चेक आउट केले आणि योग्य बिल मिळाले. दुसऱ्या दिवशी, हॉटेलने माझ्या संमतीशिवाय जास्त शुल्क आकारले. हे एक भयंकर ठिकाण आहे. येथे बुकिंग करून स्वतःला शिक्षा करू नका. | काहीही नाही. भयंकर ठिकाण. दूर रहा. | व्यवसाय प्रवास, जोडपे, स्टँडर्ड डबल रूम, 2 रात्री मुक्काम |

जसे तुम्ही पाहू शकता, या पाहुण्याचा हॉटेलमध्ये मुक्काम आनंददायक नव्हता. हॉटेलला 7.8 चा चांगला सरासरी गुण आणि 1945 पुनरावलोकने आहेत, परंतु या पुनरावलोकनकर्त्याने 2.5 गुण दिले आणि त्यांच्या नकारात्मक अनुभवाबद्दल 115 शब्द लिहिले. जर त्यांनी सकारात्मक पुनरावलोकन स्तंभात काहीही लिहिले नसते, तर तुम्ही गृहीत धरू शकता की काहीही सकारात्मक नव्हते, परंतु त्यांनी 7 शब्द लिहून इशारा दिला. जर आपण शब्दांची फक्त मोजणी केली, तर पुनरावलोकनकर्त्याच्या हेतूचा चुकीचा अर्थ लागू शकतो. आश्चर्यकारकपणे, त्यांचा 2.5 चा गुण गोंधळात टाकणारा आहे, कारण जर हॉटेलचा अनुभव इतका वाईट असेल, तर त्यांनी काही गुण का दिले? डेटासेटचे बारकाईने निरीक्षण केल्यास, तुम्हाला दिसेल की किमान गुण 2.5 आहेत, 0 नाही. जास्तीत जास्त गुण 10 आहेत.

##### टॅग्स

वर नमूद केल्याप्रमाणे, प्रथमदर्शनी, डेटाचे वर्गीकरण करण्यासाठी `Tags` वापरण्याची कल्पना योग्य वाटते. दुर्दैवाने, हे टॅग्स प्रमाणित नाहीत, म्हणजे एका हॉटेलमध्ये पर्याय *सिंगल रूम*, *ट्विन रूम*, आणि *डबल रूम* असू शकतात, तर दुसऱ्या हॉटेलमध्ये ते *डिलक्स सिंगल रूम*, *क्लासिक क्वीन रूम*, आणि *एक्झिक्युटिव्ह किंग रूम* असू शकतात. हे कदाचित समान असतील, परंतु इतक्या विविधता आहेत की निवड अशी होते:

1. सर्व अटी एका मानकात बदलण्याचा प्रयत्न करा, जे खूप कठीण आहे, कारण प्रत्येक प्रकरणात रूपांतरण मार्ग स्पष्ट नाही (उदा. *क्लासिक सिंगल रूम* ला *सिंगल रूम* मध्ये नकाशा तयार करणे सोपे आहे, परंतु *सुपीरियर क्वीन रूम विथ कोर्टयार्ड गार्डन ऑर सिटी व्ह्यू* हे नकाशा तयार करणे खूप कठीण आहे)

1. NLP दृष्टिकोन स्वीकारा आणि *सोलो*, *बिझनेस ट्रॅव्हलर*, किंवा *लहान मुलांसह कुटुंब* यासारख्या विशिष्ट अटींच्या वारंवारतेचे मोजमाप करा आणि ते शिफारस मॉडेलमध्ये समाविष्ट करा  

टॅग्स सहसा (पण नेहमीच नाहीत) एकाच फील्डमध्ये 5 ते 6 अल्पविरामाने विभक्त मूल्यांची यादी असते, जी *प्रवासाचा प्रकार*, *पाहुण्यांचा प्रकार*, *खोलीचा प्रकार*, *रात्रींची संख्या*, आणि *पुनरावलोकन सबमिट करण्यासाठी वापरलेले डिव्हाइस* यांना संरेखित करते. तथापि, काही पुनरावलोकनकर्ते प्रत्येक फील्ड भरत नाहीत (ते एक रिकामे ठेवू शकतात), त्यामुळे मूल्ये नेहमीच एका क्रमाने नसतात.

उदाहरणार्थ, *गटाचा प्रकार* घ्या. `Tags` स्तंभातील या फील्डमध्ये 1025 अद्वितीय शक्यता आहेत, आणि दुर्दैवाने त्यापैकी काहीच गटाचा संदर्भ देतात (काही खोलीच्या प्रकाराशी संबंधित आहेत). जर तुम्ही फक्त कुटुंबाचा उल्लेख करणारे फिल्टर केले, तर परिणामांमध्ये अनेक *फॅमिली रूम* प्रकारचे परिणाम असतात. जर तुम्ही *with* हा शब्द समाविष्ट केला, म्हणजे *फॅमिली विथ* मूल्यांची मोजणी केली, तर परिणाम चांगले होतात, 515,000 परिणामांपैकी 80,000 हून अधिक परिणाम "लहान मुलांसह कुटुंब" किंवा "मोठ्या मुलांसह कुटुंब" या वाक्यांशांचा समावेश करतात.

याचा अर्थ टॅग्स स्तंभ आपल्यासाठी पूर्णपणे निरुपयोगी नाही, परंतु तो उपयुक्त बनवण्यासाठी थोडे काम करावे लागेल.

##### हॉटेलचा सरासरी गुण

डेटासेटमध्ये काही विचित्रता किंवा विसंगती आहेत ज्या मला समजत नाहीत, परंतु त्या येथे स्पष्ट केल्या आहेत जेणेकरून तुम्ही तुमची मॉडेल तयार करताना त्यांची जाणीव ठेवाल. जर तुम्ही त्याचा उलगडा केला, तर कृपया चर्चेच्या विभागात आम्हाला कळवा!

डेटासेटमध्ये सरासरी गुण आणि पुनरावलोकनांच्या संख्येशी संबंधित खालील स्तंभ आहेत:

1. Hotel_Name
2. Additional_Number_of_Scoring
3. Average_Score
4. Total_Number_of_Reviews
5. Reviewer_Score  

या डेटासेटमधील सर्वाधिक पुनरावलोकन असलेले एकमेव हॉटेल *ब्रिटानिया इंटरनॅशनल हॉटेल कॅनरी व्हार्फ* आहे, ज्यामध्ये 515,000 पैकी 4789 पुनरावलोकने आहेत. परंतु जर आपण या हॉटेलसाठी `Total_Number_of_Reviews` मूल्य पाहिले, तर ते 9086 आहे. तुम्ही गृहीत धरू शकता की अनेक गुण पुनरावलोकनांशिवाय आहेत, त्यामुळे कदाचित आपण `Additional_Number_of_Scoring` स्तंभ मूल्य जोडावे. ते मूल्य 2682 आहे, आणि 4789 मध्ये जोडल्यास 7,471 मिळते, जे `Total_Number_of_Reviews` पेक्षा 1615 कमी आहे.

जर तुम्ही `Average_Score` स्तंभ घेतला, तर तुम्ही गृहीत धरू शकता की तो डेटासेटमधील पुनरावलोकनांच्या सरासरीचा आहे, परंतु Kaggle वरील वर्णन आहे "*हॉटेलचा सरासरी गुण, जो गेल्या वर्षातील नवीनतम टिप्पण्यांवर आधारित आहे*". हे फारसे उपयुक्त वाटत नाही, परंतु आपण डेटासेटमधील पुनरावलोकन गुणांवर आधारित आपली स्वतःची सरासरी मोजू शकतो. त्याच हॉटेलचा एक उदाहरण म्हणून विचार केल्यास, हॉटेलचा सरासरी गुण 7.1 दिला आहे, परंतु डेटासेटमधील (पुनरावलोकनकर्त्याच्या गुणांवर आधारित) मोजलेला गुण 6.8 आहे. हे जवळपास आहे, परंतु समान मूल्य नाही, आणि आपण फक्त गृहीत धरू शकतो की `Additional_Number_of_Scoring` पुनरावलोकनांमध्ये दिलेल्या गुणांनी सरासरी 7.1 पर्यंत वाढ
या हॉटेल्सचा डेटा काही प्रमाणात अपवादात्मक असू शकतो, आणि बहुतेक मूल्ये जुळत असतील (पण काही कारणास्तव काही जुळत नाहीत), म्हणून आम्ही पुढे एक छोटा प्रोग्राम लिहिणार आहोत जो डेटासेटमधील मूल्ये तपासेल आणि योग्य वापर (किंवा गैरवापर) निश्चित करेल.

> 🚨 एक महत्त्वाची सूचना
>
> या डेटासेटवर काम करताना तुम्ही कोड लिहाल जो मजकुरातून काहीतरी मोजेल, स्वतः मजकूर वाचण्याची किंवा विश्लेषण करण्याची गरज नसेल. हे NLP चे सार आहे, मानवी हस्तक्षेपाशिवाय अर्थ किंवा भावना समजून घेणे. मात्र, काही नकारात्मक पुनरावलोकने वाचण्याची शक्यता आहे. मी तुम्हाला ते वाचू नका असे सुचवतो, कारण त्याची गरज नाही. काही पुनरावलोकने मूर्खपणाची किंवा अप्रासंगिक असू शकतात, जसे की "हवामान चांगले नव्हते", जे हॉटेलच्या किंवा कोणाच्याही नियंत्रणाबाहेर आहे. पण काही पुनरावलोकनांमध्ये गडद बाजू असते. कधी कधी नकारात्मक पुनरावलोकने वांशिक, लैंगिक किंवा वयावर आधारित असतात. हे दुर्दैवी आहे पण सार्वजनिक वेबसाइटवरून स्क्रॅप केलेल्या डेटासेटमध्ये अपेक्षित आहे. काही पुनरावलोकक असे पुनरावलोकने देतात जी तुम्हाला अप्रिय, अस्वस्थ किंवा त्रासदायक वाटू शकतात. कोडला भावना मोजू द्या, स्वतः वाचून त्रास होऊ नये. असे म्हणता येईल की अशा गोष्टी लिहिणारे अल्पसंख्याक आहेत, पण ते अस्तित्वात आहेत.

## व्यायाम - डेटा अन्वेषण
### डेटा लोड करा

डेटा व्हिज्युअली तपासणे पुरेसे झाले, आता तुम्ही काही कोड लिहाल आणि उत्तर मिळवाल! या विभागात pandas लायब्ररीचा वापर केला जातो. तुमचे पहिले काम म्हणजे CSV डेटा लोड आणि वाचण्याची खात्री करणे. pandas लायब्ररीकडे एक जलद CSV लोडर आहे, आणि परिणाम एका dataframe मध्ये ठेवला जातो, जसे मागील धड्यांमध्ये पाहिले आहे. आपण लोड करत असलेला CSV अर्धा मिलियन ओळींचा आहे, पण फक्त 17 स्तंभ आहेत. pandas तुम्हाला dataframe सह संवाद साधण्यासाठी अनेक शक्तिशाली मार्ग देते, ज्यामध्ये प्रत्येक ओळीवर ऑपरेशन्स करण्याची क्षमता आहे.

या धड्याच्या पुढील भागात कोडचे तुकडे आणि कोडचे स्पष्टीकरण तसेच परिणामांचा अर्थ काय आहे यावर चर्चा असेल. तुमच्या कोडसाठी समाविष्ट _notebook.ipynb_ वापरा.

चला डेटा फाइल लोड करण्यापासून सुरुवात करूया:

```python
# Load the hotel reviews from CSV
import pandas as pd
import time
# importing time so the start and end time can be used to calculate file loading time
print("Loading data file now, this could take a while depending on file size")
start = time.time()
# df is 'DataFrame' - make sure you downloaded the file to the data folder
df = pd.read_csv('../../data/Hotel_Reviews.csv')
end = time.time()
print("Loading took " + str(round(end - start, 2)) + " seconds")
```

आता डेटा लोड झाला आहे, आपण त्यावर काही ऑपरेशन्स करू शकतो. पुढील भागासाठी तुमच्या प्रोग्रामच्या शीर्षस्थानी हा कोड ठेवा.

## डेटा अन्वेषण

या प्रकरणात, डेटा आधीच *स्वच्छ* आहे, म्हणजे तो काम करण्यासाठी तयार आहे आणि त्यात इतर भाषांतील वर्ण नाहीत जे फक्त इंग्रजी वर्ण अपेक्षित असलेल्या अल्गोरिदममध्ये अडथळा आणू शकतात.

✅ तुम्हाला कदाचित अशा डेटासह काम करावे लागेल ज्याला NLP तंत्र लागू करण्यापूर्वी प्रारंभिक प्रक्रिया आवश्यक आहे, पण या वेळेस नाही. जर तुम्हाला करावे लागले, तर तुम्ही गैर-इंग्रजी वर्ण कसे हाताळाल?

एक क्षण घ्या आणि खात्री करा की डेटा लोड झाल्यानंतर तुम्ही कोडसह त्याचा अन्वेषण करू शकता. `Negative_Review` आणि `Positive_Review` स्तंभांवर लक्ष केंद्रित करणे सोपे आहे. ते नैसर्गिक मजकुराने भरलेले आहेत जे तुमच्या NLP अल्गोरिदमसाठी प्रक्रिया करण्यासाठी तयार आहेत. पण थांबा! NLP आणि भावना विश्लेषणात उडी मारण्यापूर्वी, खालील कोडचे अनुसरण करा आणि डेटासेटमध्ये दिलेली मूल्ये pandas सह तुम्ही मोजलेली मूल्ये जुळतात का ते तपासा.

## डेटा फ्रेम ऑपरेशन्स

या धड्याचे पहिले काम म्हणजे खालील दावे योग्य आहेत का हे तपासण्यासाठी कोड लिहिणे जे डेटा फ्रेम तपासेल (त्यात बदल न करता).

> अनेक प्रोग्रामिंग कामांप्रमाणे, हे पूर्ण करण्याचे अनेक मार्ग आहेत, पण चांगला सल्ला म्हणजे ते शक्य तितक्या सोप्या, सोप्या पद्धतीने करा, विशेषतः जर तुम्हाला भविष्यात या कोडकडे परत येणे सोपे होईल. डेटा फ्रेमसाठी, एक व्यापक API आहे जो तुम्हाला हवे ते कार्यक्षमतेने करण्याचा मार्ग देईल.

खालील प्रश्नांना कोडिंग काम म्हणून घ्या आणि उत्तर शोधण्याचा प्रयत्न करा, समाधान न पाहता.

1. तुम्ही नुकतेच लोड केलेल्या डेटा फ्रेमचे *आकार* प्रिंट करा (आकार म्हणजे ओळी आणि स्तंभांची संख्या)
2. पुनरावलोककांच्या राष्ट्रीयतेसाठी वारंवारता मोजा:
   1. `Reviewer_Nationality` स्तंभासाठी किती वेगळ्या मूल्ये आहेत आणि ती कोणती आहेत?
   2. डेटासेटमध्ये सर्वात सामान्य पुनरावलोकक राष्ट्रीयता कोणती आहे (देश आणि पुनरावलोकनांची संख्या प्रिंट करा)?
   3. पुढील 10 सर्वाधिक वारंवार आढळणाऱ्या राष्ट्रीयता कोणत्या आहेत आणि त्यांची वारंवारता मोजा?
3. प्रत्येक टॉप 10 पुनरावलोकक राष्ट्रीयतेसाठी सर्वाधिक पुनरावलोकन केलेले हॉटेल कोणते होते?
4. डेटासेटमध्ये प्रत्येक हॉटेलसाठी किती पुनरावलोकने आहेत (हॉटेलची वारंवारता मोजा)?
5. डेटासेटमधील प्रत्येक हॉटेलसाठी पुनरावलोकक स्कोअरचे सरासरी मिळवून सरासरी स्कोअर काढता येतो. तुमच्या डेटा फ्रेममध्ये `Calc_Average_Score` नावाचा नवीन स्तंभ जोडा ज्यामध्ये ती गणना केलेली सरासरी असेल.
6. कोणत्याही हॉटेल्समध्ये (1 दशांश स्थानावर गोल केलेले) `Average_Score` आणि `Calc_Average_Score` समान आहेत का?
   1. एक Python फंक्शन लिहिण्याचा प्रयत्न करा जे Series (ओळ) तर्क म्हणून घेते आणि मूल्ये समान नसल्यास संदेश प्रिंट करते. नंतर `.apply()` पद्धत वापरून प्रत्येक ओळ प्रक्रिया करा.
7. `Negative_Review` स्तंभात "No Negative" मूल्य असलेल्या किती ओळी आहेत ते मोजा आणि प्रिंट करा.
8. `Positive_Review` स्तंभात "No Positive" मूल्य असलेल्या किती ओळी आहेत ते मोजा आणि प्रिंट करा.
9. `Positive_Review` स्तंभात "No Positive" **आणि** `Negative_Review` स्तंभात "No Negative" मूल्य असलेल्या किती ओळी आहेत ते मोजा आणि प्रिंट करा.

### कोड उत्तर

1. तुम्ही नुकतेच लोड केलेल्या डेटा फ्रेमचे *आकार* प्रिंट करा (आकार म्हणजे ओळी आणि स्तंभांची संख्या)

   ```python
   print("The shape of the data (rows, cols) is " + str(df.shape))
   > The shape of the data (rows, cols) is (515738, 17)
   ```

2. पुनरावलोककांच्या राष्ट्रीयतेसाठी वारंवारता मोजा:

   1. `Reviewer_Nationality` स्तंभासाठी किती वेगळ्या मूल्ये आहेत आणि ती कोणती आहेत?
   2. डेटासेटमध्ये सर्वात सामान्य पुनरावलोकक राष्ट्रीयता कोणती आहे (देश आणि पुनरावलोकनांची संख्या प्रिंट करा)?

   ```python
   # value_counts() creates a Series object that has index and values in this case, the country and the frequency they occur in reviewer nationality
   nationality_freq = df["Reviewer_Nationality"].value_counts()
   print("There are " + str(nationality_freq.size) + " different nationalities")
   # print first and last rows of the Series. Change to nationality_freq.to_string() to print all of the data
   print(nationality_freq) 
   
   There are 227 different nationalities
    United Kingdom               245246
    United States of America      35437
    Australia                     21686
    Ireland                       14827
    United Arab Emirates          10235
                                  ...  
    Comoros                           1
    Palau                             1
    Northern Mariana Islands          1
    Cape Verde                        1
    Guinea                            1
   Name: Reviewer_Nationality, Length: 227, dtype: int64
   ```

   3. पुढील 10 सर्वाधिक वारंवार आढळणाऱ्या राष्ट्रीयता कोणत्या आहेत आणि त्यांची वारंवारता मोजा?

      ```python
      print("The highest frequency reviewer nationality is " + str(nationality_freq.index[0]).strip() + " with " + str(nationality_freq[0]) + " reviews.")
      # Notice there is a leading space on the values, strip() removes that for printing
      # What is the top 10 most common nationalities and their frequencies?
      print("The next 10 highest frequency reviewer nationalities are:")
      print(nationality_freq[1:11].to_string())
      
      The highest frequency reviewer nationality is United Kingdom with 245246 reviews.
      The next 10 highest frequency reviewer nationalities are:
       United States of America     35437
       Australia                    21686
       Ireland                      14827
       United Arab Emirates         10235
       Saudi Arabia                  8951
       Netherlands                   8772
       Switzerland                   8678
       Germany                       7941
       Canada                        7894
       France                        7296
      ```

3. प्रत्येक टॉप 10 पुनरावलोकक राष्ट्रीयतेसाठी सर्वाधिक पुनरावलोकन केलेले हॉटेल कोणते होते?

   ```python
   # What was the most frequently reviewed hotel for the top 10 nationalities
   # Normally with pandas you will avoid an explicit loop, but wanted to show creating a new dataframe using criteria (don't do this with large amounts of data because it could be very slow)
   for nat in nationality_freq[:10].index:
      # First, extract all the rows that match the criteria into a new dataframe
      nat_df = df[df["Reviewer_Nationality"] == nat]   
      # Now get the hotel freq
      freq = nat_df["Hotel_Name"].value_counts()
      print("The most reviewed hotel for " + str(nat).strip() + " was " + str(freq.index[0]) + " with " + str(freq[0]) + " reviews.") 
      
   The most reviewed hotel for United Kingdom was Britannia International Hotel Canary Wharf with 3833 reviews.
   The most reviewed hotel for United States of America was Hotel Esther a with 423 reviews.
   The most reviewed hotel for Australia was Park Plaza Westminster Bridge London with 167 reviews.
   The most reviewed hotel for Ireland was Copthorne Tara Hotel London Kensington with 239 reviews.
   The most reviewed hotel for United Arab Emirates was Millennium Hotel London Knightsbridge with 129 reviews.
   The most reviewed hotel for Saudi Arabia was The Cumberland A Guoman Hotel with 142 reviews.
   The most reviewed hotel for Netherlands was Jaz Amsterdam with 97 reviews.
   The most reviewed hotel for Switzerland was Hotel Da Vinci with 97 reviews.
   The most reviewed hotel for Germany was Hotel Da Vinci with 86 reviews.
   The most reviewed hotel for Canada was St James Court A Taj Hotel London with 61 reviews.
   ```

4. डेटासेटमध्ये प्रत्येक हॉटेलसाठी किती पुनरावलोकने आहेत (हॉटेलची वारंवारता मोजा)?

   ```python
   # First create a new dataframe based on the old one, removing the uneeded columns
   hotel_freq_df = df.drop(["Hotel_Address", "Additional_Number_of_Scoring", "Review_Date", "Average_Score", "Reviewer_Nationality", "Negative_Review", "Review_Total_Negative_Word_Counts", "Positive_Review", "Review_Total_Positive_Word_Counts", "Total_Number_of_Reviews_Reviewer_Has_Given", "Reviewer_Score", "Tags", "days_since_review", "lat", "lng"], axis = 1)
   
   # Group the rows by Hotel_Name, count them and put the result in a new column Total_Reviews_Found
   hotel_freq_df['Total_Reviews_Found'] = hotel_freq_df.groupby('Hotel_Name').transform('count')
   
   # Get rid of all the duplicated rows
   hotel_freq_df = hotel_freq_df.drop_duplicates(subset = ["Hotel_Name"])
   display(hotel_freq_df) 
   ```
   |                 Hotel_Name                 | Total_Number_of_Reviews | Total_Reviews_Found |
   | :----------------------------------------: | :---------------------: | :-----------------: |
   | Britannia International Hotel Canary Wharf |          9086           |        4789         |
   |    Park Plaza Westminster Bridge London    |          12158          |        4169         |
   |   Copthorne Tara Hotel London Kensington   |          7105           |        3578         |
   |                    ...                     |           ...           |         ...         |
   |       Mercure Paris Porte d Orleans        |           110           |         10          |
   |                Hotel Wagner                |           135           |         10          |
   |            Hotel Gallitzinberg             |           173           |          8          |
   
   तुम्हाला कदाचित *डेटासेटमध्ये मोजलेले* परिणाम `Total_Number_of_Reviews` मूल्याशी जुळत नाहीत असे दिसेल. डेटासेटमधील हे मूल्य हॉटेलला मिळालेल्या पुनरावलोकनांची एकूण संख्या दर्शवते, पण सर्व स्क्रॅप केलेली नाहीत, किंवा काही अन्य गणना. `Total_Number_of_Reviews` मॉडेलमध्ये वापरले जात नाही कारण याबाबत स्पष्टता नाही.

5. डेटासेटमधील प्रत्येक हॉटेलसाठी पुनरावलोकक स्कोअरचे सरासरी मिळवून सरासरी स्कोअर काढता येतो. तुमच्या डेटा फ्रेममध्ये `Calc_Average_Score` नावाचा नवीन स्तंभ जोडा ज्यामध्ये ती गणना केलेली सरासरी असेल. `Hotel_Name`, `Average_Score`, आणि `Calc_Average_Score` स्तंभ प्रिंट करा.

   ```python
   # define a function that takes a row and performs some calculation with it
   def get_difference_review_avg(row):
     return row["Average_Score"] - row["Calc_Average_Score"]
   
   # 'mean' is mathematical word for 'average'
   df['Calc_Average_Score'] = round(df.groupby('Hotel_Name').Reviewer_Score.transform('mean'), 1)
   
   # Add a new column with the difference between the two average scores
   df["Average_Score_Difference"] = df.apply(get_difference_review_avg, axis = 1)
   
   # Create a df without all the duplicates of Hotel_Name (so only 1 row per hotel)
   review_scores_df = df.drop_duplicates(subset = ["Hotel_Name"])
   
   # Sort the dataframe to find the lowest and highest average score difference
   review_scores_df = review_scores_df.sort_values(by=["Average_Score_Difference"])
   
   display(review_scores_df[["Average_Score_Difference", "Average_Score", "Calc_Average_Score", "Hotel_Name"]])
   ```

   तुम्हाला कदाचित `Average_Score` मूल्य आणि गणना केलेल्या सरासरी स्कोअरबाबत आश्चर्य वाटेल आणि ते कधी कधी वेगळे का असते. काही मूल्ये जुळतात, पण इतरांमध्ये फरक का आहे हे आम्हाला माहित नसल्यामुळे, या प्रकरणात सुरक्षिततेसाठी आम्ही पुनरावलोकन स्कोअर वापरून स्वतः सरासरी काढू. असे म्हणता येईल की फरक सहसा खूप लहान असतो, येथे डेटासेट सरासरी आणि गणना केलेल्या सरासरीमधील सर्वाधिक विचलन असलेली हॉटेल्स आहेत:

   | Average_Score_Difference | Average_Score | Calc_Average_Score |                                  Hotel_Name |
   | :----------------------: | :-----------: | :----------------: | ------------------------------------------: |
   |           -0.8           |      7.7      |        8.5         |                  Best Western Hotel Astoria |
   |           -0.7           |      8.8      |        9.5         | Hotel Stendhal Place Vend me Paris MGallery |
   |           -0.7           |      7.5      |        8.2         |               Mercure Paris Porte d Orleans |
   |           -0.7           |      7.9      |        8.6         |             Renaissance Paris Vendome Hotel |
   |           -0.5           |      7.0      |        7.5         |                         Hotel Royal Elys es |
   |           ...            |      ...      |        ...         |                                         ... |
   |           0.7            |      7.5      |        6.8         |     Mercure Paris Op ra Faubourg Montmartre |
   |           0.8            |      7.1      |        6.3         |      Holiday Inn Paris Montparnasse Pasteur |
   |           0.9            |      6.8      |        5.9         |                               Villa Eugenie |
   |           0.9            |      8.6      |        7.7         |   MARQUIS Faubourg St Honor Relais Ch teaux |
   |           1.3            |      7.2      |        5.9         |                          Kube Hotel Ice Bar |

   फक्त 1 हॉटेलमध्ये स्कोअरचा फरक 1 पेक्षा जास्त आहे, याचा अर्थ आम्ही फरक दुर्लक्षित करू शकतो आणि गणना केलेला सरासरी स्कोअर वापरू शकतो.

6. `Negative_Review` स्तंभात "No Negative" मूल्य असलेल्या किती ओळी आहेत ते मोजा आणि प्रिंट करा.

7. `Positive_Review` स्तंभात "No Positive" मूल्य असलेल्या किती ओळी आहेत ते मोजा आणि प्रिंट करा.

8. `Positive_Review` स्तंभात "No Positive" **आणि** `Negative_Review` स्तंभात "No Negative" मूल्य असलेल्या किती ओळी आहेत ते मोजा आणि प्रिंट करा.

   ```python
   # with lambdas:
   start = time.time()
   no_negative_reviews = df.apply(lambda x: True if x['Negative_Review'] == "No Negative" else False , axis=1)
   print("Number of No Negative reviews: " + str(len(no_negative_reviews[no_negative_reviews == True].index)))
   
   no_positive_reviews = df.apply(lambda x: True if x['Positive_Review'] == "No Positive" else False , axis=1)
   print("Number of No Positive reviews: " + str(len(no_positive_reviews[no_positive_reviews == True].index)))
   
   both_no_reviews = df.apply(lambda x: True if x['Negative_Review'] == "No Negative" and x['Positive_Review'] == "No Positive" else False , axis=1)
   print("Number of both No Negative and No Positive reviews: " + str(len(both_no_reviews[both_no_reviews == True].index)))
   end = time.time()
   print("Lambdas took " + str(round(end - start, 2)) + " seconds")
   
   Number of No Negative reviews: 127890
   Number of No Positive reviews: 35946
   Number of both No Negative and No Positive reviews: 127
   Lambdas took 9.64 seconds
   ```

## दुसरा मार्ग

लॅम्बडाशिवाय आयटम मोजण्याचा दुसरा मार्ग, आणि ओळी मोजण्यासाठी sum वापरा:

   ```python
   # without lambdas (using a mixture of notations to show you can use both)
   start = time.time()
   no_negative_reviews = sum(df.Negative_Review == "No Negative")
   print("Number of No Negative reviews: " + str(no_negative_reviews))
   
   no_positive_reviews = sum(df["Positive_Review"] == "No Positive")
   print("Number of No Positive reviews: " + str(no_positive_reviews))
   
   both_no_reviews = sum((df.Negative_Review == "No Negative") & (df.Positive_Review == "No Positive"))
   print("Number of both No Negative and No Positive reviews: " + str(both_no_reviews))
   
   end = time.time()
   print("Sum took " + str(round(end - start, 2)) + " seconds")
   
   Number of No Negative reviews: 127890
   Number of No Positive reviews: 35946
   Number of both No Negative and No Positive reviews: 127
   Sum took 0.19 seconds
   ```

   तुम्हाला कदाचित लक्षात आले असेल की `Negative_Review` आणि `Positive_Review` स्तंभांमध्ये "No Negative" आणि "No Positive" मूल्य असलेल्या 127 ओळी आहेत. याचा अर्थ पुनरावलोककाने हॉटेलला संख्यात्मक स्कोअर दिला, पण सकारात्मक किंवा नकारात्मक पुनरावलोकन लिहिण्यास नकार दिला. सुदैवाने, ही ओळींची संख्या कमी आहे (127 पैकी 515738, म्हणजे 0.02%), त्यामुळे कदाचित आमच्या मॉडेल किंवा परिणामांवर कोणत्याही विशिष्ट दिशेने प्रभाव पडणार नाही, पण तुम्हाला कदाचित पुनरावलोकन असलेल्या डेटासेटमध्ये पुनरावलोकन नसलेल्या ओळी असतील अशी अपेक्षा नसावी, त्यामुळे अशा ओळी शोधण्यासाठी डेटा अन्वेषण करणे योग्य आहे.

आता तुम्ही डेटासेटचा अन्वेषण केला आहे, पुढील धड्यात तुम्ही डेटा फिल्टर कराल आणि काही भावना विश्लेषण जोडाल.

---
## 🚀चॅलेंज

या धड्याने, जसे मागील धड्यांमध्ये पाहिले, हे दाखवले की तुमच्या डेटाचा आणि त्याच्या त्रुटींचा सखोल अभ्यास करणे किती महत्त्वाचे आहे. मजकूर-आधारित डेटाला विशेषतः काळजीपूर्वक तपासण्याची गरज असते. विविध मजकूर-प्रधान डेटासेटमध्ये खोदून पाहा आणि मॉडेलमध्ये पूर्वग्रह किंवा विकृत भावना आणू शकणाऱ्या क्षेत्रांचा शोध घेण्याचा प्रयत्न करा.

## [पश्चात-व्याख्यान क्विझ](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/38/)

## पुनरावलोकन आणि स्व-अभ्यास

[NLP वरचा हा लर्निंग पथ](https://docs.microsoft.com/learn/paths/explore-natural-language-processing/?WT.mc_id=academic-77952-leestott) घ्या आणि भाषण आणि मजकूर-प्रधान मॉडेल तयार करताना वापरण्यासाठी साधने शोधा.

## असाइनमेंट 

[NLTK](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून निर्माण होणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.