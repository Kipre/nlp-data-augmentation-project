# NLP Data Augmentation Project

__Blachier, M'Bida, Qohafa, Beye & Neverov__

## Intoduction

Data augmentation is a very common practice in deep learning, especially is computer vision. 
Since there are a few simple transformations that can be done to images without modifying the label, it is quite common to multiply the total amout of training data by a factor of two or three. 
Those simple transformations can be color modifications, slight rotations, mirrorings, croppings and more, as long as they are label invariant (for example flipping over an image of a 9 is not label invariant in a digit recognition task).

![Data augmentation](https://i2.wp.com/deeplylearning.fr/wp-content/uploads/2018/09/data-augmentation-sur-image.png?resize=801%2C335&ssl=1)

But what about data augmentation for NLP tasks?