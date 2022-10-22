# DADS7202_HW02 The pre-trained CNN
![image](https://user-images.githubusercontent.com/107410157/197267919-ac58b7ea-f75d-4610-9408-eb14e26ceb85.png)

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

เราได้ทำการเก็บรูปโทรศัพท์มือถือทั้ง 4 ยี่ห้อ ได้แก่ Apple(iPhone), Huawei, OPPO และ Samsung ที่มีวางจำหน่ายในปัจจุบัน (ปี 2022) โดยเลือกเก็บรูปถ่ายในหลากหลายมุมมอง ทั้งด้านหน้า ด้านหลัง ด้านข้าง รูปเฉาพส่วน เช่น ส่วนกล้องถ่ายรูป โดยแหล่งที่เก็บเราได้เก็บมาจาก official page BaNANA online shop **`"https://www.bnn.in.th/th"`** และ unofficial page (Facebook market place) เพื่อให้ข้อมูล คุณภาพของภาพมีความหลากหลาย รวมทั้งหมด 434 ภาพ โดยแบ่งเป็น iPhone 100 ภาพ, Huawei 125 ภาพ, OPPO 109 ภาพ และ Samsung 100 ภาพ.


## Assumption:
ในการศึกษาครั้งนี้ เราคาดว่าโทรศัพท์มือถือรูปแบบในปัจจุบัน pre-trained model ที่ validation บน ImageNet dataset น่าจะยังไม่รู้จักในระดับที่สามารถแยกยี่ห้อได้ เราจึงเลือก model มา 3 model โดยพิจารณาจาก size และ parameter แบ่งเป็น ขนาด ใหญ่ กลาง และ เล็ก โดย model ที่เลือกได้แก่ **`"VGG16"`**, **`"ResNet152V2"`** และ **`"MobileNet"`** ตามลำดับ โดยเราคาดว่า โมเดลที่มีขนาดใหญ่ที่สุด คือ VGG16 จะให้ผล accuracy ที่ดีที่สุด

## Data pre-processing and splitting :
 * ในการเตรียมข้อมูลรูปภาพ เราจัดเก็บรูปภาพทั้งหมด เป็น file .jpg จากนั้นใช้วิธีการ manual จัดเก็บแบ่งตาม folder ชื่อยี่ห้อ และ แยกเป็น 2 ส่วน คือ train_ds และ test_ds โดยแบ่งสัดส่วนของ train, validation และ test ตามรายละเอียดในตารางที่ 1
* ทำการ label class ของยี่ห้อ เรียงตามลำดับตัวอักษร โดย 'apple' คือ class 0 และ 'samsung' คือ class 3 ตามลำดับ
* ทำการ resize โดย กำหนด input_shape = (224, 224, 3)
![image](https://user-images.githubusercontent.com/107410157/197308226-29a91b68-5a4d-467e-9e3f-402624fc36fa.png)


**Table 1: Data pre-processing and splitting**
![image](https://user-images.githubusercontent.com/107410157/197307356-859c04f9-4520-4d96-b5c8-3c1c3124ba5d.png)



## ฺBefore Fine-tuning:
ในการศึกษาครั้งนี้ ผลของ pre-train model ก่อน fine-tuning พบว่า ทั้ง 3 model (**`"VGG16"`**, **`"ResNet152V2"`** , **`"MobileNet"`**) ให้ค่า Accuracy = 0 นั่นหมายความว่า pre-train model ทั้ง 3 ไม่สามารถจำแนกยี่ห้อของโทรศัพท์ตามที่เราต้องการศึกษาได้ โดยผลของการ prediction มีการทำนาย iPhone ว่าเป็น projector, ทำนาย Huawei ว่าเป็น ipod, ทำนาย Oppo ว่าเป็น switch, ทำนาย Samsung ว่าเป็น notebook เป็นต้น

**Table 2: Result before fine-tuning**
| Model |Test Accuracy | Test Loss | Runtime with GPU (H:M:S) | GPU Name |
| :------ | :----: |:-----:|:-----:|:-----:|
|**`"VGG16"`**| 0 | 18.2531 | 0:02:41 | Tesla T4
|**`"MobileNet"`**| 0 | 13.3670 | 0:02:41 | Tesla T4
|**`"ResNet152V2"`**| 0 | 2508.23 | 0:03:10 | Tesla T4

ผลการทายของแต่ละโมเดล 
![image](https://user-images.githubusercontent.com/107410157/197308600-4f872a6d-8f47-4f41-93e9-aa1666180ce1.png)


## Data Augmentation :
เราได้มีการทำ Data augmentation เพื่อให้ ......... โดยแต่ละ model เลือกใช้วิธีการทำ augmentation แตกต่างกันไป ดังตารางที่ 3

**Table 3: Data Augmentation**
| Model         | Image data augmentation                     |
| ------------- |---------------------------------------------|
| VGG16         |tf.keras.layers.RandomFlip                   |
|               |tf.keras.layers.RandomTranslation            |
| MobileNet     |tf.keras.layers.RandomFlip                   |
|               |tf.keras.layers.RandomRotation               |
| ResNet152V2   |tf.keras.layers.RandomFlip                   |
|               |tf.keras.layers.RandomTranslation            |
|               |tf.keras.layers.RandomRotation               |

## After Fine-tuning:

เราได้ทำการปรับจูนพารามิเตอร์ เพิ่มเติมจาก pre-trained model จนได้ค่า accuracy ที่ดีขึ้น ด้วยการปรับพารามิเตอร์ต่างๆ ดังนี้

**Table 4: Fine-tuning parameters**
| Model | epoc | Feature extractor | Feature classifier | Optimizer | learning rate |
| :------ | :----: |:-----:|:-----:|:-----:|:-----:|
|**`"VGG16"`**|15|Conv2D : 3 Layer|activation="relu" & "tanh"|Adam|0.0001|
|**`"MobileNet"`**|100|'all trainable|activation="relu" & Dropout =0.5|Adam|0.0001|
|**`"ResNet152V2"`**|30|'all trainable|activation="relu" & Dropout =0.2|Adam|0.0001|

ผลของการรัน 5 รอบของทั้ง 3 โมเดลหลังจากการ Fine-tuning พบว่าที่ 3 โมเดลสามารถทายชื่อแบรนด์ของโทรศัพท์ได้ ซึ่งมีค่าความถูกต้องต่างกันไปในแต่ละ model ดังตารางที่ 5

**Table 5: Result after fine-tuning**
| Model | AVG. Test Accuracy | SD Test Accuracy | AVG. Test Loss | SD Test Loss | AVG. Runtime with GPU (H:M:S) |
| :------ | :----: |:-----:|:-----:|:-----:|:-----:|
|**`"VGG16"`**|0.730|±0.0167|0.715|±0.0749|0:02:50|
|**`"MobileNet"`**|0.870|±0.0313|0.631|±0.1281|0:07:14|
|**`"ResNet152V2"`**|0.795|±0.0447|0.873|±0.1333|0:02:46|

ผลของการทายของแต่ละโมลเดล โดยชื่อของ class คือ Actual brand - Predict Brand
 - **`"VGG16"`**
 
 ![image](https://user-images.githubusercontent.com/86920208/197242106-bb7c47f0-7009-4ee4-82c2-57f7f319bed3.png)
 
 - **`"MobileNet"`**
 
 ![image](https://user-images.githubusercontent.com/86920208/197242438-267ffb37-8307-46c2-bd21-ed170df14ac1.png)

 - **`"ResNet152V2"`**
 
![image](https://user-images.githubusercontent.com/86920208/197242572-f5c2f464-fd14-4cd0-92f8-9e95d1ce9f93.png)




## Results:


![30](https://user-images.githubusercontent.com/86920208/197248454-7298a1a3-ea89-4a58-9083-41f02d71bc38.png)




## Discussion:
1.session crash due to ran out of RAM (ต้องใช้ resource มาก)
![MicrosoftTeams-image (10)](https://user-images.githubusercontent.com/107410157/196458197-d0e59956-51d9-4be5-8566-edc6683d903c.png)

2.การเพิ่มจำนวนรูปภาพในการ Train ไม่ได้ทำให้ประสิทธิผลของ Model เพิ่มขึ้นอย่างมีนัยสำคัญ,  การ split มีผล ความหลากหลายของรูปภาพใน train/test set


## Conclusion:



## References:
* https://keras.io/api/applications/


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

1. รูปแบบ Data Aug layer
2. Feature extraction
2.1 แก้ freeze ของ pre-train
2.2 เพิ่ม Convolution / pooling ต่อจาก pre-train
3. เพิ่ม/ปรับ Classifier layer
Note : การเขียนรายงาน HW02

-ให้เครดิตที่มาของภาพ dataset

-เป็น dataset ที่ pre-train ยังทำงานได้ไม่ดี

-ต้องเปรียบเทียบอย่างน้อย 3 backbone(feature extracter) สำหรับกลุ่มที่เลือกทำหัวข้อ classifier

เช่น เปลี่ยนจาก VGG เป็น efficientDet แล้วสรุปผลเปรียบเทียบ

(เพราะการเปลี่ยน backbone จะเป็นจุดเปลี่ยนประสิทธิภาพของผลลัพธ์ได้ง่ายที่สุดและได้ผลดีที่สุด)

-สรุปผลรายงาน ให้มีผลของการทำ pre-train ด้วยว่า ผลก่อน fine-tune เป็นอย่างไร แล้วผลหลัง fune-tune เป็นอย่างไร
