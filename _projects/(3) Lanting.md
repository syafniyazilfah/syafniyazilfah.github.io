---
name: Lanting
tools: [YoLoV3, Machine Learning]
image: https://i.postimg.cc/qq2xVnYK/lantingg.jpg

description: Lanting is an application that prevent / reduce stunting cases in Indonesia by controlling the adequacy of nutritional needs for the body via application.
---

### Overview

![](https://i.postimg.cc/qq2xVnYK/lantingg.jpg)

This project is the capstone project of the Awakening program held by the Ministry of Education and Culture in collaboration with Gojek, Google, Tokopedia and Traveloka.
Lanting was carried out by 6 people:

1. Fahri Ahmad Fachrudin (Mobile Developer, UX Designer)
2. Fitria Urbach (Machine Learning)
3. Hafifsyah Rifaldi (Cloud Computing)
4. Syafniya Zilfah Aniesiy (Machine Learning, UI Designer, Illustrator)
5. Muhammad Zulfikri (Cloud Computing)
6. Firli Subhi Ramadani (Mobile Developer)

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
This application uses image processing using the YoLoV3 model with 7 classes.


#### Project Repo
{% include elements/button.html link="https://github.com/muhzulfik/bangkit-capstone" text="Project Github Repo (Machine Learning + Cloud Computing" block=true %}
{% include elements/button.html link="https://github.com/fhrii/lanting" text="Project Github Repo (Mobile Developer" block=true %}
