# DADS7202_HW02 The pre-trained CNN

# Classification of Mobile phone brand



## Introduction: 

Nowadays there are a lot of mobile phones in the market there has a lot of unique function for their brand however the appearance of mobile phone are very the same make the customer very confused when they try to find a phone that they want "which one is the right one that I want?" or "Is this the phone that I'm looking for?" there is the most question when customer try to find the phone because when search mobile phone on Google sometime the picture that comes up looks like the brand that search but it isn't because of this problem our team come with the idea "Classification of mobile phone brand" to classified the picture of mobile phone which one is which brand from our discussion we choose 4 mobile phone's brand that we think it's easy to confuse and hard to tell which brand is the right one.

There are a lot of mobile phones in the market but **the appearance of every mobile phone are look the same** make it's hard for the customer to find a phone that they want.  even the photo of the phone on Google sometime the picture that comes up looks like the brand that search but it isn't. **Because of this problem our team come with the idea** **`"Classification of mobile phone brand"`** to classified the picture of mobile phone which one is which brand

* 📱 **`Apple (iPhone)`**    
* 📱 **`Huawei`**
* 📱 **`OPPO`**   
* 📱 **`Samsung`**


## 📋 Image Dataset
 - [✨ Dataset](https://drive.google.com/drive/folders/16B2ut6co3qQ1eBGqpvZMb8ZJNta62rp4?usp=sharing) <br>
Link to download the dataset: https://drive.google.com/drive/folders/16B2ut6co3qQ1eBGqpvZMb8ZJNta62rp4?usp=sharing
เราได้ทำการเก็บรูปโทรศัพท์มือถือทั้ง 4 ยี่ห้อ ได้แก่ Apple(iPhone), Huawei, OPPO และ Sumsung ที่มีวางจำหน่ายในปัจจุบัน (ปี 2022) โดยเลือกเก็บรูปถ่ายในหลากหลายมุมมอง ทั้งด้านหน้า ด้านหลัง ด้านข้าง รูปเฉาพส่วน เช่น ส่วนกล้องถ่ายรูป โดยแหล่งที่เก็บเราได้เก็บมาจาก official page BaNANA online shop **`"https://www.bnn.in.th/th"`** และ unofficial page (Facebook market place) เพื่อให้ข้อมูล คุณภาพของภาพมีความหลากหลาย รวมทั้งหมด 434 ภาพ โดยแบ่งเป็น iphone 100 ภาพ, Huawei 125 ภาพ, OPPO 109 ภาพ และ Sumsung 100 ภาพ.


## Assumption:
ในการศึกษาครั้งนี้ เราคาดว่าโทรศัพท์มือถือรูปแบบในปัจจุบัน pre-trained model ที่ validation  บน ImageNet dataset น่าจะยังไม่รู้จักในระดับที่สามารถแยกยี่ห้อได้ เราจึงเลือก model มา 3 model โดยพิจารณาจาก size และ parameter แบ่งเป็น ขนาด ใหญ่ กลาง และ เล็ก โดย model ที่เลือกได้แก่ **`"VGG16"`**, **`"ResNet152V2"`** และ **`"MobileNet"`** ตามลำดับ โดยเราคาดว่า โมเดลที่มีขนาดใหญ่ที่สุด คือ VGG16 จะให้ผล accuracy ที่ดีที่สุด

## Data pre-processing and splitting :
ในการเตรียมข้อมูลรูปภาพ เราจัดเก็บรูปภาพทั้งหมด เป็น file .jpg จากนั้นใช้วิธีการ manual จัดเก็บแบ่งตาม folder ชื่อยี่ห้อ และ แยกเป็น 2 ส่วน คือ train_ds และ test_ds โดยแบ่งสัดส่วนของ train,validationและ test ตามรายละเอียดในตาราง

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

no-tune reult model ทายว่าเป็นอะไรบ้าง



## Discussion:
1.session crash due to ran out of RAM (ต้องใช้ resource มาก)
![MicrosoftTeams-image (10)](https://user-images.githubusercontent.com/107410157/196458197-d0e59956-51d9-4be5-8566-edc6683d903c.png)

2.การเพิ่มจำนวนรูปภาพในการ Train ไม่ได้ทำให้ประสิทธิผลของ Model เพิ่มขึ้นอย่างมีนัยสำคัญ,  การ split มีผล ความหลากหลายของรูปภาพใน train/test set


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
