# DADS7202_HW02 The pre-trained CNN

## Project title:



## Introduction: 

Nowadays there are a lot of mobile phones in the market there has a lot of unique function for their brand however the appearance of mobile phone are very the same make the customer very confused when they try to find a phone that they want "which one is the right one that I want?" or "Is this the phone that I'm looking for?" there is the most question when customer try to find the phone because when search mobile phone on Google sometime the picture that comes up looks like the brand that search but it isn't because of this problem our team come with the idea "Classification of mobile phone brand" to classified the picture of mobile phone which one is which brand from our discussion we choose 4 mobile phone's brand that we think it's easy to confuse and hard to tell which brand is the right one.

There are a lot of mobile phones in the market but **the appearance of every mobile phone are look the same** make it's hard for the customer to find a phone that they want.  even the photo of the phone on Google sometime the picture that comes up looks like the brand that search but it isn't. **Because of this problem our team come with the idea** **`"Classification of mobile phone brand"`** to classified the picture of mobile phone which one is which brand

* 📱 **`Apple (iPhone)`**                      
* 📱 **`Samsung`**
* 📱 **`OPPO`**                              
* 📱 **`Huawei`**


## Dataset
Link to download the dataset: https://drive.google.com/drive/folders/16B2ut6co3qQ1eBGqpvZMb8ZJNta62rp4?usp=sharing
How to labeling data?


## Assumption:

## Data pre-processing and splitting :
In the process, all images were converted to .jpg files and manually extracted into sub-folders separate by brand. Then, we resized the images by running tf.keras.preprocessing.image.load_img() function for loading the images with different heights and widths into PIL format, sizing 224 x 224 pixels as CNN models expect such a target size. A PIL Image instance was then converted to a Numpy array using tf.keras.preprocessing.image.img_to_array() function, returning a 3D Numpy array (501, 224, 224, 3). Last step, we also needed to run the images through a preprocess input function of the models we have used, such as tf.keras.applications.efficientnet.preprocess_input() for preprocessing the NumPy array encoding a batch of images.

## Data Augmentation :


How to split train/test set? manual or method?

## Pre-train model:
จุดที่ Fine Tuning ได้

1. รูปแบบ Data Aug layer
2. Feature extraction
2.1 แก้ freeze ของ pre-train
2.2 เพิ่ม Convolution / pooling ต่อจาก pre-train
3. เพิ่ม/ปรับ Classifier layer


## Comparison performance:

1.VGG16

2.Mobilenet

3.inception-V3



## Training:




## Results:



## Discussion:
1.session crash due to ran out of RAM
![MicrosoftTeams-image (10)](https://user-images.githubusercontent.com/107410157/196458197-d0e59956-51d9-4be5-8566-edc6683d903c.png)



## Conclusion:



## References:



## 🙋 Deepsleep's Member:
| %|ID|Name |Responsibility  |
| :------ | ------ |:------|:-------|
|⭐ **`20%`** | **`6410414007`**  | 👦 Athit Santikarn  |**`Collect data(Oppo)`**, **`Write result`**, **`conclusion report`**|
|⭐ **`20%`** | **`6410422020`**  | 👩 Suphanun Sukamta |**`Collect data(Samsung)`**, **`Write result`**, **`conclusion report`**|
|⭐ **`20%`** | **`6410422004`**  | 👦 Chokchai Kenpho  |**`Collect data(Apple)`**, **`Train model-VGG16`**|
|⭐ **`20%`** | **`6410422009`**  | 👦 Noppol Anakpluek  |**`Preprocess data`**, **`Train model-ResNet152V2`**|
|⭐ **`20%`** | **`6420422006`**  | 👦 Watcharakorn Pasanta  | **`Collect data(Huawei)`**, **`Train model-MobileNet`**|


## End credit: 
This project is a part of Course DADS7202 Deep Learning, Data Analytics and Data Science, NIDA.


Note : การเขียนรายงาน HW02

-ให้เครดิตที่มาของภาพ dataset

-เป็น dataset ที่ pre-train ยังทำงานได้ไม่ดี

-ต้องเปรียบเทียบอย่างน้อย 3 backbone(feature extracter) สำหรับกลุ่มที่เลือกทำหัวข้อ classifier

เช่น เปลี่ยนจาก VGG เป็น efficientDet แล้วสรุปผลเปรียบเทียบ

(เพราะการเปลี่ยน backbone จะเป็นจุดเปลี่ยนประสิทธิภาพของผลลัพธ์ได้ง่ายที่สุดและได้ผลดีที่สุด)

-สรุปผลรายงาน ให้มีผลของการทำ pre-train ด้วยว่า ผลก่อน fine-tune เป็นอย่างไร แล้วผลหลัง fune-tune เป็นอย่างไร
