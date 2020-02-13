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



For this  
## Bibliography

1. Jason Wei and Kai Zou, EDA: Easy Data Augmentation Techniques for Boosting Performance on Text Classification Tasks, 2019, arXiv.com/1901.11196