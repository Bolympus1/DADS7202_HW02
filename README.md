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


## Before Fine-tuning:
ในการศึกษาครั้งนี้ ผลของ pre-train model ก่อน fine-tuning พบว่า ทั้ง 3 model (**`"VGG16"`**, **`"ResNet152V2"`** , **`"MobileNet"`**) ให้ค่า Accuracy = 0 นั่นหมายความว่า pre-train model ทั้ง 3 ไม่สามารถจำแนกยี่ห้อของโทรศัพท์ตามที่เราต้องการศึกษาได้ โดยผลของการ prediction มีการทำนาย iPhone ว่าเป็น projector, ทำนาย Huawei ว่าเป็น ipod, ทำนาย Oppo ว่าเป็น switch, ทำนาย Samsung ว่าเป็น notebook เป็นต้น

**Table 2: Result before fine-tuning**
| Model |Test Accuracy | Test Loss | Runtime with GPU (H:M:S) | GPU Name |
| :------ | :----: |:-----:|:-----:|:-----:|
|**`"VGG16"`**| 0 | 18.2531 | 0:02:41 | Tesla T4
|**`"MobileNet"`**| 0 | 13.3670 | 0:02:41 | Tesla T4
|**`"ResNet152V2"`**| 0 | 2508.23 | 0:03:10 | Tesla T4

ผลการทายของแต่ละโมเดล 
![image](https://user-images.githubusercontent.com/107410157/197340501-6658c397-1659-48f6-bbd2-8c6a4364263e.png)


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
| :------ | :----: |:-----:|--------|:-----:|:-----:|
|**`"VGG16"`**|15|Conv2D : 3 Layer|activation="relu" & "tanh"|Adam|0.0001|
|**`"MobileNet"`**|100|all trainable|activation="relu" & Dropout =0.5|Adam|0.0001|
|**`"ResNet152V2"`**|30|all trainable|activation="relu" & Dropout =0.2|Adam|0.0001|

**Train accuracy/Train loss**
![image](https://user-images.githubusercontent.com/107410157/197338882-ee1b09af-3c49-4c88-a945-29f753e8cb0b.png)

ผลของการรัน 5 รอบของทั้ง 3 โมเดลหลังจากการ Fine-tuning พบว่าที่ 3 โมเดลสามารถทายชื่อแบรนด์ของโทรศัพท์ได้ ซึ่งมีค่าความถูกต้องต่างกันไปในแต่ละ model ดังตารางที่ 5

**Table 5: Result after fine-tuning**
| Model | AVG. Test Accuracy | SD Test Accuracy | AVG. Test Loss | SD Test Loss | AVG. Runtime with GPU (H:M:S) |
| :------ | :----: |:-----:|:-----:|:-----:|:-----:|
|**`"VGG16"`**|0.730|±0.0167|0.715|±0.0749|0:02:50|
|**`"MobileNet"`**|0.870|±0.0313|0.631|±0.1281|0:07:14|
|**`"ResNet152V2"`**|0.795|±0.0447|0.873|±0.1333|0:02:46|

ผลของการทายของแต่ละโมลเดล โดยชื่อของ class คือ Actual brand - Predict Brand
![image](https://user-images.githubusercontent.com/107410157/197340370-b178c8a0-4478-4d77-a95f-2cfe677bb599.png)
![image](https://user-images.githubusercontent.com/107410157/197340236-3596088e-27cb-46c3-9c76-139dc42eed42.png)
![image](https://user-images.githubusercontent.com/107410157/197340204-583dced2-bc65-476a-a6da-c19d97be76ac.png)



## Results:
จาก model ที่เราเลือกมา 3 model พบว่า **`"MobileNet"`** ให้ค่า accuracy ที่ดีที่สุด โดยผลจากการรันแบบ random seed 5 รอบ Test accuracy เฉลี่ยเท่ากับ 87.00% +/-3.13% และ Test loss เฉลี่ยเท่ากับ 63.13% +/-12.81% เวลาที่ใช้ในการ train model บน GPU เฉลี่ยเท่ากับ 7 min 14 sec ซึ่งหากพิจารณาในด้านเวลา **`"MobileNet"`** จะใช้เวลาในการ train มากที่สุด เนื่องด้วยการกำหนดค่า epoc ที่สูงกว่า อีก 2 model และ ข้อจำกัดของการรันบน Colab

![image](https://user-images.githubusercontent.com/107410157/197309429-bc6da6a4-b423-4b94-83ab-ac2f2abe1b16.png)





## Discussion:

จากการศึกษาในครั้งนี้ กลุ่มเราได้สรุปประเด็นที่น่าสนใจในการทำ Deep Learning กับ image dataset ดังนี้

**1. การ train image data ต้องใช้ resource ในการรันอย่างมาก ซึ่งทางกลุ่มพบปัญหาว่าไม่สามารถรันบน local pc ได้เลย เนื่องจาก session crash due to ran out of RAM**

![MicrosoftTeams-image (11)](https://user-images.githubusercontent.com/107410157/197311406-017fbef7-854f-415a-a92b-a6b41c0b95ce.png)

**2. ขนาดของ Model ที่เหมาะสมกับขนาดของ data ของเรา บวกกับการปรับจูนพารามิเตอร์ที่เหมาะสม อาจทำให้ได้ Accuracy ที่ดี โดยไม่จำเป็นต้องใช้ Model ที่มีขนาดใหญ่เกินไป 
จากสมมติฐานที่เราตั้งไว้เบื้องต้น เราคาดว่า VGG16 ซึ่งเป็น model ขนาดใหญ่ จะให้ผลที่ดีที่สุด แต่ผลออกมา ปรากฎว่า MobileNet ซึ่งเป็น model ขนาดเล็กกลับให้ผลที่ดีที่สุด**

![image](https://user-images.githubusercontent.com/107410157/197337370-e4c943fe-e8e3-4be3-a43a-0bb05bbf1a10.png)

(https://keras.io/api/applications/)

**3. การ split data มีผลต่อความหลากหลายของรูปภาพใน train/test set หากเรานำภาพที่คล้ายๆกันไปกองอยู่ใน train set หรือ test set อาจทำให้เกิดการ bias ต่อผล accuracy ที่ได้ หากนำ model นี้ไปใช้งานกับ test set ชุดอื่นๆที่ได้จากการเก็บ data ครั้งถัดไป อาจพบว่า โมเดลจะทายไม่ถูกมากขึ้น**

**4. การพิจารณาทำ Data Augmentation ที่เหมาะสม ช่วยให้ลดเวลา และ save resource ในการรันอย่างมาก**

## Conclusion:

* ผลของ model before fine-tuning ทั้ง 3 model ยังไม่สามารถแยกยี่ห้อของโทรศัพท์ได้
* ผลของ model after fine-tuning ไม่ตรงกับสมมติฐานที่ได้ตั้งไว้ในเบื้องต้น ที่คาดว่า **`"VGG16"`** ที่เป็นตัวแทนของ model ที่มีขนาดใหญ่สุดจากที่เลือก จะให้ผล Accuracy ที่ดีที่สุด แต่ผล after fine-tuning พบว่า **`"MobileNet"`** ที่เป็นตัวแทนของ model ที่มีขนาดเล็กสุด ให้ผล Accuracy ที่สูงที่สุด รองลงมาคือ **`"ResNet152V2"`** ที่เป็นตัวแทนของ model ที่มีขนาดกลาง ส่วน **`"VGG16"`** ให้ผล Accuracy ที่น้อยที่สุด




## References:
* https://keras.io/api/applications/
* 
* ref code Aj.
* 
## References version:
| Library | Version |
| :------ | :----: |
|**`"Python"`**|3.7.15|
|**`"Numpy"`**|1.21.6|
|**`"TensorFlow"`**|2.9.2|



## 🙋 Deepsleep's Member:
| %|ID|Name |Responsibility  |
| :------ | ------ |:------|:-------|
|⭐ **`20%`** | **`6410414007`**  | 👦 Athit Santikarn  |**`Collect data(Oppo)`**, **`Write result`**, **`conclusion report`**|
|⭐ **`20%`** | **`6410422020`**  | 👩 Suphanun Sukamta |**`Collect data(Samsung)`**, **`Write result`**, **`conclusion report`**|
|⭐ **`20%`** | **`6410422004`**  | 👦 Chokchai Kenpho  |**`Collect data(Apple)`**, **`Train model-VGG16`**|
|⭐ **`20%`** | **`6410422009`**  | 👦 Noppol Anakpluek  |**`Preprocess data`**, **`Train model-ResNet152V2`**|
|⭐ **`20%`** | **`6420422006`**  | 👦 Watcharakorn Pasanta  | **`Collect data(Huawei)`**, **`Train model-MobileNet`**|


## End credit: 
**This project is a part of Course DADS7202 Deep Learning, Data Analytics and Data Science, NIDA.**

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
