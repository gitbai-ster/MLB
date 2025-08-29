<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "76438ce4e5d48982d48f1b55c981caac",
  "translation_date": "2025-08-29T17:58:19+00:00",
  "source_file": "4-Classification/1-Introduction/README.md",
  "language_code": "pa"
}
-->
# ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਦਾ ਪਰਚੇ

ਇਹ ਚਾਰ ਪਾਠਾਂ ਵਿੱਚ, ਤੁਸੀਂ ਕਲਾਸਿਕ ਮਸ਼ੀਨ ਲਰਨਿੰਗ ਦੇ ਇੱਕ ਮੂਲ ਧਿਆਨ - _ਕਲਾਸੀਫਿਕੇਸ਼ਨ_ - ਦੀ ਖੋਜ ਕਰੋਗੇ। ਅਸੀਂ ਏਸ਼ੀਆ ਅਤੇ ਭਾਰਤ ਦੇ ਸਾਰੇ ਸ਼ਾਨਦਾਰ ਖਾਣਿਆਂ ਦੇ ਡੇਟਾਸੈਟ ਨਾਲ ਵੱਖ-ਵੱਖ ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਐਲਗੋਰਿਥਮ ਦੀ ਵਰਤੋਂ ਕਰਨ ਦਾ ਤਰੀਕਾ ਸਿੱਖਾਂਗੇ। ਉਮੀਦ ਹੈ ਕਿ ਤੁਸੀਂ ਭੁੱਖੇ ਹੋ!

![ਸਿਰਫ਼ ਇੱਕ ਚੁਟਕੀ!](../../../../translated_images/pinch.1b035ec9ba7e0d408313b551b60c721c9c290b2dd2094115bc87e6ddacd114c9.pa.png)

> ਇਹ ਪਾਠ ਪੈਨ-ਏਸ਼ੀਆਈ ਖਾਣਿਆਂ ਦਾ ਜਸ਼ਨ ਮਨਾਉਂਦੇ ਹਨ! ਚਿੱਤਰ [Jen Looper](https://twitter.com/jenlooper) ਦੁਆਰਾ

ਕਲਾਸੀਫਿਕੇਸ਼ਨ [ਸੁਪਰਵਾਈਜ਼ਡ ਲਰਨਿੰਗ](https://wikipedia.org/wiki/Supervised_learning) ਦਾ ਇੱਕ ਰੂਪ ਹੈ ਜੋ ਰਿਗ੍ਰੈਸ਼ਨ ਤਕਨੀਕਾਂ ਨਾਲ ਕਾਫ਼ੀ ਸਮਾਨਤਾ ਰੱਖਦਾ ਹੈ। ਜੇ ਮਸ਼ੀਨ ਲਰਨਿੰਗ ਡੇਟਾਸੈਟ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਮੁੱਲ ਜਾਂ ਚੀਜ਼ਾਂ ਦੇ ਨਾਮਾਂ ਦੀ ਪੇਸ਼ਗੂਈ ਕਰਨ ਬਾਰੇ ਹੈ, ਤਾਂ ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਆਮ ਤੌਰ 'ਤੇ ਦੋ ਸਮੂਹਾਂ ਵਿੱਚ ਵੰਡਿਆ ਜਾਂਦਾ ਹੈ: _ਬਾਈਨਰੀ ਕਲਾਸੀਫਿਕੇਸ਼ਨ_ ਅਤੇ _ਮਲਟੀਕਲਾਸ ਕਲਾਸੀਫਿਕੇਸ਼ਨ_।

[![ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਦਾ ਪਰਚੇ](https://img.youtube.com/vi/eg8DJYwdMyg/0.jpg)](https://youtu.be/eg8DJYwdMyg "ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਦਾ ਪਰਚੇ")

> 🎥 ਉਪਰੋਕਤ ਚਿੱਤਰ 'ਤੇ ਕਲਿਕ ਕਰੋ: MIT ਦੇ John Guttag ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਦੀ ਜਾਣਕਾਰੀ ਦਿੰਦੇ ਹਨ

ਯਾਦ ਰੱਖੋ:

- **ਲਿਨੀਅਰ ਰਿਗ੍ਰੈਸ਼ਨ** ਨੇ ਤੁਹਾਨੂੰ ਵੈਰੀਏਬਲਾਂ ਦੇ ਵਿਚਕਾਰ ਸੰਬੰਧਾਂ ਦੀ ਪੇਸ਼ਗੂਈ ਕਰਨ ਅਤੇ ਨਵੀਂ ਡੇਟਾਪੌਇੰਟ ਕਿੱਥੇ ਲਾਈਨ ਦੇ ਸੰਬੰਧ ਵਿੱਚ ਆਵੇਗੀ, ਇਸ ਦੀ ਸਹੀ ਪੇਸ਼ਗੂਈ ਕਰਨ ਵਿੱਚ ਮਦਦ ਕੀਤੀ। ਉਦਾਹਰਣ ਲਈ, ਤੁਸੀਂ ਪੇਸ਼ਗੂਈ ਕਰ ਸਕਦੇ ਹੋ ਕਿ _ਸਤੰਬਰ ਦੇ ਮੁਕਾਬਲੇ ਦਸੰਬਰ ਵਿੱਚ ਕਦੂ ਦੀ ਕੀਮਤ ਕੀ ਹੋਵੇਗੀ_।
- **ਲੌਜਿਸਟਿਕ ਰਿਗ੍ਰੈਸ਼ਨ** ਨੇ ਤੁਹਾਨੂੰ "ਬਾਈਨਰੀ ਸ਼੍ਰੇਣੀਆਂ" ਦੀ ਖੋਜ ਕਰਨ ਵਿੱਚ ਮਦਦ ਕੀਤੀ: ਇਸ ਕੀਮਤ 'ਤੇ, _ਕੀ ਇਹ ਕਦੂ ਸੰਤਰੀ ਹੈ ਜਾਂ ਨਾ-ਸੰਤਰੀ_?

ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਵੱਖ-ਵੱਖ ਐਲਗੋਰਿਥਮ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ ਤਾਂ ਜੋ ਡੇਟਾਪੌਇੰਟ ਦੇ ਲੇਬਲ ਜਾਂ ਕਲਾਸ ਨੂੰ ਨਿਰਧਾਰਤ ਕਰਨ ਦੇ ਹੋਰ ਤਰੀਕੇ ਨਿਰਧਾਰਤ ਕੀਤੇ ਜਾ ਸਕਣ। ਆਓ ਇਸ ਖਾਣੇ ਦੇ ਡੇਟਾ ਨਾਲ ਕੰਮ ਕਰੀਏ ਤਾਂ ਜੋ ਦੇਖਿਆ ਜਾ ਸਕੇ ਕਿ ਸਮੂਹ ਦੇ ਸਮੱਗਰੀਆਂ ਨੂੰ ਦੇਖ ਕੇ, ਅਸੀਂ ਇਸ ਦੇ ਖਾਣੇ ਦੇ ਮੂਲ ਦੇਸ਼ ਦਾ ਪਤਾ ਲਗਾ ਸਕਦੇ ਹਾਂ।

## [ਪ੍ਰੀ-ਪਾਠ ਕਵਿਜ਼](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/19/)

> ### [ਇਹ ਪਾਠ R ਵਿੱਚ ਉਪਲਬਧ ਹੈ!](../../../../4-Classification/1-Introduction/solution/R/lesson_10.html)

### ਪਰਚੇ

ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਮਸ਼ੀਨ ਲਰਨਿੰਗ ਖੋਜਕਰਤਾ ਅਤੇ ਡੇਟਾ ਸਾਇੰਟਿਸਟ ਦੀਆਂ ਮੂਲ ਗਤੀਵਿਧੀਆਂ ਵਿੱਚੋਂ ਇੱਕ ਹੈ। ਬਾਈਨਰੀ ਮੁੱਲ ("ਕੀ ਇਹ ਈਮੇਲ ਸਪੈਮ ਹੈ ਜਾਂ ਨਹੀਂ?") ਦੀ ਬੁਨਿਆਦੀ ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਤੋਂ ਲੈ ਕੇ ਕੰਪਿਊਟਰ ਵਿਜ਼ਨ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਜਟਿਲ ਚਿੱਤਰ ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਅਤੇ ਸੈਗਮੈਂਟੇਸ਼ਨ ਤੱਕ, ਡੇਟਾ ਨੂੰ ਕਲਾਸਾਂ ਵਿੱਚ ਵੰਡਣਾ ਅਤੇ ਇਸ ਤੋਂ ਸਵਾਲ ਪੁੱਛਣਾ ਹਮੇਸ਼ਾ ਲਾਭਦਾਇਕ ਹੁੰਦਾ ਹੈ।

ਇਸ ਪ੍ਰਕਿਰਿਆ ਨੂੰ ਹੋਰ ਵਿਗਿਆਨਕ ਢੰਗ ਨਾਲ ਵਿਆਖਿਆ ਕਰਨ ਲਈ, ਤੁਹਾਡਾ ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਤਰੀਕਾ ਇੱਕ ਪੇਸ਼ਗੂਈ ਮਾਡਲ ਬਣਾਉਂਦਾ ਹੈ ਜੋ ਤੁਹਾਨੂੰ ਇਨਪੁਟ ਵੈਰੀਏਬਲਾਂ ਅਤੇ ਆਉਟਪੁਟ ਵੈਰੀਏਬਲਾਂ ਦੇ ਵਿਚਕਾਰ ਸੰਬੰਧ ਨੂੰ ਨਕਸ਼ਾ ਬਣਾਉਣ ਯੋਗ ਬਣਾਉਂਦਾ ਹੈ।

![ਬਾਈਨਰੀ ਵਸ. ਮਲਟੀਕਲਾਸ ਕਲਾਸੀਫਿਕੇਸ਼ਨ](../../../../translated_images/binary-multiclass.b56d0c86c81105a697dddd82242c1d11e4d78b7afefea07a44627a0f1111c1a9.pa.png)

> ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਐਲਗੋਰਿਥਮਾਂ ਲਈ ਬਾਈਨਰੀ ਵਸ. ਮਲਟੀਕਲਾਸ ਸਮੱਸਿਆਵਾਂ। ਇਨਫੋਗ੍ਰਾਫਿਕ [Jen Looper](https://twitter.com/jenlooper) ਦੁਆਰਾ

ਡੇਟਾ ਨੂੰ ਸਾਫ਼ ਕਰਨ, ਇਸ ਨੂੰ ਵਿਜ਼ੁਅਲ ਬਣਾਉਣ ਅਤੇ ਇਸ ਨੂੰ ML ਕੰਮਾਂ ਲਈ ਤਿਆਰ ਕਰਨ ਦੀ ਪ੍ਰਕਿਰਿਆ ਸ਼ੁਰੂ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ, ਆਓ ਸਿੱਖੀਏ ਕਿ ਮਸ਼ੀਨ ਲਰਨਿੰਗ ਨੂੰ ਡੇਟਾ ਨੂੰ ਕਲਾਸੀਫਾਈ ਕਰਨ ਲਈ ਕਿਵੇਂ ਲੈਵਰੇਜ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ।

[ਅੰਕੜੇ](https://wikipedia.org/wiki/Statistical_classification) ਤੋਂ ਲਿਆ ਗਿਆ, ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਕਲਾਸਿਕ ਮਸ਼ੀਨ ਲਰਨਿੰਗ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ ਜਿਵੇਂ ਕਿ `smoker`, `weight`, ਅਤੇ `age` ਵਰਗੇ ਫੀਚਰਾਂ ਨੂੰ ਵਰਤ ਕੇ _ਕਿਸੇ X ਬਿਮਾਰੀ ਦੇ ਵਿਕਾਸ ਦੀ ਸੰਭਾਵਨਾ_ ਦਾ ਪਤਾ ਲਗਾਉਣ ਲਈ। ਇੱਕ ਸੁਪਰਵਾਈਜ਼ਡ ਲਰਨਿੰਗ ਤਕਨੀਕ ਦੇ ਤੌਰ 'ਤੇ ਜੋ ਤੁਸੀਂ ਪਹਿਲਾਂ ਕੀਤੇ ਰਿਗ੍ਰੈਸ਼ਨ ਅਭਿਆਸਾਂ ਦੇ ਸਮਾਨ ਹੈ, ਤੁਹਾਡਾ ਡੇਟਾ ਲੇਬਲ ਕੀਤਾ ਜਾਂਦਾ ਹੈ ਅਤੇ ML ਐਲਗੋਰਿਥਮ ਉਹਨਾਂ ਲੇਬਲਾਂ ਦੀ ਵਰਤੋਂ ਕਰਦੇ ਹਨ ਤਾਂ ਜੋ ਡੇਟਾਸੈਟ ਦੇ ਕਲਾਸਾਂ (ਜਾਂ 'ਫੀਚਰਾਂ') ਦੀ ਪੇਸ਼ਗੂਈ ਕੀਤੀ ਜਾ ਸਕੇ ਅਤੇ ਉਨ੍ਹਾਂ ਨੂੰ ਇੱਕ ਸਮੂਹ ਜਾਂ ਨਤੀਜੇ ਵਿੱਚ ਸੌਂਪਿਆ ਜਾ ਸਕੇ।

✅ ਇੱਕ ਖਾਣੇ ਦੇ ਡੇਟਾਸੈਟ ਦੀ ਕਲਪਨਾ ਕਰਨ ਲਈ ਇੱਕ ਪਲ ਲਓ। ਇੱਕ ਮਲਟੀਕਲਾਸ ਮਾਡਲ ਕੀ ਸਵਾਲ ਦੇ ਸਕਦਾ ਹੈ? ਇੱਕ ਬਾਈਨਰੀ ਮਾਡਲ ਕੀ ਸਵਾਲ ਦੇ ਸਕਦਾ ਹੈ? ਜੇ ਤੁਸੀਂ ਇਹ ਪਤਾ ਲਗਾਉਣਾ ਚਾਹੁੰਦੇ ਹੋ ਕਿ ਦਿੱਤੇ ਗਏ ਖਾਣੇ ਵਿੱਚ ਮੀਥੀ ਦੇ ਪੱਤੇ ਦੀ ਵਰਤੋਂ ਹੋਵੇਗੀ ਜਾਂ ਨਹੀਂ, ਤਾਂ ਕੀ ਹੋਵੇਗਾ? ਜੇ ਤੁਸੀਂ ਇੱਕ ਕਿਰਾਣੇ ਦੇ ਬੈਗ ਵਿੱਚ ਸਟਾਰ ਐਨੀਸ, ਅਰਟੀਚੋਕ, ਫੁੱਲਗੋਭੀ, ਅਤੇ ਹਾਰਸਰੈਡਿਸ਼ ਦੇ ਤੋਹਫ਼ੇ ਦੇ ਨਾਲ ਇੱਕ ਆਮ ਭਾਰਤੀ ਖਾਣਾ ਬਣਾਉਣਾ ਚਾਹੁੰਦੇ ਹੋ, ਤਾਂ ਕੀ ਹੋਵੇਗਾ?

[![ਪ੍ਰੇਸ਼ਾਨ ਕਰਨ ਵਾਲੇ ਮਿਸਟਰੀ ਬਾਸਕਟ](https://img.youtube.com/vi/GuTeDbaNoEU/0.jpg)](https://youtu.be/GuTeDbaNoEU "ਪ੍ਰੇਸ਼ਾਨ ਕਰਨ ਵਾਲੇ ਮਿਸਟਰੀ ਬਾਸਕਟ")

> 🎥 ਉਪਰੋਕਤ ਚਿੱਤਰ 'ਤੇ ਕਲਿਕ ਕਰੋ। 'Chopped' ਸ਼ੋਅ ਦਾ ਸਾਰ ਇਹ ਹੈ ਕਿ 'ਮਿਸਟਰੀ ਬਾਸਕਟ' ਜਿੱਥੇ ਸ਼ੈਫ਼ਾਂ ਨੂੰ ਬੇਤਰਤੀਬ ਚੁਣੇ ਗਏ ਸਮੱਗਰੀਆਂ ਨਾਲ ਕੁਝ ਖਾਣਾ ਬਣਾਉਣਾ ਪੈਂਦਾ ਹੈ। ਨਿਸ਼ਚਿਤ ਤੌਰ 'ਤੇ ਇੱਕ ML ਮਾਡਲ ਮਦਦ ਕਰਦਾ!

## ਹੈਲੋ 'ਕਲਾਸੀਫਾਇਰ'

ਜੋ ਸਵਾਲ ਅਸੀਂ ਇਸ ਖਾਣੇ ਦੇ ਡੇਟਾਸੈਟ ਤੋਂ ਪੁੱਛਣਾ ਚਾਹੁੰਦੇ ਹਾਂ, ਉਹ ਅਸਲ ਵਿੱਚ ਇੱਕ **ਮਲਟੀਕਲਾਸ ਸਵਾਲ** ਹੈ, ਕਿਉਂਕਿ ਸਾਡੇ ਕੋਲ ਕੰਮ ਕਰਨ ਲਈ ਕਈ ਸੰਭਾਵਿਤ ਰਾਸ਼ਟਰੀ ਖਾਣੇ ਹਨ। ਦਿੱਤੇ ਗਏ ਸਮੱਗਰੀਆਂ ਦੇ ਬੈਚ ਦੇ ਆਧਾਰ 'ਤੇ, ਇਹ ਡੇਟਾ ਕਿਹੜੇ ਕਈ ਕਲਾਸਾਂ ਵਿੱਚ ਫਿੱਟ ਹੋਵੇਗਾ?

Scikit-learn ਵੱਖ-ਵੱਖ ਐਲਗੋਰਿਥਮ ਪੇਸ਼ ਕਰਦਾ ਹੈ ਜੋ ਤੁਸੀਂ ਡੇਟਾ ਨੂੰ ਕਲਾਸੀਫਾਈ ਕਰਨ ਲਈ ਵਰਤ ਸਕਦੇ ਹੋ, ਇਸ 'ਤੇ ਨਿਰਭਰ ਕਰਦੇ ਹੋਏ ਕਿ ਤੁਸੀਂ ਕਿਹੜੀ ਸਮੱਸਿਆ ਹੱਲ ਕਰਨਾ ਚਾਹੁੰਦੇ ਹੋ। ਅਗਲੇ ਦੋ ਪਾਠਾਂ ਵਿੱਚ, ਤੁਸੀਂ ਇਹਨਾਂ ਐਲਗੋਰਿਥਮਾਂ ਬਾਰੇ ਸਿੱਖੋਗੇ।

## ਅਭਿਆਸ - ਆਪਣੇ ਡੇਟਾ ਨੂੰ ਸਾਫ਼ ਅਤੇ ਸੰਤੁਲਿਤ ਕਰੋ

ਇਸ ਪ੍ਰਾਜੈਕਟ ਨੂੰ ਸ਼ੁਰੂ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ ਪਹਿਲਾ ਕੰਮ, ਤੁਹਾਡੇ ਡੇਟਾ ਨੂੰ ਸਾਫ਼ ਅਤੇ **ਸੰਤੁਲਿਤ** ਕਰਨਾ ਹੈ ਤਾਂ ਜੋ ਵਧੀਆ ਨਤੀਜੇ ਪ੍ਰਾਪਤ ਕੀਤੇ ਜਾ ਸਕਣ। ਇਸ ਫੋਲਡਰ ਦੇ ਰੂਟ ਵਿੱਚ ਖਾਲੀ _notebook.ipynb_ ਫਾਈਲ ਨਾਲ ਸ਼ੁਰੂ ਕਰੋ।

ਸਭ ਤੋਂ ਪਹਿਲਾਂ [imblearn](https://imbalanced-learn.org/stable/) ਇੰਸਟਾਲ ਕਰੋ। ਇਹ Scikit-learn ਪੈਕੇਜ ਹੈ ਜੋ ਤੁਹਾਨੂੰ ਡੇਟਾ ਨੂੰ ਵਧੀਆ ਸੰਤੁਲਿਤ ਕਰਨ ਦੀ ਆਗਿਆ ਦੇਵੇਗਾ (ਤੁਸੀਂ ਇਸ ਕੰਮ ਬਾਰੇ ਇੱਕ ਮਿੰਟ ਵਿੱਚ ਹੋਰ ਸਿੱਖੋਗੇ)।

1. `imblearn` ਨੂੰ ਇੰਸਟਾਲ ਕਰਨ ਲਈ, `pip install` ਚਲਾਓ, ਇਸ ਤਰ੍ਹਾਂ:

    ```python
    pip install imblearn
    ```

1. ਉਹ ਪੈਕੇਜ ਇੰਪੋਰਟ ਕਰੋ ਜੋ ਤੁਹਾਨੂੰ ਆਪਣੇ ਡੇਟਾ ਨੂੰ ਇੰਪੋਰਟ ਕਰਨ ਅਤੇ ਵਿਜ਼ੁਅਲ ਬਣਾਉਣ ਲਈ ਲੋੜੀਂਦੇ ਹਨ, `SMOTE` ਨੂੰ `imblearn` ਤੋਂ ਵੀ ਇੰਪੋਰਟ ਕਰੋ।

    ```python
    import pandas as pd
    import matplotlib.pyplot as plt
    import matplotlib as mpl
    import numpy as np
    from imblearn.over_sampling import SMOTE
    ```

    ਹੁਣ ਤੁਸੀਂ ਅਗਲੇ ਕਦਮ ਵਿੱਚ ਡੇਟਾ ਨੂੰ ਇੰਪੋਰਟ ਕਰਨ ਲਈ ਸੈਟਅੱਪ ਹੋ।

1. ਅਗਲਾ ਕੰਮ ਡੇਟਾ ਨੂੰ ਇੰਪੋਰਟ ਕਰਨਾ ਹੋਵੇਗਾ:

    ```python
    df  = pd.read_csv('../data/cuisines.csv')
    ```

   `read_csv()` ਦੀ ਵਰਤੋਂ _cusines.csv_ ਫਾਈਲ ਦੀ ਸਮੱਗਰੀ ਨੂੰ ਪੜ੍ਹੇਗੀ ਅਤੇ ਇਸ ਨੂੰ ਵੈਰੀਏਬਲ `df` ਵਿੱਚ ਰੱਖੇਗੀ।

1. ਡੇਟਾ ਦੇ ਆਕਾਰ ਦੀ ਜਾਂਚ ਕਰੋ:

    ```python
    df.head()
    ```

   ਪਹਿਲੇ ਪੰਜ ਪੰਕਤਾਂ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦੇ ਹਨ:

    ```output
    |     | Unnamed: 0 | cuisine | almond | angelica | anise | anise_seed | apple | apple_brandy | apricot | armagnac | ... | whiskey | white_bread | white_wine | whole_grain_wheat_flour | wine | wood | yam | yeast | yogurt | zucchini |
    | --- | ---------- | ------- | ------ | -------- | ----- | ---------- | ----- | ------------ | ------- | -------- | --- | ------- | ----------- | ---------- | ----------------------- | ---- | ---- | --- | ----- | ------ | -------- |
    | 0   | 65         | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
    | 1   | 66         | indian  | 1      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
    | 2   | 67         | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
    | 3   | 68         | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 0      | 0        |
    | 4   | 69         | indian  | 0      | 0        | 0     | 0          | 0     | 0            | 0       | 0        | ... | 0       | 0           | 0          | 0                       | 0    | 0    | 0   | 0     | 1      | 0        |
    ```

1. ਇਸ ਡੇਟਾ ਬਾਰੇ ਜਾਣਕਾਰੀ ਪ੍ਰਾਪਤ ਕਰਨ ਲਈ `info()` ਕਾਲ ਕਰੋ:

    ```python
    df.info()
    ```

    ਤੁਹਾਡਾ ਆਉਟਪੁੱਟ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦਾ ਹੈ:

    ```output
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2448 entries, 0 to 2447
    Columns: 385 entries, Unnamed: 0 to zucchini
    dtypes: int64(384), object(1)
    memory usage: 7.2+ MB
    ```

## ਅਭਿਆਸ - ਖਾਣਿਆਂ ਬਾਰੇ ਸਿੱਖਣਾ

ਹੁਣ ਕੰਮ ਹੋਰ ਦਿਲਚਸਪ ਹੋਣਾ ਸ਼ੁਰੂ ਹੁੰਦਾ ਹੈ। ਆਓ ਖਾਣੇ ਦੇ ਅਨੁਸਾਰ ਡੇਟਾ ਦੇ ਵੰਡਨ ਦੀ ਖੋਜ ਕਰੀਏ।

1. `barh()` ਕਾਲ ਕਰਕੇ ਡੇਟਾ ਨੂੰ ਬਾਰਾਂ ਵਜੋਂ ਪਲਾਟ ਕਰੋ:

    ```python
    df.cuisine.value_counts().plot.barh()
    ```

    ![ਖਾਣੇ ਦੇ ਡੇਟਾ ਦਾ ਵੰਡ](../../../../translated_images/cuisine-dist.d0cc2d551abe5c25f83d73a5f560927e4a061e9a4560bac1e97d35682ef3ca6d.pa.png)

    ਖਾਣੇ ਦੀ ਗਿਣਤੀ ਸੀਮਿਤ ਹੈ, ਪਰ ਡੇਟਾ ਦਾ ਵੰਡ ਅਸਮਾਨ ਹੈ। ਤੁਸੀਂ ਇਸ ਨੂੰ ਠੀਕ ਕਰ ਸਕਦੇ ਹੋ! ਇਸ ਨੂੰ ਠੀਕ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ, ਹੋਰ ਖੋਜ ਕਰੋ।

1. ਪਤਾ ਕਰੋ ਕਿ ਹਰ ਖਾਣੇ ਲਈ ਕਿੰਨਾ ਡੇਟਾ ਉਪਲਬਧ ਹੈ ਅਤੇ ਇਸ ਨੂੰ ਪ੍ਰਿੰਟ ਕਰੋ:

    ```python
    thai_df = df[(df.cuisine == "thai")]
    japanese_df = df[(df.cuisine == "japanese")]
    chinese_df = df[(df.cuisine == "chinese")]
    indian_df = df[(df.cuisine == "indian")]
    korean_df = df[(df.cuisine == "korean")]
    
    print(f'thai df: {thai_df.shape}')
    print(f'japanese df: {japanese_df.shape}')
    print(f'chinese df: {chinese_df.shape}')
    print(f'indian df: {indian_df.shape}')
    print(f'korean df: {korean_df.shape}')
    ```

    ਆਉਟਪੁੱਟ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦਾ ਹੈ:

    ```output
    thai df: (289, 385)
    japanese df: (320, 385)
    chinese df: (442, 385)
    indian df: (598, 385)
    korean df: (799, 385)
    ```

## ਸਮੱਗਰੀਆਂ ਦੀ ਖੋਜ

ਹੁਣ ਤੁਸੀਂ ਡੇਟਾ ਵਿੱਚ ਹੋਰ ਗਹਿਰਾਈ ਵਿੱਚ ਖੋਜ ਕਰ ਸਕਦੇ ਹੋ ਅਤੇ ਸਿੱਖ ਸਕਦੇ ਹੋ ਕਿ ਹਰ ਖਾਣੇ ਲਈ ਆਮ ਸਮੱਗਰੀਆਂ ਕੀ ਹਨ। ਤੁਸੀਂ ਮੁੜ-ਮੁੜ ਆਉਣ ਵਾਲੇ ਡੇਟਾ ਨੂੰ ਸਾਫ਼ ਕਰਨਾ ਚਾਹੁੰਦੇ ਹੋ ਜੋ ਵੱਖ-ਵੱਖ ਖਾਣਿਆਂ ਵਿੱਚ ਗੁੰਝਲ ਪੈਦਾ ਕਰਦਾ ਹੈ, ਤਾਂ ਆਓ ਇਸ ਸਮੱਸਿਆ ਬਾਰੇ ਸਿੱਖੀਏ।

1. Python ਵਿੱਚ ਇੱਕ ਫੰਕਸ਼ਨ `create_ingredient()` ਬਣਾਓ ਜੋ ਇੱਕ ਸਮੱਗਰੀ ਡੇਟਾਫਰੇਮ ਬਣਾਏ। ਇਹ ਫੰਕਸ਼ਨ ਇੱਕ ਅਣਉਪਯੋਗ ਕਾਲਮ ਨੂੰ ਡ੍ਰਾਪ ਕਰਕੇ ਸ਼ੁਰੂ ਕਰੇਗਾ ਅਤੇ ਗਿਣਤੀ ਦੇ ਅਨੁਸਾਰ ਸਮੱਗਰੀਆਂ ਨੂੰ ਸੌਰਟ ਕਰੇਗਾ:

    ```python
    def create_ingredient_df(df):
        ingredient_df = df.T.drop(['cuisine','Unnamed: 0']).sum(axis=1).to_frame('value')
        ingredient_df = ingredient_df[(ingredient_df.T != 0).any()]
        ingredient_df = ingredient_df.sort_values(by='value', ascending=False,
        inplace=False)
        return ingredient_df
    ```

   ਹੁਣ ਤੁਸੀਂ ਇਸ ਫੰਕਸ਼ਨ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਹਰ ਖਾਣੇ ਲਈ ਸਭ ਤੋਂ ਪ੍ਰਸਿੱਧ ਦਸ ਸਮੱਗਰੀਆਂ ਦਾ ਅੰਦਾਜ਼ਾ ਲਗਾ ਸਕਦੇ ਹੋ।

1. `create_ingredient()` ਕਾਲ ਕਰੋ ਅਤੇ `barh()` ਕਾਲ ਕਰਕੇ ਇਸ ਨੂੰ ਪਲਾਟ ਕਰੋ:

    ```python
    thai_ingredient_df = create_ingredient_df(thai_df)
    thai_ingredient_df.head(10).plot.barh()
    ```

    ![ਥਾਈ](../../../../translated_images/thai.0269dbab2e78bd38a132067759fe980008bdb80b6d778e5313448dbe12bed846.pa.png)

1. ਜਪਾਨੀ ਡੇਟਾ ਲਈ ਵੀ ਇਹੀ ਕਰੋ:

    ```python
    japanese_ingredient_df = create_ingredient_df(japanese_df)
    japanese_ingredient_df.head(10).plot.barh()
    ```

    ![ਜਪਾਨੀ](../../../../translated_images/japanese.30260486f2a05c463c8faa62ebe7b38f0961ed293bd9a6db8eef5d3f0cf17155.pa.png)

1. ਹੁਣ ਚੀਨੀ ਸਮੱਗਰੀਆਂ ਲਈ:

    ```python
    chinese_ingredient_df = create_ingredient_df(chinese_df)
    chinese_ingredient_df.head(10).plot.barh()
    ```

    ![ਚੀਨੀ](../../../../translated_images/chinese.e62cafa5309f111afd1b54490336daf4e927ce32bed837069a0b7ce481dfae8d.pa.png)

1. ਭਾਰਤੀ ਸਮੱਗਰੀਆਂ ਨੂੰ ਪਲਾਟ ਕਰੋ:

    ```python
    indian_ingredient_df = create_ingredient_df(indian_df)
    indian_ingredient_df.head(10).plot.barh()
    ```

    ![ਭਾਰਤੀ](../../../../translated_images/indian.2c4292002af1a1f97a4a24fec6b1459ee8ff616c3822ae56bb62b9903e192af6.pa.png)

1. ਆਖਿਰਕਾਰ, ਕੋਰੀਆਈ ਸਮੱਗਰੀਆਂ ਨੂੰ ਪਲਾਟ ਕਰੋ:

    ```python
    korean_ingredient_df = create_ingredient_df(korean_df)
    korean_ingredient_df.head(10).plot.barh()
    ```

    ![ਕੋਰੀਆਈ](../../../../translated_images/korean.4a4f0274f3d9805a65e61f05597eeaad8620b03be23a2c0a705c023f65fad2c0.pa.png)

1. ਹੁਣ, ਵੱਖ-ਵੱਖ ਖਾਣਿਆਂ ਵਿੱਚ ਗੁੰਝਲ ਪੈਦਾ ਕਰਨ ਵਾਲੀਆਂ ਸਭ ਤੋਂ ਆਮ ਸਮੱਗਰੀਆਂ ਨੂੰ `drop()` ਕਾਲ ਕਰਕੇ ਹਟਾਓ:

   ਹਰ ਕੋਈ ਚਾਵਲ, ਲਸਣ ਅਤੇ ਅਦਰਕ ਨੂੰ ਪਸੰਦ ਕਰਦਾ ਹੈ!

    ```python
    feature_df= df.drop(['cuisine','Unnamed: 0','rice','garlic','ginger'], axis=1)
    labels_df = df.cuisine #.unique()
    feature_df.head()
    ```

## ਡੇਟਾਸੈਟ ਨੂੰ ਸੰਤੁਲਿਤ ਕਰੋ

ਹੁਣ ਜਦੋਂ ਤੁਸੀਂ ਡੇਟਾ ਨੂੰ ਸਾਫ਼ ਕਰ ਲਿਆ ਹੈ, [SMOTE](https://imbalanced-learn.org/dev/references/generated/imblearn.over_sampling.SMOTE.html) - "Synthetic Minority Over-sampling Technique" - ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਇਸ ਨੂੰ ਸੰਤੁਲਿਤ ਕਰੋ।

1. `fit_resample()` ਕਾਲ ਕਰੋ, ਇਹ ਰਣਨੀਤੀ ਇੰਟਰਪੋਲੇਸ਼ਨ ਦੁਆਰਾ ਨਵੇਂ ਨਮੂਨੇ ਬਣਾਉਂਦੀ ਹੈ।

    ```python
    oversample = SMOTE()
    transformed_feature_df, transformed_label_df = oversample.fit_resample(feature_df, labels_df)
    ```

    ਡੇਟਾ ਨੂੰ ਸੰਤੁਲਿਤ ਕਰਕੇ, ਤੁਹਾਨੂੰ ਇਸ ਨੂੰ ਕਲਾਸੀਫਾਈ ਕਰਨ ਵੇਲੇ ਵਧੀਆ ਨਤੀਜੇ ਮਿਲਣਗੇ। ਇੱਕ ਬਾਈਨਰੀ ਕਲਾਸੀਫਿਕੇਸ਼ਨ ਬਾਰੇ ਸੋਚੋ। ਜੇ ਤੁਹਾਡੇ ਡੇਟਾ ਦਾ ਜ਼ਿਆਦਾਤਰ ਹਿੱਸਾ ਇੱਕ ਕਲਾਸ ਹੈ, ਤਾਂ ਇੱਕ ML ਮਾਡਲ ਉਸ ਕਲਾਸ ਦੀ ਵਧੇਰੇ ਪੇਸ਼ਗੂਈ ਕਰੇਗਾ, ਸਿਰਫ਼ ਇਸ ਲਈ ਕਿ ਇਸ ਲਈ ਹੋਰ ਡੇਟਾ ਉਪਲਬਧ ਹੈ। ਡੇਟਾ ਨੂੰ ਸੰਤੁਲਿਤ ਕਰਨਾ ਕਿਸੇ ਵੀ ਤਰ੍ਹਾਂ ਦੇ ਡੇਟਾ ਨੂੰ ਲੈ ਕੇ ਇਸ ਅਸਮਾਨਤਾ ਨੂੰ ਹਟਾਉਣ ਵਿੱਚ ਮਦਦ ਕਰਦਾ ਹੈ।

1. ਹੁਣ ਤੁਸੀਂ ਹਰ ਸਮੱਗਰੀ ਲਈ ਲੇਬਲਾਂ ਦੀ ਗਿਣਤੀ ਦੀ ਜਾਂਚ ਕਰ ਸਕਦੇ ਹੋ:

    ```python
    print(f'new label count: {transformed_label_df.value_counts()}')
    print(f'old label count: {df.cuisine.value_counts()}')
    ```

    ਤੁਹਾਡਾ ਆਉਟਪੁੱਟ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦਾ ਹੈ:

    ```output
    new label count: korean      799
    chinese     799
    indian      799
    japanese    799
    thai        799
    Name: cuisine, dtype: int64
    old label count: korean      799
    indian      598
    chinese     442
    japanese    320
    thai        289
    Name: cuisine, dtype: int64
    ```

    ਡੇਟਾ ਸੁੰਦਰ, ਸਾਫ਼, ਸੰਤੁਲਿਤ ਅਤੇ ਬਹੁਤ ਹੀ ਸੁਆਦਿਸ਼ਟ ਹੈ!

1. ਆਖਰੀ ਕਦਮ ਇਹ ਹੈ ਕਿ ਸੰਤੁਲਿਤ ਡੇਟਾ, ਲੇਬਲਾਂ ਅਤੇ ਫੀਚਰਾਂ ਸਮੇਤ, ਨੂੰ ਇੱਕ ਨਵੇਂ ਡੇਟਾਫਰੇਮ ਵਿੱਚ ਸੇਵ ਕਰੋ ਜੋ ਇੱਕ ਫਾਈਲ ਵਿੱਚ ਐਕਸਪੋਰਟ ਕੀਤਾ ਜਾ ਸਕੇ:

    ```python
    transformed_df = pd.concat([transformed_label_df,transformed_feature_df],axis=1, join='outer')
    ```

1. ਤੁਸੀਂ `transformed_df.head()` ਅਤੇ `transformed_df.info()` ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਡੇਟਾ ਨੂੰ ਇੱਕ ਵਾਰ ਹੋਰ ਦੇਖ ਸਕਦੇ ਹੋ। ਭਵਿੱਖ ਦੇ ਪਾਠਾਂ ਵਿੱਚ ਵਰਤੋਂ ਲਈ ਇਸ ਡੇਟਾ ਦੀ ਇੱਕ ਕਾਪੀ ਸੇਵ ਕਰੋ:

    ```python
    transformed_df.head()
    transformed_df.info()
    transformed_df.to_csv("../data/cleaned_cuisines.csv")
    ```

    ਇਹ ਤਾਜ਼ਾ CSV ਹੁਣ ਰੂਟ ਡੇਟਾ ਫੋਲਡਰ

---

**ਅਸਵੀਕਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੱਜੇਪਣ ਹੋ ਸਕਦੇ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼, ਜੋ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਹੈ, ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।