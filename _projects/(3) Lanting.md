---
name: Lanting
tools: [Computer Vision, Machine Learning]
image: https://i.postimg.cc/HLntR0nj/lanting.jpg

description: Lanting is an application that prevent / reduce stunting cases in Indonesia by controlling the adequacy of nutritional needs for the body via application.
---

# Overview

![](https://i.postimg.cc/HLntR0nj/lanting.jpg)

#### Dataset
Because we use YoLoV3 to process images, we create our own dataset by looking for images that contain more than 2 objects in 1 image. then we give the image a label based on the object in each image. We make 7 classes namely:
1. white rice
2. boiled eggs
3. fried chicken
4. stir-fried kale
5. avocado
6. banana
7. papaya


##### Model



{% include elements/button.html link="https://github.com/muhzulfik/bangkit-capstone" text="Project Github Repo (Machine Learning + Cloud Computing" block=true %}
{% include elements/button.html link="https://github.com/fhrii/lanting" text="Project Github Repo (Mobile Developer" block=true %}