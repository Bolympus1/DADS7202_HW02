# DADS7202_HW02 The pre-trained CNN
![image](https://user-images.githubusercontent.com/107410157/197267919-ac58b7ea-f75d-4610-9408-eb14e26ceb85.png)

## Introduction: 

Nowadays there are a lot of mobile phones in the market. There has a lot of unique functions for their brand. However the appearance of mobile phone are very the same, making the customer very confused when they try to find a phone that they want. "which one is the right one that I want?" or "Is this the phone that I'm looking for?" there is the most question when customer try to find the phone because when searching mobile phone on Google, sometimes the picture that comes up looks like the brand that search but it isn't. Because of this problem, our team comes up with the idea of "Classification of mobile phone brand" to classify the picture of mobile phones which one is which brand. From our discussion, we choose 4 mobile phone brands that we think it's easy to confuse and hard to tell which brand is the right one.

There are a lot of mobile phones in the market but **the appearance of every mobile phone are look the same** makes it hard for the customer to find the phone that they want. Even the photo of the phone on Google sometimes the picture that comes up looks like the brand that searched but it isn't. **Because of this problem our team come up with the idea** **`" Classification of mobile phone brand"`** to classify the picture of mobile phones which one is which brand.

* 📱 **`Apple (iPhone)`**    
* 📱 **`Huawei`**
* 📱 **`OPPO`**   
* 📱 **`Samsung`**


## 📋 Image Dataset
 - [✨ Dataset](https://drive.google.com/drive/folders/16B2ut6co3qQ1eBGqpvZMb8ZJNta62rp4?usp=sharing) <br>
Link to download the dataset: https://drive.google.com/drive/folders/16B2ut6co3qQ1eBGqpvZMb8ZJNta62rp4?usp=sharing

We collected 4 brands of mobile phone image(3 color channel) datasets which are Apple(iPhone), Huawei, OPPO, and Samsung that are still sale in 2022. We try to select various images in every dimension of the phone (frontside, backside, and some specific areas such as the camera ) source of the official image are from  BaNANA online shop **`"https://www.bnn.in.th/th"`** and unofficial image from Facebook market place. The total image that we collected from 2 sources is 434 images (iPhone 100 images, Huawei 124 images, Oppo 109 images, and Samsung 100 images).


## Assumption:
We think the pre-trained model that validation on ImageNet dataset can't classify present moblie phone design to tell which image is which brand cause of that we choose 3 models such as VGG16, ResNet152V2, and MobileNet for study in this project.

In this case our assumption about the pre-trained model is the largest model will have the best accuracy which is VGG16
and the lowest accuracy is MobileNet.

## Data pre-processing and splitting :
* Image Preparation : collected all images in .jpg and manually put them into the brand's folder then in a sub-folder split into 2 folders "train_ds" and "test_ds "of each brand. Ratio of train, validation and test as shown in table 1.

* We label images by importing datasets with tf.keras.utils.image_dataset_from_directory image will be labeled as the sub-folder name.

* label class : 0,1,2, and 3 mean Apple, Huawei, Oppo, and Samsung as ordered. then used "sparse_categorical_crossentropy" to calculate Loss

* Resizing image dataset to 224 x 224 to match with model requirement.

![image](https://user-images.githubusercontent.com/107410157/197308226-29a91b68-5a4d-467e-9e3f-402624fc36fa.png)


**Table 1: Data pre-processing and splitting**
![MicrosoftTeams-image](https://user-images.githubusercontent.com/86920208/197348853-1eac9f2a-a8c0-490f-b524-6c8b382d9b65.png)


## Before Fine-tuning:
From testing all the pre-trained model (**`"VGG16"`**, **`"ResNet152V2"`** , **`"MobileNet"`**) before fine-tuning the result of all model show accuracy = 0 which mean all these 3 models can't tell the mobile phone brand that we want. Example of model prediction show iPhone = projector,  Huawei = iPod, Oppo = switch, and Samsung = notebook.

**Table 2: Result before fine-tuning**
| Model |Test Accuracy | Test Loss | Runtime with GPU (H:M:S) | GPU Name |
| :------ | :----: |:-----:|:-----:|:-----:|
|**`"VGG16"`**| 0 | 18.2531 | 0:02:41 | Tesla T4
|**`"MobileNet"`**| 0 | 13.3670 | 0:02:41 | Tesla T4
|**`"ResNet152V2"`**| 0 | 2508.23 | 0:03:10 | Tesla T4

![MicrosoftTeams-image (2)](https://user-images.githubusercontent.com/86920208/197349159-4e116fc5-017e-49b3-98ac-6dca7eda4dfb.png)

Result of pre-trained model.
![image](https://user-images.githubusercontent.com/107410157/197340501-6658c397-1659-48f6-bbd2-8c6a4364263e.png)


## Data Augmentation :
We decided to do data augmentation to increase the number of dataset and minimize overfit and each model use different data augmentation combination to perform the best result of each model as follow.

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

To get more accuracy, the parameter that we adjust from the pre-trained model.

**Table 4: Fine-tuning parameters**
| Model | epoc | Feature extractor | Feature classifier | Optimizer | learning rate |
| :------ | :----: |:-----:|--------|:-----:|:-----:|
|**`"VGG16"`**|15|Conv2D : 3 Layer|activation="relu" & "tanh"|Adam|0.0001|
|**`"MobileNet"`**|100|all trainable|activation="relu" & Dropout =0.5|Adam|0.0001|
|**`"ResNet152V2"`**|30|all trainable|activation="relu" & Dropout =0.2|Adam|0.0001|

**Train accuracy/Train loss**
![image](https://user-images.githubusercontent.com/107410157/197338882-ee1b09af-3c49-4c88-a945-29f753e8cb0b.png)

After running 5 times, 3 models after fine-tuning results say the models can predict the brand of mobile phone. However, the accuracy is different in each model as show in the table below.

**Table 5: Result after fine-tuning**
| Model | AVG. Test Accuracy | SD Test Accuracy | AVG. Test Loss | SD Test Loss | AVG. Runtime with GPU (H:M:S) |
| :------ | :----: |:-----:|:-----:|:-----:|:-----:|
|**`"VGG16"`**|0.730|±0.0167|0.715|±0.0749|0:02:50|
|**`"MobileNet"`**|0.870|±0.0313|0.631|±0.1281|0:07:14|
|**`"ResNet152V2"`**|0.795|±0.0447|0.873|±0.1333|0:02:46|



The result of models (Actual brand - Predict Brand)
![image](https://user-images.githubusercontent.com/107410157/197340370-b178c8a0-4478-4d77-a95f-2cfe677bb599.png)
![image](https://user-images.githubusercontent.com/107410157/197340236-3596088e-27cb-46c3-9c76-139dc42eed42.png)
![image](https://user-images.githubusercontent.com/107410157/197340204-583dced2-bc65-476a-a6da-c19d97be76ac.png)



## Results:
All of the models that we choose,  **`"MobileNet"`** have the best accuracy score. Result after using random seed 5 times average test accuracy is 87.00% +/-3.13% and the average test loss is 63.13% +/-12.81%, the average runtime with GPU is 7 min 14 sec but if ranking model performance by runtime **`"MobileNet"`** is the slowest because it uses the most epoc and limitation of Google Colab.

![image](https://user-images.githubusercontent.com/107410157/197309429-bc6da6a4-b423-4b94-83ab-ac2f2abe1b16.png)





## Discussion:

จากการศึกษาในครั้งนี้ กลุ่มเราได้สรุปประเด็นที่น่าสนใจในการทำ Deep Learning กับ image dataset ดังนี้

**1. ได้มีการลองรัน Model **`"NASNetLarge"`** ที่มีขนาดใหญ่ และจำนวน parameter เยอะ แต่ไม่สามารถรันได้ เนื่องจากต้องใช้ทรัพยากรในการรันอย่างมาก (session crash due to ran out of RAM)**

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
* Tensorflow
https://www.tensorflow.org/tutorials/images/classification
https://www.tensorflow.org/tutorials/load_data/images
https://www.tensorflow.org/api_docs/python/tf/keras/utils/image_dataset_from_directory
https://www.tensorflow.org/api_docs/python/tf/keras/Model#predict

* Keras (https://keras.io/api/)
https://keras.io/examples/vision/image_classification_from_scratch/
https://keras.io/guides/preprocessing_layers/

* Data_loading >> https://keras.io/api/data_loading/image/
image_dataset_from_directory function = Generates a tf.data.Dataset from image files in a directory. (https://www.tensorflow.org/api_docs/python/tf/keras/utils/image_dataset_from_directory)


## References version:
| Library | Version |
| :------ | :----: |
|Python|3.7.15|
|Numpy|1.21.6|
|TensorFlow|2.9.2|
|GPU|NVIDIA GeForce RTX 3060 Laptop GPU|
|Colab Pro|Tesla P100-PCIE-16GB/A100-SXM4-40GB|

## References:
Code from class DADS7202
https://keras.io/api/applications/
https://keras.io/examples/vision/image_classification_from_scratch/
https://keras.io/guides/preprocessing_layers/
https://www.tensorflow.org/tutorials/load_data/images
https://www.tensorflow.org/tutorials/images/classification


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

