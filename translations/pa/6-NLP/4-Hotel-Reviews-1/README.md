<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "3c4738bb0836dd838c552ab9cab7e09d",
  "translation_date": "2025-08-29T18:27:06+00:00",
  "source_file": "6-NLP/4-Hotel-Reviews-1/README.md",
  "language_code": "pa"
}
-->
# ਹੋਟਲ ਰਿਵਿਊਜ਼ ਨਾਲ ਭਾਵਨਾ ਵਿਸ਼ਲੇਸ਼ਣ - ਡਾਟਾ ਪ੍ਰੋਸੈਸਿੰਗ

ਇਸ ਭਾਗ ਵਿੱਚ ਤੁਸੀਂ ਪਿਛਲੇ ਪਾਠਾਂ ਵਿੱਚ ਸਿੱਖੀਆਂ ਤਕਨੀਕਾਂ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਇੱਕ ਵੱਡੇ ਡਾਟਾਸੈਟ ਦੀ ਖੋਜਾਤਮਕ ਡਾਟਾ ਵਿਸ਼ਲੇਸ਼ਣ ਕਰੋਗੇ। ਜਦੋਂ ਤੁਹਾਨੂੰ ਵੱਖ-ਵੱਖ ਕਾਲਮਾਂ ਦੀ ਉਪਯੋਗਤਾ ਦੀ ਚੰਗੀ ਸਮਝ ਹੋ ਜਾਵੇਗੀ, ਤਾਂ ਤੁਸੀਂ ਸਿੱਖੋਗੇ:

- ਕਿਵੇਂ ਗੈਰ-ਜ਼ਰੂਰੀ ਕਾਲਮਾਂ ਨੂੰ ਹਟਾਉਣਾ ਹੈ
- ਮੌਜੂਦਾ ਕਾਲਮਾਂ ਦੇ ਆਧਾਰ 'ਤੇ ਕੁਝ ਨਵਾਂ ਡਾਟਾ ਕਿਵੇਂ ਗਿਣਨਾ ਹੈ
- ਅੰਤਿਮ ਚੁਣੌਤੀ ਵਿੱਚ ਵਰਤਣ ਲਈ ਨਤੀਜੇ ਵਾਲੇ ਡਾਟਾਸੈਟ ਨੂੰ ਕਿਵੇਂ ਸੇਵ ਕਰਨਾ ਹੈ

## [ਪ੍ਰੀ-ਲੈਕਚਰ ਕਵਿਜ਼](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/37/)

### ਪਰਿਚਯ

ਹੁਣ ਤੱਕ ਤੁਸੀਂ ਸਿੱਖਿਆ ਹੈ ਕਿ ਟੈਕਸਟ ਡਾਟਾ ਗਿਣਤੀ ਵਾਲੇ ਡਾਟਾ ਦੀ ਕਿਸਮਾਂ ਤੋਂ ਕਾਫ਼ੀ ਵੱਖਰਾ ਹੁੰਦਾ ਹੈ। ਜੇ ਇਹ ਟੈਕਸਟ ਕਿਸੇ ਮਨੁੱਖ ਦੁਆਰਾ ਲਿਖਿਆ ਜਾਂ ਬੋਲਾ ਗਿਆ ਹੈ, ਤਾਂ ਇਸ ਦਾ ਵਿਸ਼ਲੇਸ਼ਣ ਕਰਕੇ ਪੈਟਰਨ ਅਤੇ ਆਵ੍ਰਿੱਤੀਆਂ, ਭਾਵਨਾ ਅਤੇ ਅਰਥ ਲੱਭੇ ਜਾ ਸਕਦੇ ਹਨ। ਇਹ ਪਾਠ ਤੁਹਾਨੂੰ ਇੱਕ ਅਸਲ ਡਾਟਾਸੈਟ ਅਤੇ ਇੱਕ ਅਸਲ ਚੁਣੌਤੀ ਵਿੱਚ ਲੈ ਜਾਂਦਾ ਹੈ: **[ਯੂਰਪ ਵਿੱਚ 515K ਹੋਟਲ ਰਿਵਿਊਜ਼ ਡਾਟਾ](https://www.kaggle.com/jiashenliu/515k-hotel-reviews-data-in-europe)**, ਜਿਸ ਵਿੱਚ ਇੱਕ [CC0: ਪਬਲਿਕ ਡੋਮੇਨ ਲਾਇਸੈਂਸ](https://creativecommons.org/publicdomain/zero/1.0/) ਸ਼ਾਮਲ ਹੈ। ਇਹ ਡਾਟਾ Booking.com ਤੋਂ ਜਨਤਕ ਸਰੋਤਾਂ ਤੋਂ ਸਕ੍ਰੈਪ ਕੀਤਾ ਗਿਆ ਸੀ। ਡਾਟਾਸੈਟ ਦੇ ਰਚਨਹਾਰ Jiashen Liu ਹਨ।

### ਤਿਆਰੀ

ਤੁਹਾਨੂੰ ਲੋੜ ਹੋਵੇਗੀ:

* Python 3 ਦੀ ਵਰਤੋਂ ਕਰਕੇ .ipynb ਨੋਟਬੁੱਕ ਚਲਾਉਣ ਦੀ ਸਮਰੱਥਾ
* pandas
* NLTK, [ਜਿਸਨੂੰ ਤੁਹਾਨੂੰ ਸਥਾਨਕ ਤੌਰ 'ਤੇ ਇੰਸਟਾਲ ਕਰਨਾ ਚਾਹੀਦਾ ਹੈ](https://www.nltk.org/install.html)
* ਡਾਟਾਸੈਟ ਜੋ Kaggle 'ਤੇ ਉਪਲਬਧ ਹੈ [ਯੂਰਪ ਵਿੱਚ 515K ਹੋਟਲ ਰਿਵਿਊਜ਼ ਡਾਟਾ](https://www.kaggle.com/jiashenliu/515k-hotel-reviews-data-in-europe)। ਇਹ ਅਨਜ਼ਿਪ ਕਰਨ ਤੋਂ ਬਾਅਦ ਲਗਭਗ 230 MB ਹੈ। ਇਸਨੂੰ `/data` ਫੋਲਡਰ ਵਿੱਚ ਡਾਊਨਲੋਡ ਕਰੋ ਜੋ ਕਿ ਇਹਨਾਂ NLP ਪਾਠਾਂ ਨਾਲ ਸੰਬੰਧਿਤ ਹੈ।

## ਖੋਜਾਤਮਕ ਡਾਟਾ ਵਿਸ਼ਲੇਸ਼ਣ

ਇਹ ਚੁਣੌਤੀ ਇਹ ਮੰਨ ਕੇ ਚਲਦੀ ਹੈ ਕਿ ਤੁਸੀਂ ਭਾਵਨਾ ਵਿਸ਼ਲੇਸ਼ਣ ਅਤੇ ਮਹਿਮਾਨ ਰਿਵਿਊ ਸਕੋਰ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਇੱਕ ਹੋਟਲ ਸਿਫਾਰਸ਼ੀ ਬੋਟ ਬਣਾ ਰਹੇ ਹੋ। ਡਾਟਾਸੈਟ ਜਿਸਦੀ ਤੁਸੀਂ ਵਰਤੋਂ ਕਰ ਰਹੇ ਹੋ, ਇਸ ਵਿੱਚ 6 ਸ਼ਹਿਰਾਂ ਵਿੱਚ 1493 ਵੱਖ-ਵੱਖ ਹੋਟਲਾਂ ਦੇ ਰਿਵਿਊ ਸ਼ਾਮਲ ਹਨ।

Python, ਹੋਟਲ ਰਿਵਿਊਜ਼ ਦੇ ਡਾਟਾਸੈਟ, ਅਤੇ NLTK ਦੀ ਭਾਵਨਾ ਵਿਸ਼ਲੇਸ਼ਣ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਤੁਸੀਂ ਪਤਾ ਲਗਾ ਸਕਦੇ ਹੋ:

* ਰਿਵਿਊਜ਼ ਵਿੱਚ ਸਭ ਤੋਂ ਵੱਧ ਵਰਤੇ ਜਾਣ ਵਾਲੇ ਸ਼ਬਦ ਅਤੇ ਵਾਕਾਂਸ਼ ਕਿਹੜੇ ਹਨ?
* ਕੀ ਹੋਟਲ ਨੂੰ ਵਰਣਨ ਕਰਨ ਵਾਲੇ ਅਧਿਕਾਰਕ *ਟੈਗ* ਰਿਵਿਊ ਸਕੋਰ ਨਾਲ ਸਬੰਧਤ ਹਨ (ਜਿਵੇਂ ਕਿ ਕੀ ਕਿਸੇ ਖਾਸ ਹੋਟਲ ਲਈ *Family with young children* ਦੇ ਰਿਵਿਊ *Solo traveller* ਦੇ ਰਿਵਿਊ ਨਾਲੋਂ ਜ਼ਿਆਦਾ ਨਕਾਰਾਤਮਕ ਹਨ, ਜੋ ਸ਼ਾਇਦ ਇਹ ਦਰਸਾਉਂਦਾ ਹੈ ਕਿ ਇਹ *Solo travellers* ਲਈ ਬਿਹਤਰ ਹੈ)?
* ਕੀ NLTK ਭਾਵਨਾ ਸਕੋਰ ਹੋਟਲ ਰਿਵਿਊਅਰ ਦੇ ਗਿਣਤੀ ਵਾਲੇ ਸਕੋਰ ਨਾਲ 'ਸਹਿਮਤ' ਹਨ?

#### ਡਾਟਾਸੈਟ

ਆਓ ਡਾਟਾਸੈਟ ਦੀ ਜਾਂਚ ਕਰੀਏ ਜੋ ਤੁਸੀਂ ਡਾਊਨਲੋਡ ਕੀਤਾ ਹੈ ਅਤੇ ਸਥਾਨਕ ਤੌਰ 'ਤੇ ਸੇਵ ਕੀਤਾ ਹੈ। ਫਾਇਲ ਨੂੰ ਕਿਸੇ ਐਡੀਟਰ ਜਿਵੇਂ ਕਿ VS Code ਜਾਂ Excel ਵਿੱਚ ਖੋਲ੍ਹੋ।

ਡਾਟਾਸੈਟ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤੇ ਸਿਰਲੇਖ ਹਨ:

*Hotel_Address, Additional_Number_of_Scoring, Review_Date, Average_Score, Hotel_Name, Reviewer_Nationality, Negative_Review, Review_Total_Negative_Word_Counts, Total_Number_of_Reviews, Positive_Review, Review_Total_Positive_Word_Counts, Total_Number_of_Reviews_Reviewer_Has_Given, Reviewer_Score, Tags, days_since_review, lat, lng*

ਇਹਨਾਂ ਨੂੰ ਹੇਠਾਂ ਦਿੱਤੇ ਤਰੀਕੇ ਨਾਲ ਸਮੂਹਬੱਧ ਕੀਤਾ ਗਿਆ ਹੈ ਜੋ ਸ਼ਾਇਦ ਜਾਂਚਣ ਲਈ ਆਸਾਨ ਹੋਵੇ:  
##### ਹੋਟਲ ਕਾਲਮ

* `Hotel_Name`, `Hotel_Address`, `lat` (ਅਕਸ਼ਾਂਸ), `lng` (ਦੇਸ਼ਾਂਤਰ)
  * `lat` ਅਤੇ `lng` ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਤੁਸੀਂ Python ਨਾਲ ਇੱਕ ਨਕਸ਼ਾ ਬਣਾਉਣ ਦੀ ਯੋਜਨਾ ਬਣਾ ਸਕਦੇ ਹੋ ਜੋ ਹੋਟਲ ਦੇ ਸਥਾਨਾਂ ਨੂੰ ਦਰਸਾਉਂਦਾ ਹੈ (ਸ਼ਾਇਦ ਨਕਾਰਾਤਮਕ ਅਤੇ ਸਕਾਰਾਤਮਕ ਰਿਵਿਊਜ਼ ਲਈ ਵੱਖ-ਵੱਖ ਰੰਗਾਂ ਨਾਲ)
  * `Hotel_Address` ਸਾਡੇ ਲਈ ਸਪਸ਼ਟ ਤੌਰ 'ਤੇ ਉਪਯੋਗ ਨਹੀਂ ਹੈ, ਅਤੇ ਅਸਾਨ ਸਾਰਟਿੰਗ ਅਤੇ ਖੋਜ ਲਈ ਅਸੀਂ ਇਸਨੂੰ ਇੱਕ ਦੇਸ਼ ਨਾਲ ਬਦਲ ਸਕਦੇ ਹਾਂ

**ਹੋਟਲ ਮੈਟਾ-ਰਿਵਿਊ ਕਾਲਮ**

* `Average_Score`
  * ਡਾਟਾਸੈਟ ਦੇ ਰਚਨਹਾਰ ਦੇ ਅਨੁਸਾਰ, ਇਹ ਕਾਲਮ ਹੈ *ਹੋਟਲ ਦਾ ਔਸਤ ਸਕੋਰ, ਜੋ ਪਿਛਲੇ ਸਾਲ ਦੇ ਤਾਜ਼ਾ ਟਿੱਪਣੀ ਦੇ ਆਧਾਰ 'ਤੇ ਗਿਣਿਆ ਗਿਆ ਹੈ*। ਇਹ ਸਕੋਰ ਗਿਣਨ ਦਾ ਇੱਕ ਅਜੀਬ ਤਰੀਕਾ ਲੱਗਦਾ ਹੈ, ਪਰ ਇਹ ਸਕ੍ਰੈਪ ਕੀਤਾ ਡਾਟਾ ਹੈ, ਇਸ ਲਈ ਅਸੀਂ ਇਸਨੂੰ ਫਿਲਹਾਲ ਸੱਚ ਮੰਨ ਸਕਦੇ ਹਾਂ। 
  
  ✅ ਇਸ ਡਾਟੇ ਵਿੱਚ ਹੋਰ ਕਾਲਮਾਂ ਦੇ ਆਧਾਰ 'ਤੇ ਕੀ ਤੁਸੀਂ ਔਸਤ ਸਕੋਰ ਗਿਣਨ ਦਾ ਹੋਰ ਤਰੀਕਾ ਸੋਚ ਸਕਦੇ ਹੋ?

* `Total_Number_of_Reviews`
  * ਇਹ ਹੋਟਲ ਨੂੰ ਮਿਲੇ ਕੁੱਲ ਰਿਵਿਊਜ਼ ਦੀ ਗਿਣਤੀ ਹੈ - ਇਹ ਸਪਸ਼ਟ ਨਹੀਂ ਹੈ (ਕੋਡ ਲਿਖਣ ਤੋਂ ਬਿਨਾਂ) ਕਿ ਕੀ ਇਹ ਡਾਟਾਸੈਟ ਵਿੱਚ ਸ਼ਾਮਲ ਰਿਵਿਊਜ਼ ਨੂੰ ਦਰਸਾਉਂਦਾ ਹੈ।
* `Additional_Number_of_Scoring`
  * ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਰਿਵਿਊ ਸਕੋਰ ਦਿੱਤਾ ਗਿਆ ਸੀ ਪਰ ਰਿਵਿਊਅਰ ਦੁਆਰਾ ਕੋਈ ਸਕਾਰਾਤਮਕ ਜਾਂ ਨਕਾਰਾਤਮਕ ਟਿੱਪਣੀ ਨਹੀਂ ਲਿਖੀ ਗਈ

**ਰਿਵਿਊ ਕਾਲਮ**

- `Reviewer_Score`
  - ਇਹ ਇੱਕ ਗਿਣਤੀਮੂਲਕ ਮੁੱਲ ਹੈ ਜਿਸ ਵਿੱਚ ਘੱਟੋ-ਘੱਟ 1 ਦਸ਼ਮਲਵ ਅੰਕ ਹੁੰਦਾ ਹੈ ਅਤੇ ਇਸਦੀ ਘੱਟ ਤੋਂ ਘੱਟ ਅਤੇ ਵੱਧ ਤੋਂ ਵੱਧ ਕੀਮਤ 2.5 ਅਤੇ 10 ਹੈ
  - ਇਹ ਨਹੀਂ ਸਮਝਾਇਆ ਗਿਆ ਕਿ 2.5 ਘੱਟੋ-ਘੱਟ ਸਕੋਰ ਕਿਉਂ ਹੈ
- `Negative_Review`
  - ਜੇਕਰ ਕਿਸੇ ਰਿਵਿਊਅਰ ਨੇ ਕੁਝ ਨਹੀਂ ਲਿਖਿਆ, ਤਾਂ ਇਸ ਖੇਤਰ ਵਿੱਚ "**No Negative**" ਹੋਵੇਗਾ
  - ਧਿਆਨ ਦਿਓ ਕਿ ਇੱਕ ਰਿਵਿਊਅਰ ਨਕਾਰਾਤਮਕ ਰਿਵਿਊ ਕਾਲਮ ਵਿੱਚ ਸਕਾਰਾਤਮਕ ਟਿੱਪਣੀ ਲਿਖ ਸਕਦਾ ਹੈ (ਜਿਵੇਂ ਕਿ "ਇਸ ਹੋਟਲ ਬਾਰੇ ਕੁਝ ਵੀ ਬੁਰਾ ਨਹੀਂ ਹੈ")
- `Review_Total_Negative_Word_Counts`
  - ਵੱਧ ਨਕਾਰਾਤਮਕ ਸ਼ਬਦ ਗਿਣਤੀ ਘੱਟ ਸਕੋਰ ਦਰਸਾਉਂਦੀ ਹੈ (ਭਾਵਨਾ ਦੀ ਜਾਂਚ ਕੀਤੇ ਬਿਨਾਂ)
- `Positive_Review`
  - ਜੇਕਰ ਕਿਸੇ ਰਿਵਿਊਅਰ ਨੇ ਕੁਝ ਨਹੀਂ ਲਿਖਿਆ, ਤਾਂ ਇਸ ਖੇਤਰ ਵਿੱਚ "**No Positive**" ਹੋਵੇਗਾ
  - ਧਿਆਨ ਦਿਓ ਕਿ ਇੱਕ ਰਿਵਿਊਅਰ ਸਕਾਰਾਤਮਕ ਰਿਵਿਊ ਕਾਲਮ ਵਿੱਚ ਨਕਾਰਾਤਮਕ ਟਿੱਪਣੀ ਲਿਖ ਸਕਦਾ ਹੈ (ਜਿਵੇਂ ਕਿ "ਇਸ ਹੋਟਲ ਬਾਰੇ ਕੁਝ ਵੀ ਚੰਗਾ ਨਹੀਂ ਹੈ")
- `Review_Total_Positive_Word_Counts`
  - ਵੱਧ ਸਕਾਰਾਤਮਕ ਸ਼ਬਦ ਗਿਣਤੀ ਵੱਧ ਸਕੋਰ ਦਰਸਾਉਂਦੀ ਹੈ (ਭਾਵਨਾ ਦੀ ਜਾਂਚ ਕੀਤੇ ਬਿਨਾਂ)
- `Review_Date` ਅਤੇ `days_since_review`
  - ਇੱਕ ਤਾਜ਼ਗੀ ਜਾਂ ਪੁਰਾਣੇਪਨ ਦਾ ਮਾਪ ਲਾਗੂ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ (ਪੁਰਾਣੇ ਰਿਵਿਊ ਸ਼ਾਇਦ ਨਵੇਂ ਰਿਵਿਊਜ਼ ਜਿੰਨੇ ਸਹੀ ਨਾ ਹੋਣ, ਕਿਉਂਕਿ ਹੋਟਲ ਪ੍ਰਬੰਧਨ ਬਦਲ ਗਿਆ ਹੋਵੇ, ਜਾਂ ਨਵੀਨੀਕਰਨ ਹੋਏ ਹੋਣ, ਜਾਂ ਇੱਕ ਤਲਾਬ ਸ਼ਾਮਲ ਕੀਤਾ ਗਿਆ ਹੋਵੇ ਆਦਿ)
- `Tags`
  - ਇਹ ਛੋਟੇ ਵਰਣਨ ਹਨ ਜੋ ਇੱਕ ਰਿਵਿਊਅਰ ਚੁਣ ਸਕਦਾ ਹੈ ਜਿਵੇਂ ਕਿ ਉਹ ਕਿਸ ਕਿਸਮ ਦੇ ਮਹਿਮਾਨ ਸਨ (ਜਿਵੇਂ ਕਿ ਸਿੰਗਲ ਜਾਂ ਪਰਿਵਾਰ), ਉਹਨਾਂ ਕੋਲ ਕਿਹੜਾ ਕਮਰਾ ਸੀ, ਰਹਿਣ ਦੀ ਮਿਆਦ ਅਤੇ ਰਿਵਿਊ ਕਿਵੇਂ ਜਮ੍ਹਾਂ ਕੀਤਾ ਗਿਆ ਸੀ।
  - ਦੁਖਦਾਈ ਗੱਲ ਇਹ ਹੈ ਕਿ ਇਹ ਟੈਗ ਵਰਤਣਾ ਮੁਸ਼ਕਲ ਹੈ, ਹੇਠਾਂ ਦਿੱਤੇ ਭਾਗ ਵਿੱਚ ਇਸ ਦੀ ਵਰਤੋਂਯੋਗਤਾ 'ਤੇ ਚਰਚਾ ਕੀਤੀ ਗਈ ਹੈ

**ਰਿਵਿਊਅਰ ਕਾਲਮ**

- `Total_Number_of_Reviews_Reviewer_Has_Given`
  - ਇਹ ਸਿਫਾਰਸ਼ੀ ਮਾਡਲ ਵਿੱਚ ਇੱਕ ਕਾਰਕ ਹੋ ਸਕਦਾ ਹੈ, ਉਦਾਹਰਣ ਲਈ, ਜੇ ਤੁਸੀਂ ਇਹ ਨਿਰਧਾਰਤ ਕਰ ਸਕਦੇ ਹੋ ਕਿ ਸੈਂਕੜਿਆਂ ਰਿਵਿਊਜ਼ ਵਾਲੇ ਵੱਧ ਉਤਪਾਦਕ ਰਿਵਿਊਅਰ ਨਕਾਰਾਤਮਕ ਹੋਣ ਦੀ ਸੰਭਾਵਨਾ ਜ਼ਿਆਦਾ ਸੀ। ਹਾਲਾਂਕਿ, ਕਿਸੇ ਖਾਸ ਰਿਵਿਊ ਦੇ ਰਿਵਿਊਅਰ ਨੂੰ ਇੱਕ ਵਿਲੱਖਣ ਕੋਡ ਨਾਲ ਪਛਾਣਿਆ ਨਹੀਂ ਗਿਆ ਹੈ, ਅਤੇ ਇਸ ਲਈ ਇਸਨੂੰ ਰਿਵਿਊਜ਼ ਦੇ ਸੈੱਟ ਨਾਲ ਜੋੜਿਆ ਨਹੀਂ ਜਾ ਸਕਦਾ। 100 ਜਾਂ ਇਸ ਤੋਂ ਵੱਧ ਰਿਵਿਊਜ਼ ਵਾਲੇ 30 ਰਿਵਿਊਅਰ ਹਨ, ਪਰ ਇਹ ਦੇਖਣਾ ਮੁਸ਼ਕਲ ਹੈ ਕਿ ਇਹ ਸਿਫਾਰਸ਼ੀ ਮਾਡਲ ਵਿੱਚ ਕਿਵੇਂ ਸਹਾਇਕ ਹੋ ਸਕਦਾ ਹੈ।
- `Reviewer_Nationality`
  - ਕੁਝ ਲੋਕ ਸੋਚ ਸਕਦੇ ਹਨ ਕਿ ਕੁਝ ਰਾਸ਼ਟਰੀਤਾ ਵਾਲੇ ਲੋਕ ਸਕਾਰਾਤਮਕ ਜਾਂ ਨਕਾਰਾਤਮਕ ਰਿਵਿਊ ਦੇਣ ਦੀ ਵੱਧ ਸੰਭਾਵਨਾ ਰੱਖਦੇ ਹਨ। ਆਪਣੇ ਮਾਡਲਾਂ ਵਿੱਚ ਇਸ ਤਰ੍ਹਾਂ ਦੇ ਅਨੁਮਾਨਾਂ ਨੂੰ ਸ਼ਾਮਲ ਕਰਨ ਤੋਂ ਸਾਵਧਾਨ ਰਹੋ। ਇਹ ਰਾਸ਼ਟਰੀ (ਅਤੇ ਕਈ ਵਾਰ ਨਸਲੀ) ਸਟਿਰਿਓਟਾਈਪ ਹਨ, ਅਤੇ ਹਰ ਰਿਵਿਊਅਰ ਇੱਕ ਵਿਅਕਤੀਗਤ ਸੀ ਜਿਸਨੇ ਆਪਣੇ ਤਜਰਬੇ ਦੇ ਆਧਾਰ 'ਤੇ ਰਿਵਿਊ ਲਿਖਿਆ। 

##### ਉਦਾਹਰਣ

| Average  Score | Total Number   Reviews | Reviewer   Score | Negative <br />Review                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Positive   Review                 | Tags                                                                                      |
| -------------- | ---------------------- | ---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- | ----------------------------------------------------------------------------------------- |
| 7.8            | 1945                   | 2.5              | This is  currently not a hotel but a construction site I was terrorized from early  morning and all day with unacceptable building noise while resting after a  long trip and working in the room People were working all day i e with  jackhammers in the adjacent rooms I asked for a room change but no silent  room was available To make things worse I was overcharged I checked out in  the evening since I had to leave very early flight and received an appropriate  bill A day later the hotel made another charge without my consent in excess  of booked price It's a terrible place Don't punish yourself by booking  here | Nothing  Terrible place Stay away | Business trip                                Couple Standard Double  Room Stayed 2 nights |

ਜਿਵੇਂ ਤੁਸੀਂ ਦੇਖ ਸਕਦੇ ਹੋ, ਇਸ ਮਹਿਮਾਨ ਦਾ ਹੋਟਲ ਵਿੱਚ ਰਹਿਣ ਦਾ ਤਜਰਬਾ ਬਹੁਤ ਮਾੜਾ ਸੀ।
ਇਹ ਸੰਭਾਵਨਾ ਹੈ ਕਿ ਇਹ ਹੋਟਲ ਇੱਕ ਅਸਧਾਰਨ ਹੋ ਸਕਦਾ ਹੈ, ਅਤੇ ਸ਼ਾਇਦ ਜ਼ਿਆਦਾਤਰ ਮੁੱਲ ਸਹੀ ਹੋ ਸਕਦੇ ਹਨ (ਪਰ ਕੁਝ ਕਿਸੇ ਕਾਰਨ ਕਰਕੇ ਨਹੀਂ), ਅਸੀਂ ਅਗਲੇ ਹਿੱਸੇ ਵਿੱਚ ਇੱਕ ਛੋਟਾ ਪ੍ਰੋਗਰਾਮ ਲਿਖਾਂਗੇ ਤਾਂ ਜੋ ਡਾਟਾਸੈਟ ਵਿੱਚ ਮੁੱਲਾਂ ਦੀ ਜਾਂਚ ਕੀਤੀ ਜਾ ਸਕੇ ਅਤੇ ਸਹੀ ਵਰਤੋਂ (ਜਾਂ ਗਲਤ ਵਰਤੋਂ) ਦਾ ਨਿਰਧਾਰਨ ਕੀਤਾ ਜਾ ਸਕੇ।

> 🚨 ਸਾਵਧਾਨੀ ਦੀ ਨੋਟ
>
> ਜਦੋਂ ਤੁਸੀਂ ਇਸ ਡਾਟਾਸੈਟ ਨਾਲ ਕੰਮ ਕਰ ਰਹੇ ਹੋ, ਤੁਸੀਂ ਕੋਡ ਲਿਖੋਗੇ ਜੋ ਟੈਕਸਟ ਤੋਂ ਕੁਝ ਗਣਨਾ ਕਰਦਾ ਹੈ ਬਿਨਾਂ ਟੈਕਸਟ ਨੂੰ ਖੁਦ ਪੜ੍ਹਨ ਜਾਂ ਵਿਸ਼ਲੇਸ਼ਣ ਕਰਨ ਦੀ ਲੋੜ। ਇਹ NLP ਦਾ ਮੂਲ ਹੈ, ਅਰਥ ਜਾਂ ਭਾਵਨਾ ਦੀ ਵਿਆਖਿਆ ਕਰਨਾ ਬਿਨਾਂ ਕਿਸੇ ਮਨੁੱਖ ਦੀ ਮਦਦ ਲਈ। ਹਾਲਾਂਕਿ, ਇਹ ਸੰਭਵ ਹੈ ਕਿ ਤੁਸੀਂ ਕੁਝ ਨਕਾਰਾਤਮਕ ਸਮੀਖਿਆਵਾਂ ਪੜ੍ਹ ਸਕਦੇ ਹੋ। ਮੈਂ ਤੁਹਾਨੂੰ ਇਹ ਕਰਨ ਤੋਂ ਰੋਕਾਂਗਾ, ਕਿਉਂਕਿ ਤੁਹਾਨੂੰ ਇਸ ਦੀ ਲੋੜ ਨਹੀਂ। ਕੁਝ ਸਮੀਖਿਆਵਾਂ ਮੂਰਖ ਹਨ ਜਾਂ ਅਸੰਗਤ ਨਕਾਰਾਤਮਕ ਹੋਟਲ ਸਮੀਖਿਆਵਾਂ ਹਨ, ਜਿਵੇਂ ਕਿ "ਮੌਸਮ ਚੰਗਾ ਨਹੀਂ ਸੀ", ਜੋ ਹੋਟਲ ਜਾਂ ਕਿਸੇ ਦੇ ਵੀ ਨਿਯੰਤਰਣ ਤੋਂ ਬਾਹਰ ਹੈ। ਪਰ ਕੁਝ ਸਮੀਖਿਆਵਾਂ ਦਾ ਇੱਕ ਅੰਧਕਾਰ ਪਾਸਾ ਵੀ ਹੁੰਦਾ ਹੈ। ਕਈ ਵਾਰ ਨਕਾਰਾਤਮਕ ਸਮੀਖਿਆਵਾਂ ਨਸਲਵਾਦੀ, ਲਿੰਗਵਾਦੀ, ਜਾਂ ਉਮਰਵਾਦੀ ਹੁੰਦੀਆਂ ਹਨ। ਇਹ ਦੁਖਦਾਈ ਹੈ ਪਰ ਇੱਕ ਜਨਤਕ ਵੈਬਸਾਈਟ ਤੋਂ ਡਾਟਾ ਸਕ੍ਰੈਪ ਕਰਨ ਵਿੱਚ ਉਮੀਦ ਕੀਤੀ ਜਾ ਸਕਦੀ ਹੈ। ਕੁਝ ਸਮੀਖਿਆਕਾਰ ਅਜਿਹੀਆਂ ਸਮੀਖਿਆਵਾਂ ਛੱਡਦੇ ਹਨ ਜੋ ਤੁਹਾਨੂੰ ਅਸਵੀਕਾਰਯੋਗ, ਅਸੁਖਦਾਈ, ਜਾਂ ਪਰੇਸ਼ਾਨ ਕਰਨ ਵਾਲੀਆਂ ਲੱਗ ਸਕਦੀਆਂ ਹਨ। ਇਹ ਬਿਹਤਰ ਹੈ ਕਿ ਕੋਡ ਭਾਵਨਾ ਨੂੰ ਮਾਪੇ ਬਜਾਏ ਕਿ ਤੁਸੀਂ ਖੁਦ ਪੜ੍ਹੋ ਅਤੇ ਪਰੇਸ਼ਾਨ ਹੋਵੋ। ਇਹ ਕਹਿਣ ਤੋਂ ਬਾਅਦ, ਇਹ ਇੱਕ ਘੱਟ ਸੰਖਿਆ ਹੈ ਜੋ ਅਜਿਹੀਆਂ ਚੀਜ਼ਾਂ ਲਿਖਦੇ ਹਨ, ਪਰ ਇਹ ਫਿਰ ਵੀ ਮੌਜੂਦ ਹਨ।

## ਅਭਿਆਸ - ਡਾਟਾ ਦੀ ਜਾਂਚ
### ਡਾਟਾ ਲੋਡ ਕਰੋ

ਡਾਟਾ ਨੂੰ ਦ੍ਰਿਸ਼ੀ ਰੂਪ ਵਿੱਚ ਜਾਂਚਣ ਲਈ ਕਾਫ਼ੀ ਹੈ, ਹੁਣ ਤੁਸੀਂ ਕੁਝ ਕੋਡ ਲਿਖੋਗੇ ਅਤੇ ਕੁਝ ਜਵਾਬ ਪ੍ਰਾਪਤ ਕਰੋਗੇ! ਇਸ ਭਾਗ ਵਿੱਚ pandas ਲਾਇਬ੍ਰੇਰੀ ਦੀ ਵਰਤੋਂ ਕੀਤੀ ਗਈ ਹੈ। ਤੁਹਾਡਾ ਸਭ ਤੋਂ ਪਹਿਲਾ ਕੰਮ ਇਹ ਯਕੀਨੀ ਬਣਾਉਣਾ ਹੈ ਕਿ ਤੁਸੀਂ CSV ਡਾਟਾ ਲੋਡ ਅਤੇ ਪੜ੍ਹ ਸਕਦੇ ਹੋ। pandas ਲਾਇਬ੍ਰੇਰੀ ਵਿੱਚ ਇੱਕ ਤੇਜ਼ CSV ਲੋਡਰ ਹੈ, ਅਤੇ ਨਤੀਜਾ ਇੱਕ ਡਾਟਾਫਰੇਮ ਵਿੱਚ ਰੱਖਿਆ ਜਾਂਦਾ ਹੈ, ਜਿਵੇਂ ਪਿਛਲੇ ਪਾਠਾਂ ਵਿੱਚ। ਜੋ CSV ਅਸੀਂ ਲੋਡ ਕਰ ਰਹੇ ਹਾਂ, ਉਸ ਵਿੱਚ ਅੱਧੇ ਮਿਲੀਅਨ ਤੋਂ ਵੱਧ ਪੰਕਤੀਆਂ ਹਨ, ਪਰ ਸਿਰਫ 17 ਕਾਲਮ ਹਨ। pandas ਤੁਹਾਨੂੰ ਡਾਟਾਫਰੇਮ ਨਾਲ ਸੰਚਾਰ ਕਰਨ ਦੇ ਬਹੁਤ ਸਾਰੇ ਸ਼ਕਤੀਸ਼ਾਲੀ ਤਰੀਕੇ ਦਿੰਦਾ ਹੈ, ਜਿਸ ਵਿੱਚ ਹਰ ਪੰਕਤੀ 'ਤੇ ਕਾਰਵਾਈ ਕਰਨ ਦੀ ਸਮਰਥਾ ਸ਼ਾਮਲ ਹੈ।

ਇਸ ਪਾਠ ਦੇ ਇਸ ਹਿੱਸੇ ਤੋਂ ਅੱਗੇ, ਕੋਡ ਸਨਿੱਪਟਸ ਹੋਣਗੇ ਅਤੇ ਕੋਡ ਦੀ ਕੁਝ ਵਿਆਖਿਆ ਅਤੇ ਨਤੀਜਿਆਂ ਬਾਰੇ ਕੁਝ ਚਰਚਾ ਕੀਤੀ ਜਾਵੇਗੀ। ਆਪਣੇ ਕੋਡ ਲਈ ਸ਼ਾਮਲ _notebook.ipynb_ ਦੀ ਵਰਤੋਂ ਕਰੋ।

ਆਓ ਡਾਟਾ ਫਾਈਲ ਲੋਡ ਕਰਨ ਨਾਲ ਸ਼ੁਰੂ ਕਰੀਏ:

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

ਹੁਣ ਜਦੋਂ ਡਾਟਾ ਲੋਡ ਹੋ ਗਿਆ ਹੈ, ਅਸੀਂ ਇਸ 'ਤੇ ਕੁਝ ਕਾਰਵਾਈ ਕਰ ਸਕਦੇ ਹਾਂ। ਇਸ ਕੋਡ ਨੂੰ ਆਪਣੇ ਪ੍ਰੋਗਰਾਮ ਦੇ ਸਿਖਰ 'ਤੇ ਰੱਖੋ ਅਗਲੇ ਹਿੱਸੇ ਲਈ।

## ਡਾਟਾ ਦੀ ਜਾਂਚ

ਇਸ ਮਾਮਲੇ ਵਿੱਚ, ਡਾਟਾ ਪਹਿਲਾਂ ਹੀ *ਸਾਫ* ਹੈ, ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਇਹ ਕੰਮ ਕਰਨ ਲਈ ਤਿਆਰ ਹੈ, ਅਤੇ ਇਸ ਵਿੱਚ ਹੋਰ ਭਾਸ਼ਾਵਾਂ ਦੇ ਅੱਖਰ ਨਹੀਂ ਹਨ ਜੋ ਸਿਰਫ ਅੰਗਰੇਜ਼ੀ ਅੱਖਰਾਂ ਦੀ ਉਮੀਦ ਕਰਨ ਵਾਲੇ ਐਲਗੋਰਿਥਮ ਨੂੰ ਰੋਕ ਸਕਦੇ ਹਨ।

✅ ਤੁਹਾਨੂੰ ਅਜਿਹੇ ਡਾਟਾ ਨਾਲ ਕੰਮ ਕਰਨਾ ਪੈ ਸਕਦਾ ਹੈ ਜਿਸਨੂੰ NLP ਤਕਨੀਕਾਂ ਲਾਗੂ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ ਕੁਝ ਸ਼ੁਰੂਆਤੀ ਪ੍ਰੋਸੈਸਿੰਗ ਦੀ ਲੋੜ ਹੋਵੇ, ਪਰ ਇਸ ਵਾਰ ਨਹੀਂ। ਜੇ ਤੁਹਾਨੂੰ ਕਰਨਾ ਪਵੇ, ਤਾਂ ਤੁਸੀਂ ਗੈਰ-ਅੰਗਰੇਜ਼ੀ ਅੱਖਰਾਂ ਨੂੰ ਕਿਵੇਂ ਸੰਭਾਲੋਗੇ?

ਇੱਕ ਪਲ ਲਓ ਇਹ ਯਕੀਨੀ ਬਣਾਉਣ ਲਈ ਕਿ ਜਦੋਂ ਡਾਟਾ ਲੋਡ ਹੋ ਜਾਂਦਾ ਹੈ, ਤੁਸੀਂ ਇਸਨੂੰ ਕੋਡ ਨਾਲ ਜਾਂਚ ਸਕਦੇ ਹੋ। `Negative_Review` ਅਤੇ `Positive_Review` ਕਾਲਮਾਂ 'ਤੇ ਧਿਆਨ ਕੇਂਦਰਿਤ ਕਰਨਾ ਬਹੁਤ ਆਸਾਨ ਹੈ। ਇਹ ਕੁਦਰਤੀ ਟੈਕਸਟ ਨਾਲ ਭਰੇ ਹੋਏ ਹਨ ਜੋ ਤੁਹਾਡੇ NLP ਐਲਗੋਰਿਥਮ ਨੂੰ ਪ੍ਰਕਿਰਿਆ ਕਰਨ ਲਈ ਹਨ। ਪਰ ਰੁਕੋ! NLP ਅਤੇ ਭਾਵਨਾ ਵਿੱਚ ਛਾਲ ਮਾਰਨ ਤੋਂ ਪਹਿਲਾਂ, ਤੁਹਾਨੂੰ ਹੇਠਾਂ ਦਿੱਤੇ ਕੋਡ ਦੀ ਪਾਲਣਾ ਕਰਨੀ ਚਾਹੀਦੀ ਹੈ ਤਾਂ ਜੋ ਇਹ ਪਤਾ ਲਗਾਇਆ ਜਾ ਸਕੇ ਕਿ ਡਾਟਾਸੈਟ ਵਿੱਚ ਦਿੱਤੇ ਮੁੱਲ pandas ਨਾਲ ਗਣਨਾ ਕੀਤੇ ਮੁੱਲਾਂ ਨਾਲ ਮੇਲ ਖਾਂਦੇ ਹਨ ਜਾਂ ਨਹੀਂ।

## ਡਾਟਾਫਰੇਮ ਕਾਰਵਾਈਆਂ

ਇਸ ਪਾਠ ਵਿੱਚ ਪਹਿਲਾ ਕੰਮ ਇਹ ਜਾਂਚਣਾ ਹੈ ਕਿ ਹੇਠਾਂ ਦਿੱਤੇ ਦਾਅਵੇ ਸਹੀ ਹਨ ਜਾਂ ਨਹੀਂ, ਇਸ ਲਈ ਡਾਟਾਫਰੇਮ ਦੀ ਜਾਂਚ ਕਰਨ ਵਾਲਾ ਕੁਝ ਕੋਡ ਲਿਖੋ (ਇਸਨੂੰ ਬਦਲਣ ਤੋਂ ਬਿਨਾਂ)।

> ਬਹੁਤ ਸਾਰੇ ਪ੍ਰੋਗਰਾਮਿੰਗ ਕੰਮਾਂ ਦੀ ਤਰ੍ਹਾਂ, ਇਸਨੂੰ ਪੂਰਾ ਕਰਨ ਦੇ ਕਈ ਤਰੀਕੇ ਹਨ, ਪਰ ਚੰਗੀ ਸਲਾਹ ਇਹ ਹੈ ਕਿ ਇਸਨੂੰ ਸਭ ਤੋਂ ਸਧਾਰਨ, ਆਸਾਨ ਤਰੀਕੇ ਨਾਲ ਕਰੋ, ਖਾਸ ਕਰਕੇ ਜੇ ਇਹ ਭਵਿੱਖ ਵਿੱਚ ਇਸ ਕੋਡ ਨੂੰ ਸਮਝਣ ਲਈ ਆਸਾਨ ਹੋਵੇ। ਡਾਟਾਫਰੇਮਾਂ ਨਾਲ, ਇੱਕ ਵਿਸਤ੍ਰਿਤ API ਹੈ ਜੋ ਅਕਸਰ ਤੁਹਾਡੇ ਲਈ ਜੋ ਤੁਸੀਂ ਚਾਹੁੰਦੇ ਹੋ, ਕੁਸ਼ਲਤਾਪੂਰਵਕ ਕਰਨ ਦਾ ਤਰੀਕਾ ਹੋਵੇਗਾ।

ਹੇਠਾਂ ਦਿੱਤੇ ਪ੍ਰਸ਼ਨਾਂ ਨੂੰ ਕੋਡਿੰਗ ਟਾਸਕ ਵਜੋਂ ਮਾਨੋ ਅਤੇ ਹੱਲ ਦੇਖਣ ਤੋਂ ਬਿਨਾਂ ਉਨ੍ਹਾਂ ਦਾ ਜਵਾਬ ਦੇਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰੋ।

1. ਤੁਸੀਂ ਹੁਣੇ ਲੋਡ ਕੀਤੇ ਡਾਟਾਫਰੇਮ ਦਾ *shape* ਪ੍ਰਿੰਟ ਕਰੋ (shape ਪੰਕਤੀਆਂ ਅਤੇ ਕਾਲਮਾਂ ਦੀ ਗਿਣਤੀ ਹੈ)
2. ਸਮੀਖਿਆਕਾਰ ਦੇ ਰਾਸ਼ਟਰੀਤਾ ਲਈ ਫ੍ਰੀਕਵੈਂਸੀ ਗਿਣਤੀ ਦੀ ਗਣਨਾ ਕਰੋ:
   1. `Reviewer_Nationality` ਕਾਲਮ ਲਈ ਕਿੰਨੇ ਵਿਲੱਖਣ ਮੁੱਲ ਹਨ ਅਤੇ ਉਹ ਕੀ ਹਨ?
   2. ਡਾਟਾਸੈਟ ਵਿੱਚ ਸਭ ਤੋਂ ਆਮ ਸਮੀਖਿਆਕਾਰ ਰਾਸ਼ਟਰੀਤਾ ਕਿਹੜੀ ਹੈ (ਦੇਸ਼ ਅਤੇ ਸਮੀਖਿਆਵਾਂ ਦੀ ਗਿਣਤੀ ਪ੍ਰਿੰਟ ਕਰੋ)?
   3. ਅਗਲੇ 10 ਸਭ ਤੋਂ ਵੱਧ ਆਮ ਰਾਸ਼ਟਰੀਤਾਵਾਂ ਅਤੇ ਉਨ੍ਹਾਂ ਦੀ ਫ੍ਰੀਕਵੈਂਸੀ ਗਿਣਤੀ ਕੀ ਹੈ?
3. ਹਰ ਇੱਕ ਦੇ 10 ਸਭ ਤੋਂ ਵੱਧ ਸਮੀਖਿਆਕਾਰ ਰਾਸ਼ਟਰੀਤਾਵਾਂ ਲਈ ਸਭ ਤੋਂ ਵੱਧ ਸਮੀਖਿਆ ਕੀਤੇ ਗਏ ਹੋਟਲ ਕਿਹੜੇ ਸਨ?
4. ਡਾਟਾਸੈਟ ਵਿੱਚ ਪ੍ਰਤੀ ਹੋਟਲ ਕਿੰਨੀ ਸਮੀਖਿਆਵਾਂ ਹਨ (ਹੋਟਲ ਦੀ ਫ੍ਰੀਕਵੈਂਸੀ ਗਿਣਤੀ)?
5. ਜਦੋਂ ਕਿ ਡਾਟਾਸੈਟ ਵਿੱਚ ਹਰ ਹੋਟਲ ਲਈ `Average_Score` ਕਾਲਮ ਹੈ, ਤੁਸੀਂ ਇੱਕ ਔਸਤ ਸਕੋਰ ਦੀ ਗਣਨਾ ਵੀ ਕਰ ਸਕਦੇ ਹੋ (ਹਰ ਹੋਟਲ ਲਈ ਡਾਟਾਸੈਟ ਵਿੱਚ ਸਾਰੇ ਸਮੀਖਿਆਕਾਰ ਸਕੋਰਾਂ ਦਾ ਔਸਤ ਪ੍ਰਾਪਤ ਕਰਨਾ)। ਆਪਣੇ ਡਾਟਾਫਰੇਮ ਵਿੱਚ `Calc_Average_Score` ਕਾਲਮ ਹੈਡਰ ਨਾਲ ਇੱਕ ਨਵਾਂ ਕਾਲਮ ਸ਼ਾਮਲ ਕਰੋ ਜਿਸ ਵਿੱਚ ਉਹ ਗਣਨਾ ਕੀਤੀ ਗਈ ਔਸਤ ਹੈ।
6. ਕੀ ਕੋਈ ਹੋਟਲ ਹਨ ਜਿਨ੍ਹਾਂ ਦੇ (1 ਦਸ਼ਮਲਵ ਸਥਾਨ 'ਤੇ ਗੋਲ ਕੀਤੇ) `Average_Score` ਅਤੇ `Calc_Average_Score` ਇੱਕੋ ਜਿਹੇ ਹਨ?
   1. ਇੱਕ Python ਫੰਕਸ਼ਨ ਲਿਖਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰੋ ਜੋ ਇੱਕ Series (row) ਨੂੰ ਦਲੀਲ ਵਜੋਂ ਲੈਂਦਾ ਹੈ ਅਤੇ ਮੁੱਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ, ਜਦੋਂ ਮੁੱਲ ਇੱਕੋ ਜਿਹੇ ਨਹੀਂ ਹੁੰਦੇ ਤਾਂ ਸੁਨੇਹਾ ਪ੍ਰਿੰਟ ਕਰਦਾ ਹੈ। ਫਿਰ `.apply()` ਵਿਧੀ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਹਰ ਪੰਕਤੀ ਨੂੰ ਫੰਕਸ਼ਨ ਨਾਲ ਪ੍ਰਕਿਰਿਆ ਕਰੋ।
7. ਕਾਲਮ `Negative_Review` ਦੇ "No Negative" ਮੁੱਲਾਂ ਵਾਲੀਆਂ ਕਿੰਨੀ ਪੰਕਤੀਆਂ ਹਨ, ਇਹ ਗਿਣਨਾ ਕਰੋ ਅਤੇ ਪ੍ਰਿੰਟ ਕਰੋ।
8. ਕਾਲਮ `Positive_Review` ਦੇ "No Positive" ਮੁੱਲਾਂ ਵਾਲੀਆਂ ਕਿੰਨੀ ਪੰਕਤੀਆਂ ਹਨ, ਇਹ ਗਿਣਨਾ ਕਰੋ ਅਤੇ ਪ੍ਰਿੰਟ ਕਰੋ।
9. ਕਾਲਮ `Positive_Review` ਦੇ "No Positive" **ਅਤੇ** `Negative_Review` ਦੇ "No Negative" ਮੁੱਲਾਂ ਵਾਲੀਆਂ ਕਿੰਨੀ ਪੰਕਤੀਆਂ ਹਨ, ਇਹ ਗਿਣਨਾ ਕਰੋ ਅਤੇ ਪ੍ਰਿੰਟ ਕਰੋ।

### ਕੋਡ ਜਵਾਬ

1. ਤੁਸੀਂ ਹੁਣੇ ਲੋਡ ਕੀਤੇ ਡਾਟਾਫਰੇਮ ਦਾ *shape* ਪ੍ਰਿੰਟ ਕਰੋ (shape ਪੰਕਤੀਆਂ ਅਤੇ ਕਾਲਮਾਂ ਦੀ ਗਿਣਤੀ ਹੈ)

   ```python
   print("The shape of the data (rows, cols) is " + str(df.shape))
   > The shape of the data (rows, cols) is (515738, 17)
   ```

2. ਸਮੀਖਿਆਕਾਰ ਦੇ ਰਾਸ਼ਟਰੀਤਾ ਲਈ ਫ੍ਰੀਕਵੈਂਸੀ ਗਿਣਤੀ ਦੀ ਗਣਨਾ ਕਰੋ:

   1. `Reviewer_Nationality` ਕਾਲਮ ਲਈ ਕਿੰਨੇ ਵਿਲੱਖਣ ਮੁੱਲ ਹਨ ਅਤੇ ਉਹ ਕੀ ਹਨ?
   2. ਡਾਟਾਸੈਟ ਵਿੱਚ ਸਭ ਤੋਂ ਆਮ ਸਮੀਖਿਆਕਾਰ ਰਾਸ਼ਟਰੀਤਾ ਕਿਹੜੀ ਹੈ (ਦੇਸ਼ ਅਤੇ ਸਮੀਖਿਆਵਾਂ ਦੀ ਗਿਣਤੀ ਪ੍ਰਿੰਟ ਕਰੋ)?

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

   3. ਅਗਲੇ 10 ਸਭ ਤੋਂ ਵੱਧ ਆਮ ਰਾਸ਼ਟਰੀਤਾਵਾਂ ਅਤੇ ਉਨ੍ਹਾਂ ਦੀ ਫ੍ਰੀਕਵੈਂਸੀ ਗਿਣਤੀ ਕੀ ਹੈ?

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

3. ਹਰ ਇੱਕ ਦੇ 10 ਸਭ ਤੋਂ ਵੱਧ ਸਮੀਖਿਆਕਾਰ ਰਾਸ਼ਟਰੀਤਾਵਾਂ ਲਈ ਸਭ ਤੋਂ ਵੱਧ ਸਮੀਖਿਆ ਕੀਤੇ ਗਏ ਹੋਟਲ ਕਿਹੜੇ ਸਨ?

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

4. ਡਾਟਾਸੈਟ ਵਿੱਚ ਪ੍ਰਤੀ ਹੋਟਲ ਕਿੰਨੀ ਸਮੀਖਿਆਵਾਂ ਹਨ (ਹੋਟਲ ਦੀ ਫ੍ਰੀਕਵੈਂਸੀ ਗਿਣਤੀ)?

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
   
   ਤੁਸੀਂ ਧਿਆਨ ਦੇ ਸਕਦੇ ਹੋ ਕਿ *counted in the dataset* ਨਤੀਜੇ `Total_Number_of_Reviews` ਵਿੱਚ ਮੁੱਲਾਂ ਨਾਲ ਮੇਲ ਨਹੀਂ ਖਾਂਦੇ। ਇਹ ਸਪਸ਼ਟ ਨਹੀਂ ਹੈ ਕਿ ਡਾਟਾਸੈਟ ਵਿੱਚ ਇਹ ਮੁੱਲ ਹੋਟਲ ਦੀ ਕੁੱਲ ਸਮੀਖਿਆਵਾਂ ਦੀ ਨੁਮਾਇੰਦਗੀ ਕਰਦਾ ਹੈ, ਪਰ ਸਾਰੀਆਂ ਸਕ੍ਰੈਪ ਨਹੀਂ ਕੀਤੀਆਂ ਗਈਆਂ, ਜਾਂ ਕੁਝ ਹੋਰ ਗਣਨਾ। `Total_Number_of_Reviews` ਮਾਡਲ ਵਿੱਚ ਵਰਤਿਆ ਨਹੀਂ ਜਾਂਦਾ ਕਿਉਂਕਿ ਇਹ ਸਪਸ਼ਟਤਾ ਨਹੀਂ ਹੈ।

5. ਜਦੋਂ ਕਿ ਡਾਟਾਸੈਟ ਵਿੱਚ ਹਰ ਹੋਟਲ ਲਈ `Average_Score` ਕਾਲਮ ਹੈ, ਤੁਸੀਂ ਇੱਕ ਔਸਤ ਸਕੋਰ ਦੀ ਗਣਨਾ ਵੀ ਕਰ ਸਕਦੇ ਹੋ (ਹਰ ਹੋਟਲ ਲਈ ਡਾਟਾਸੈਟ ਵਿੱਚ ਸਾਰੇ ਸਮੀਖਿਆਕਾਰ ਸਕੋਰਾਂ ਦਾ ਔਸਤ ਪ੍ਰਾਪਤ ਕਰਨਾ)। ਆਪਣੇ ਡਾਟਾਫਰੇਮ ਵਿੱਚ `Calc_Average_Score` ਕਾਲਮ ਹੈਡਰ ਨਾਲ ਇੱਕ ਨਵਾਂ ਕਾਲਮ ਸ਼ਾਮਲ ਕਰੋ ਜਿਸ ਵਿੱਚ ਉਹ ਗਣਨਾ ਕੀਤੀ ਗਈ ਔਸਤ ਹੈ। ਕਾਲਮ `Hotel_Name`, `Average_Score`, ਅਤੇ `Calc_Average_Score` ਪ੍ਰਿੰਟ ਕਰੋ।

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

   ਤੁਸੀਂ ਇਹ ਵੀ ਸੋਚ ਸਕਦੇ ਹੋ ਕਿ `Average_Score` ਮੁੱਲ ਅਤੇ ਗਣਨਾ ਕੀਤੇ ਔਸਤ ਸਕੋਰ ਵਿੱਚ ਕਿਉਂ ਕਈ ਵਾਰ ਅੰਤਰ ਹੁੰਦਾ ਹੈ। ਜਿਵੇਂ ਕਿ ਅਸੀਂ ਨਹੀਂ ਜਾਣ ਸਕਦੇ ਕਿ ਕਿਉਂ ਕੁਝ ਮੁੱਲ ਮੇਲ ਖਾਂਦੇ ਹਨ, ਪਰ ਹੋਰਾਂ ਵਿੱਚ ਅੰਤਰ ਹੈ, ਇਸ ਮਾਮਲੇ ਵਿੱਚ ਸੁਰੱਖਿਅਤ ਹੈ ਕਿ ਅਸੀਂ ਆਪਣੇ ਆਪ ਗਣਨਾ ਕਰਨ ਲਈ ਸਮੀਖਿਆ ਸਕੋਰਾਂ ਦੀ ਵਰਤੋਂ ਕਰੀਏ। ਇਹ ਕਹਿਣ ਤੋਂ ਬਾਅਦ, ਅੰਤਰ ਆਮ ਤੌਰ 'ਤੇ ਬਹੁਤ ਛੋਟਾ ਹੁੰਦਾ ਹੈ, ਇੱਥੇ ਉਹ ਹੋਟਲ ਹਨ ਜਿਨ੍ਹਾਂ ਦੇ ਡਾਟਾਸੈਟ ਔਸਤ ਅਤੇ ਗਣਨਾ ਕੀਤੇ ਔਸਤ ਵਿੱਚ ਸਭ ਤੋਂ ਵੱਧ ਅੰਤਰ ਹੈ:

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

   ਸਿਰਫ 1 ਹੋਟਲ ਜਿਸਦਾ ਸਕੋਰ ਵਿੱਚ 1 ਤੋਂ ਵੱਧ ਅੰਤਰ ਹੈ, ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਅਸੀਂ ਸ਼ਾਇਦ ਅੰਤਰ ਨੂੰ ਨਜ਼ਰਅੰਦਾਜ਼ ਕਰ ਸਕਦੇ ਹਾਂ ਅਤੇ ਗਣਨਾ ਕੀਤੇ ਔਸਤ ਸਕੋਰ ਦੀ ਵਰਤੋਂ ਕਰ ਸਕਦੇ ਹਾਂ।

6. ਕਾਲਮ `Negative_Review` ਦੇ "No Negative" ਮੁੱਲਾਂ ਵਾਲੀਆਂ ਕਿੰਨੀ ਪੰਕਤੀਆਂ ਹਨ, ਇਹ ਗਿਣਨਾ ਕਰੋ ਅਤੇ ਪ੍ਰਿੰਟ ਕਰੋ।

7. ਕਾਲਮ `Positive_Review` ਦੇ "No Positive" ਮੁੱਲਾਂ ਵਾਲੀਆਂ ਕਿੰਨੀ ਪੰਕਤੀਆਂ ਹਨ, ਇਹ ਗਿਣਨਾ ਕਰੋ ਅਤੇ ਪ੍ਰਿੰਟ ਕਰੋ।

8. ਕਾਲਮ `Positive_Review` ਦੇ "No Positive" **ਅਤੇ** `Negative_Review` ਦੇ "No Negative" ਮੁੱਲਾਂ ਵਾਲੀਆਂ ਕਿੰਨੀ ਪੰਕਤੀਆਂ ਹਨ, ਇਹ ਗਿਣਨਾ ਕਰੋ ਅਤੇ ਪ੍ਰਿੰਟ ਕਰੋ।

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

## ਇੱਕ ਹੋਰ ਤਰੀਕਾ

ਲੈਂਬਡਾ ਬਿਨਾਂ ਆਈਟਮਾਂ ਦੀ ਗਿਣਤੀ ਕਰਨ ਦਾ ਇੱਕ ਹੋਰ ਤਰੀਕਾ, ਅਤੇ ਪੰਕਤੀਆਂ

---

**ਅਸਵੀਕਾਰਨਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਨਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼, ਜੋ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਹੈ, ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।