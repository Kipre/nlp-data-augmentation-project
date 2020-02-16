# NLP Data Augmentation Project

__February 2020 -- Blachier, M'Bida, Qohafa, Beye & Neverov__

## Intoduction

Data augmentation is a very common practice in deep learning, especially is computer vision. 
Since there are a few simple transformations that can be done to images without modifying the label, it is quite common to multiply the total amout of training data by a factor of two or three. 
Those simple transformations can be color modifications, slight rotations, mirrorings, croppings and more, as long as they are label invariant (for example flipping over an image of a 9 is not label invariant in a digit recognition task).

![Data augmentation](https://i2.wp.com/deeplylearning.fr/wp-content/uploads/2018/09/data-augmentation-sur-image.png?resize=801%2C335&ssl=1)

But what about data augmentation for NLP tasks?
As opposed to images, words, sentences and text in general can be very easily corrupted with very small modifications.
There are a few ways to augment NLP data but the task seems to be far more complicated.
Some common ways might include:

 - Probabilistic Context Free Grammars with pattern to generate text;

 - Text generation with Language Models;

 - EDA: easy data augmentation techniques (consists of four simple but powerful operations: synonym replacement, random insertion, random swap, and random deletion)[1];

 - Replacing using word embedding similarity;

 - Back translations.

 We decided to focus on the last one: back translation.

## Back translation

This approach has the advantage of being extermely easy to implement. 
The whole code required to run the data augmentation holds on less than 50 lines of code and consists of a few POST requests. 
It consists of translating our example to a foreign language and then translating it back to our language.
This allows us to use the elaborate language structures learned by the state of the art machine translators (Google Translate, Microsoft Azure and others) and apply them to our phrases to generate semantically invariant examples. 
Here are some of the most common APIs:

 - [Google Translate API](https://cloud.google.com/translate/docs)
 - [Microsoft Translation API](https://azure.microsoft.com/fr-fr/services/cognitive-services/translator-text-api/)
 - [Yandex Translate API](https://tech.yandex.com/translate/)
 - [IBM Watson Language Translator API](https://cloud.ibm.com/apidocs/language-translator/language-translator)

Of course this sounds better than it actually is, the main disadvantage of this method is that it is not (completely) free. 
The pricings range from 15$ per 1 million characters and cheaper as the volume increases. 
For example for our problem we needed to translate a corpus of approximately 150000 characters which doesn't soud like a lot but since the method requieres 2 x 9 requests per example (forward and backward translation for each of the 9 languages we selected).
For this reasont it is preferable to have access to a service with at lest 2M characters available.

Here is a review of the free services we identified:

|Provider|Free limit|Commentary|
|--------|----------|----------|
|Microsoft Azure| 2M characters/month | We were not able tu run the service|
|Yandex Translate| 1M characters/24h | Worked great |
|Goslate (Unofficial Google)| ? | Works quickly but reaches the limit quickly as well|

This is not an exhaustive list of the free services but those are the ones we identified as more reliable/easier to use.

It is important to note that we paralelized the workflow to match the allowances per ip adress/api key. For example while some of us are translating on one service, others use another but using only a subset of the 9 languages so that the total number of characters is lower than the daily limit. 

## Quality

In this section we will present some raw results to give an idea about what the backtranslated phrases might look like.

## Results

In this section we present quantitative results.

| Setting | Accuracy | F1 (micro) |
|--|--|--|
| Baseline data | 0.937 +- 0.065 | 0.938 +- 0.066 |
| Augmented data (6 languages) | 0.988 +- 0.015 | 0.988 +- 0.015 |

The first run was made using the provided evaluation code but using only 10 epochs. 
The second was done using the `test.txt` and `dev.txt` from the first run and only the `train.txt` was changed in each split so that it contains exclusively backtranslated sentences.

As we were expecting the augmented data enhanced our model but we still have lots of doubts about how representative of the reality those results are.
One of the reasons of such a difference might be that repetitiveness of the sentences leads to overfitting. 

## Conclusion

In this work we were able to augment our dataset by a factor of 6 thus proving that our approach is interesting.

## Bibliography

1. Jason Wei and Kai Zou, EDA: Easy Data Augmentation Techniques for Boosting Performance on Text Classification Tasks, 2019, arXiv.com/1901.11196