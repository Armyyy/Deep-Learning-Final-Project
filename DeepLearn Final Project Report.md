

![][image1]  
Final Project Report  
Waste Classification  
01204466-65  Deep Learning

จัดทำโดย  
นาย ธนาธิป        จินดามณี 6610505411  
นาย ภากร   ตันติวัฒนากุล 6610505535

คณะวิศวกรรมศาสตร์   
ภาควิชาวิศวกรรมคอมพิวเตอร์

สารบัญ

[**1\. หัวข้อ final project	3**](#หัวข้อ-final-project)

[1.1. การจำแนกประเภทขยะจากภาพถ่ายด้วย Convolutional Neural Network (CNN)	3](#การจำแนกประเภทขยะจากภาพถ่ายด้วย-convolutional-neural-network-\(cnn\))

[1.2. วัตถุประสงค์	3](#วัตถุประสงค์)

[1.3. เกณฑ์ในการจำแนก	3](#เกณฑ์ในการจำแนก)

[**2\. หัวข้อนี้น่าสนใจอย่างไร	4**](#หัวข้อนี้น่าสนใจอย่างไร)

[**3\. ทำไมหัวข้อนี้จึงต้องใช้ deep learning	4**](#ทำไมหัวข้อนี้จึงต้องใช้-deep-learning)

[**4\. สถาปัตยกรรม	5**](#สถาปัตยกรรม)

[4.1. Convolutional Neural Network (CNN)	5](#convolutional-neural-network-\(cnn\))

[4.2. ภาพรวมของสถาปัตยกรรม	5](#ภาพรวมของสถาปัตยกรรม)

[**5\. อธิบายโค้ด	6**](#อธิบายโค้ด)

[5.1. เตรียมข้อมูล	6](#เตรียมข้อมูล)

[5.2. การสร้าง Randomly Initialized CNN Model (Non Pre-Trained CNN Model)	7](#การสร้าง-randomly-initialized-cnn-model-\(non-pre-trained-cnn-model\))

[5.2.1. นิยามโมเดล	7](#นิยามโมเดล)

[5.2.2. นิยาม/ปรับแต่ง parameter	8](#นิยาม/ปรับแต่ง-parameter)

[5.2.3. Train โมเดล	9](#train-โมเดล)

[5.2.4. Evaluate โมเดล	9](#evaluate-โมเดล)

[5.3. Pre-trained Model	11](#pre-trained-model)

[5.3.1. นิยามโมเดล	11](#นิยามโมเดล-1)

[5.3.2. นิยาม/ปรับแต่ง parameter	12](#นิยาม/ปรับแต่ง-parameter-1)

[5.3.3. Train โมเดล	13](#train-โมเดล-1)

[5.3.4. Evaluate โมเดล	14](#evaluate-โมเดล-1)

[**6\. อธิบายวิธีใน train การและ dataset ที่เกี่ยวข้องและแหล่งที่มา	15**](#อธิบายวิธีใน-train-การและ-dataset-ที่เกี่ยวข้องและแหล่งที่มา)

[6.1. วิธีในการเทรน	15](#วิธีในการเทรน)

[6.2. แหล่งข้อมูล (Dataset)	15](#แหล่งข้อมูล-\(dataset\))

[6.2.1. Dataset	15](#dataset)

[6.2.2. ลักษณะของ Dataset	15](#ลักษณะของ-dataset)

[6.2.3. เหตุผลที่เลือกใช้ Dataset นี้	15](#เหตุผลที่เลือกใช้-dataset-นี้)

[**7\. การประเมิน model	16**](#การประเมิน-model)

[7.1. เกณฑ์การเลือก metric	16](#เกณฑ์การเลือก-metric)

[7.2. กราฟ loss	16](#กราฟ-loss)

[**8\. อ้างอิง	17**](#อ้างอิง)

[8.1. Garbage Dataset	17](#garbage-dataset)

[8.2. Waste Classification with CNN by Sashaank Sekar	17](#waste-classification-with-cnn-by-sashaank-sekar)

[8.3. Waste Classification with CNN by Beyza Nur Nakkaş	17](#waste-classification-with-cnn-by-beyza-nur-nakkaş)

[**9\. สัดส่วนงาน	17**](#สัดส่วนงาน)

1. # หัวข้อ final project {#หัวข้อ-final-project}

   1. ## การจำแนกประเภทขยะจากภาพถ่ายด้วย Convolutional Neural Network (CNN) {#การจำแนกประเภทขยะจากภาพถ่ายด้วย-convolutional-neural-network-(cnn)}

   2. ## วัตถุประสงค์ {#วัตถุประสงค์}

      1. เพื่อพัฒนาโมเดล Deep Learning สำหรับการ จำแนกประเภทของขยะจากภาพถ่ายจริง โดยใช้เทคนิค Convolutional Neural Network (CNN) ซึ่งสามารถวิเคราะห์และเรียนรู้ลักษณะเฉพาะของขยะในแต่ละประเภทได้อย่างอัตโนมัติ

   3. ## เกณฑ์ในการจำแนก {#เกณฑ์ในการจำแนก}

      1. โมเดลถูกออกแบบให้สามารถจำแนกขยะออกเป็น 10 ประเภทหลัก ได้แก่

| English | ภาษาไทย | คำอธิบายเพิ่มเติม |
| ----- | ----- | ----- |
| battery | แบตเตอรี่ | ใช้เก็บพลังงานไฟฟ้า เช่น ถ่านไฟฉาย แบตโทรศัพท์ ควรทิ้งในถังแยกเฉพาะ เพราะมีสารเคมีอันตราย |
| biological | ขยะชีวภาพ | ของเหลือจากสิ่งมีชีวิต เช่น เศษอาหาร เศษผักผลไม้ หรือของเน่าเปื่อยได้ ใช้ทำปุ๋ยได้ |
| cardboard | กระดาษแข็ง | กล่องกระดาษ เช่น กล่องพัสดุ กล่องซีเรียล รีไซเคิลได้ง่าย |
| clothes | เสื้อผ้า | เสื้อ กางเกง ผ้า ผ้าห่ม สามารถบริจาค หรือนำไปรีไซเคิลเพื่อทำวัสดุอื่นได้ |
| glass | แก้ว | ขวดแก้ว แก้วน้ำ หรือวัสดุที่ทำจากแก้ว ควรล้างก่อนนำไปรีไซเคิล |
| metal | โลหะ | เหล็ก อะลูมิเนียม กระป๋องน้ำอัดลม หรือของใช้ที่เป็นโลหะ สามารถนำไปหลอมใหม่ได้ |
| paper | กระดาษ | กระดาษหนังสือพิมพ์ กล่องกระดาษ หรือเอกสารต่าง ๆ รีไซเคิลได้ง่าย |
| plastic | พลาสติก | ขวดน้ำ ถุงพลาสติก กล่องอาหาร เป็นวัสดุที่ใช้บ่อย ควรล้างก่อนรีไซเคิล |
| shoes | รองเท้า | รองเท้าเก่า สามารถบริจาค หรือนำไปรีไซเคิลในบางโครงการได้ |
| trash | ขยะทั่วไป | ของประเภทอื่นๆ ที่นำไปรีไซเคิลยาก หรือเศษขยะชิ้นเล็กชิ้นน้อย ใน dataset ที่นำมา train ส่วนใหญ่จะเป็นหน้ากากอนามัย และแปรงสีฟัน |

2. # หัวข้อนี้น่าสนใจอย่างไร {#หัวข้อนี้น่าสนใจอย่างไร}

   1. ในปัจจุบัน ปัญหาการจัดการขยะเป็นประเด็นสำคัญระดับโลก โดยเฉพาะการคัดแยกขยะอย่างถูกต้อง ซึ่งเป็นขั้นตอนสำคัญในการรีไซเคิลและลดผลกระทบต่อสิ่งแวดล้อม อย่างไรก็ตาม การคัดแยกขยะด้วยมนุษย์นั้นใช้เวลาและแรงงานมาก อีกทั้งยังมีโอกาสเกิดความผิดพลาดสูง  
   2. ดังนั้น โครงงานนี้จึงมีจุดประสงค์เพื่อพัฒนา โมเดล Deep Learning ที่สามารถจำแนกประเภทของขยะจากภาพถ่ายได้อัตโนมัติ เพื่อช่วยสนับสนุนระบบจัดการขยะ  และสามารถประยุกต์ใช้ในสถานที่จริง เช่น จุดคัดแยกขยะอัตโนมัติในมหาวิทยาลัยหรือห้างสรรพสินค้า หุ่นยนต์คัดแยกขยะ (Recycling Robots)  
   3. การเลือกหัวข้อนี้มาทำเป็นโครงงานเกิดจากความสนใจในเทคโนโลยี AI ที่สามารถช่วยลดภาระของมนุษย์และช่วยสิ่งแวดล้อมได้จริง อีกทั้งเป็นปัญหาที่มีข้อมูลภาพจำนวนมาก เหมาะกับการนำ Deep Learning มาประยุกต์ใช้อย่างแท้จริง

3. # ทำไมหัวข้อนี้จึงต้องใช้ deep learning {#ทำไมหัวข้อนี้จึงต้องใช้-deep-learning}

   1. ความซับซ้อนของข้อมูลภาพ  
   2. ภาพถ่ายของขยะมีความหลากหลายสูง ทั้งในด้านรูปร่าง สี แสง มุมมอง และพื้นหลัง ทำให้ การใช้วิธีการแบบ Traditional Machine Learning (เช่น SVM, k-NN หรือ Decision Tree) ต้องใช้การ “ดึงคุณลักษณะ (feature extraction)” ด้วยมือ เช่น สี, รูปร่าง, texture ซึ่งต้องใช้เวลาและความเชี่ยวชาญสูง และไม่สามารถจับลักษณะที่ซับซ้อนได้ดี  
   3. ขณะที่ Deep Learning โดยเฉพาะ CNN (Convolutional Neural Network) สามารถเรียนรู้ feature เหล่านี้ได้อัตโนมัติจากภาพโดยตรงผ่านกระบวนการ convolution และ pooling จึงมีความสามารถในการจำแนกภาพได้ดีกว่าอย่างมาก  
   4. การเปรียบเทียบ

| วิธีการ | จุดเด่น | ข้อจำกัด |
| ----- | ----- | ----- |
| Traditional ML (SVM, Random Forest) | ใช้ข้อมูลน้อยกว่า, อธิบายได้ง่าย | ต้องออกแบบ feature เอง, ประสิทธิภาพต่ำกับข้อมูลภาพที่ซับซ้อน |
| Classical Image Processing (Thresholding, Edge Detection) | เข้าใจง่าย, ใช้คำนวณน้อย | ไม่สามารถแยกขยะที่มีลักษณะใกล้เคียงกัน เช่น “plastic” vs “glass” |
| Deep Learning (CNN) | เรียนรู้ feature อัตโนมัติ, ประสิทธิภาพสูงมาก, เหมาะกับภาพ | ต้องใช้ข้อมูลจำนวนมากและเวลา train สูง |

4. # สถาปัตยกรรม {#สถาปัตยกรรม}

   1. ## Convolutional Neural Network (CNN) {#convolutional-neural-network-(cnn)}

      1. เป็นโมเดลที่ได้รับความนิยมสูงในการประมวลผลภาพ เนื่องจากสามารถเรียนรู้ features จากภาพได้โดยอัตโนมัติ ผ่านกระบวนการ convolution และ pooling

   2. ## ภาพรวมของสถาปัตยกรรม {#ภาพรวมของสถาปัตยกรรม}

      1. โมเดล CNN ที่ใช้ประกอบด้วย 2 ชั้น Convolution, 2 ชั้น Max Pooling, และ 2 ชั้น Fully Connected (FC) พร้อม ReLU activation function และ Dropout layer เพื่อป้องกัน overfitting

   ![][image2]

   3. ตารางอธิบายแต่ละ layer

| Layer | ชนิด | Input → Output | Activation | รายละเอียด |
| ----- | ----- | ----- | ----- | ----- |
| Conv1 | Convolutional | 3×128×128 → 24×126×126 | ReLU | ใช้ kernel ขนาด 3×3 เพื่อสกัด feature พื้นฐาน เช่น ขอบและสี |
| Pool1 | Max Pooling | 24×126×126 → 24×63×63 | \- | ลดขนาดภาพครึ่งหนึ่งและช่วยลด noise |
| Conv2 | Convolutional | 24×63×63 → 36×61×61 | ReLU | สกัด feature ที่ซับซ้อนขึ้น เช่น รูปทรงหรือ texture |
| Pool2 | Max Pooling | 36×61×61 → 36×30×30 | \- | ลดมิติข้อมูลและเพิ่มความทนต่อการเปลี่ยนแปลงของภาพ |
| Flatten | \- | 36×30×30 → 32,400 | \- | แปลงข้อมูล 3D เป็น 1D vector เพื่อป้อนเข้า fully connected layer |
| FC1 | Fully Connected | 32,400 → 128 | ReLU | เรียนรู้การเชื่อมโยงเชิงลึกระหว่าง feature |
| Dropout | Regularization | \- | \- | ลด overfitting โดยสุ่มปิด neuron บางส่วน (p=0.3) |
| FC2 | Fully Connected | 128 → 10 | Softmax (ในขั้น evaluate) | แปลงเป็นความน่าจะเป็นของแต่ละคลาส |

5. # อธิบายโค้ด {#อธิบายโค้ด}

   1. ## เตรียมข้อมูล {#เตรียมข้อมูล}

      data\_root \= "/kaggle/working/data"

      train\_dir \= os.path.join(data\_root, "train")

      val\_dir   \= os.path.join(data\_root, "val")

      test\_dir  \= os.path.join(data\_root, "test")

      \# Create new folders

      for dir\_path in \[train\_dir, val\_dir, test\_dir\]:

          os.makedirs(dir\_path, exist\_ok=True)

      \# Split ratios

      train\_ratio \= 0.7

      val\_ratio \= 0.15

      test\_ratio \= 0.15

      \# Loop through each class folder

      for class\_name in os.listdir(dataset\_path):

          class\_path \= os.path.join(dataset\_path, class\_name)

          if not os.path.isdir(class\_path):

              continue  \# skip non-folder items

          \# Make subfolders for each split

          for split\_dir in \[train\_dir, val\_dir, test\_dir\]:

              os.makedirs(os.path.join(split\_dir, class\_name), exist\_ok=True)

          \# List all images

          images \= os.listdir(class\_path)

          random.shuffle(images)

          \# Compute split indices

          total \= len(images)

          train\_end \= int(total \* train\_ratio)

          val\_end \= train\_end \+ int(total \* val\_ratio)

          train\_files \= images\[:train\_end\]

          val\_files \= images\[train\_end:val\_end\]

          test\_files \= images\[val\_end:\]

          \# Copy images

          def copy\_files(file\_list, dest\_folder):

              for fname in file\_list:

                  src \= os.path.join(class\_path, fname)

                  dst \= os.path.join(dest\_folder, class\_name, fname)

                  shutil.copy2(src, dst)

          copy\_files(train\_files, train\_dir)

          copy\_files(val\_files, val\_dir)

          copy\_files(test\_files, test\_dir)

      print("Dataset split completed\!")

      

โค้ดนี้เป็นขั้นตอน **เตรียมข้อมูล (data preparation)** สำหรับแบ่งชุดข้อมูลภาพ (dataset) ออกเป็น 3 ส่วนคือ **train**, **validation** และ **test** โดยใช้ dataset จาก [www.kaggle.com/datasets/sumn2u/garbage-classification-v2](https://www.kaggle.com/datasets/sumn2u/garbage-classification-v2) โดย Suman Kunwar อธิบายคร่าว ๆ ได้ดังนี้

1. กำหนดตำแหน่งโฟลเดอร์ปลายทาง และสร้างโฟลเดอร์หากยังไม่มี  
   2. กำหนดอัตราส่วนการแบ่งข้อมูล ในที่นี้ แบ่งข้อมูลเป็น 70% สำหรับ train 15% สำหรับ validation 15% สำหรับ test  
      3. วนลูปสร้างโฟลเดอร์ย่อยสำหรับแต่ละคลาสในแต่ละชุด  
      4. คำนวณจำนวนไฟล์ในแต่ละชุด และ แบ่งแยกไฟล์ตามสัดส่วน  
      5. คัดลอกไฟล์ไปยังโฟลเดอร์ปลายทาง และแสดงว่าเสร็จสิ้นการทำงาน

   2. ## การสร้าง Randomly Initialized CNN Model (Non Pre-Trained CNN Model) {#การสร้าง-randomly-initialized-cnn-model-(non-pre-trained-cnn-model)}

   Randomly Initialized CNN Model คือที่ถูกเริ่มต้นด้วยค่า weight แบบสุ่ม โดยไม่มีการฝึกหรือเรียนรู้จากชุดข้อมูลใดๆ ก่อนหน้านี้ กล่าวคือ โมเดลจะเริ่มต้นด้วยค่าพารามิเตอร์ที่ถูกสุ่มขึ้นมาใหม่ตั้งแต่เริ่มแรก

      1. ### นิยามโมเดล {#นิยามโมเดล}

         class CNN(nn.Module):  
             def \_\_init\_\_(self, num\_classes\=10, in\_channels\=3, input\_size\=128,  
                          C1\=24, C2\=21, H\=591):  
                 super().\_\_init\_\_()  
           
                 self.conv1 \= nn.Conv2d(in\_channels, C1, kernel\_size=3, bias=True)  \# 128-\>126  
                 self.pool1 \= nn.MaxPool2d(2,2)                                     \# 126-\>63  
                 self.conv2 \= nn.Conv2d(C1, C2, kernel\_size=3, bias=True)           \# 63-\>61  
                 self.pool2 \= nn.MaxPool2d(2,2)                                     \# 61-\>30  
           
                 self.relu \= nn.ReLU(inplace=True)  
                 self.flatten \= nn.Flatten()  
           
                 flattened \= 30\*30\*C2                                              \# 900\*C2  
                 self.fc1 \= nn.Linear(flattened, H, bias=True)  
                 self.dropout \= nn.Dropout(p=0.3)  
                 self.fc2 \= nn.Linear(H, num\_classes, bias=True)  
           
             def forward(self, x):  
                 x \= self.pool1(self.relu(self.conv1(x)))  
                 x \= self.pool2(self.relu(self.conv2(x)))  
                 x \= self.flatten(x)  
                 x \= self.relu(self.fc1(x))  
                 x \= self.dropout(x)  
                 x \= self.fc2(x)  
                 return x

         1. โค้ดนี้เป็นการ นิยาม (define) โมเดล Convolutional Neural Network (CNN) แบบ Randomly Initialized โดยเขียนขึ้นเองด้วย PyTorch  
         2. โมเดลนี้เป็น CNN แบบพื้นฐานที่มี:  
            1. 2 ชั้น Convolution \+ Max Pooling  
            2. 1 Fully Connected Hidden Layer  
            3. 1 Output Layer ที่มีผลลัพธ์ 10 ค่าแยกประเภท  
            4. มีการ Dropout \= 0.3 เพื่อเพิ่ม Regularization ของ model

      2. ### นิยาม/ปรับแต่ง parameter {#นิยาม/ปรับแต่ง-parameter}

         batch\_size \= 64  
         epochs \= 7  
         learning\_rate \= 0.001  
         weight\_decay  \= 5e-4  
           
         optimizer \= optim.AdamW(cnn\_model.parameters(), lr=learning\_rate, weight\_decay=weight\_decay)  
         loss\_function \= nn.CrossEntropyLoss()

         1. batch\_size \= 64:  
             จำนวนตัวอย่างข้อมูลที่ใช้ในแต่ละขั้นตอนการอัปเดตน้ำหนักของโมเดล (แต่ละ batch)  
             ขนาด 64 ค่อนข้างเหมาะสมสำหรับการฝึกโมเดลใน GPU เพื่อให้การประมวลผลมีประสิทธิภาพ  
         2. epochs \= 7:  
             จำนวนครั้งที่โมเดลจะทำการเรียนรู้ผ่านชุดข้อมูลทั้งหมด (epoch)  
             ในกรณีนี้คือ 7 ครั้ง ซึ่งอาจจะปรับเพิ่มหรือลดตามความเหมาะสมของโมเดล  
         3. learning\_rate \= 0.001:  
             อัตราการเรียนรู้ (learning rate) สำหรับการอัปเดตน้ำหนักของโมเดล  
             ค่า 0.001 เป็นค่าเริ่มต้นที่ดีสำหรับ Adam optimizer และเป็นค่าที่นิยมใช้บ่อย  
         4. weight\_decay \= 5e-4:  
            ค่าของ L2 regularization หรือ weight decay เพื่อป้องกันการ overfitting  
            เมื่อใช้ weight decay, optimizer จะลดค่าน้ำหนักลงบ้างในแต่ละการอัปเดตเพื่อไม่ให้โมเดลจำกัดมากเกินไป  
         5. Optimizer \= AdamW:  
            เป็นการใช้งาน Adam optimizer แต่มีการปรับปรุง (Weight Decay Regularization) เพื่อให้การ regularize น้ำหนักดีขึ้นในระหว่างการฝึก  
         6. Loss \= CrossEntropyLoss: ใช้สำหรับการจำแนกประเภท (classification) โดยเฉพาะสำหรับปัญหาหลายคลาส, ฟังก์ชันนี้จะคำนวณ softmax ในตัวและคำนวณ

      3. ### Train โมเดล {#train-โมเดล}

         cnn\_model.train()  
           
         for epoch in range(epochs):  
             total\_loss \= 0  
             running\_loss \= 0.0  
             correct\_pred \= 0  
             total\_pred \= 0  
           
             \# First grab a batch of training data which our data loader returns as a tensor  
             for idx, (images, labels) in enumerate(tqdm(trainset\_loader)):  
                 images, labels \= images.to(device), labels.to(device)  
           
                 \# Forward pass  
                 logits \= cnn\_model(images)  
           
                 loss \= loss\_function(logits, labels)  
           
                 \# Get the loss and log it to comet and the loss\_history record  
                 loss\_value \= loss.item()  
                 comet\_model.log\_metric("loss", loss\_value, step=idx)  
                 loss\_history.append(loss\_value) \# append the loss to the loss\_history record  
                 plotter.plot(loss\_history.get())  
           
                 \# Backpropagation/backward pass  
                 optimizer.zero\_grad()  
                 loss.backward()  
                 optimizer.step()  
                 running\_loss \+= loss\_value \* images.size(0)  
           
                 \# Get the prediction and tally metrics  
                 predicted \= torch.argmax(logits, dim=1)  
                 correct\_pred \+= (predicted \== labels).sum().item()  
                 total\_pred \+= labels.size(0)  
           
             \# Compute metrics  
             train\_loss \= running\_loss / total\_pred  
             train\_acc  \= correct\_pred / total\_pred  
             val\_loss, val\_acc \= evaluate(cnn\_model, testset\_loader, loss\_function)  
             print(f"Epoch {epoch+1}: train\_loss={train\_loss:.4f} acc={train\_acc:.4f} | val\_loss={val\_loss:.4f} acc={val\_acc:.4f}")  
         

      4. ### Evaluate โมเดล {#evaluate-โมเดล}

         def evaluate(model, dataloader, loss\_function):  
             model.eval()  
             test\_loss, correct, total \= 0.0, 0, 0  
             with torch.no\_grad():  
                 for images, labels in dataloader:  
                     images, labels \= images.to(device), labels.to(device)  
                     outputs \= model(images)  
                     loss \= loss\_function(outputs, labels)  
                     test\_loss \+= loss.item() \* images.size(0)  
           
                     preds \= outputs.argmax(1)  
                     correct \+= (preds \== labels).sum().item()  
                     total \+= labels.size(0)  
             return test\_loss / total, correct / total  
         1. ตั้งค่าโหมดประเมินผล model.eval():  
             ตั้งโมเดลให้อยู่ใน evaluation mode ซึ่งจะทำให้ฟังก์ชันที่มีการใช้งาน dropout หรือ batch normalization ทำงานในลักษณะที่เหมาะสมในระหว่างการประเมิน (เช่น dropout จะถูกปิด) test\_loss, correct, total \= 0.0, 0, 0:  
         2. ปิดการคำนวณ Gradient  
            torch.no\_grad():  
            ใช้ context manager ที่จะทำให้ PyTorch ไม่คำนวณ gradients ในระหว่างการประเมิน เพื่อประหยัดหน่วยความจำและลดเวลาในการประมวลผล  
         3. วนรอบข้อมูลทดสอบจาก dataloader  
            for images, labels in dataloader:  
            images, labels \= images.to(device), labels.to(device)  
         4. ให้โมเดลทำนายผลและคำนวณ Loss  
            outputs \= model(images):  
             ใช้โมเดลในการทำนายผลลัพธ์จากภาพใน batch  
            loss \= loss\_function(outputs, labels):  
            คำนวณค่า loss โดยใช้ฟังก์ชัน  
            test\_loss \+= loss.item() \* images.size(0):  
             เพิ่มค่า loss ใน test\_loss ซึ่งจะสะสมค่า loss ของแต่ละ batch เพื่อคำนวณค่า average loss ในภายหลัง  
         5. คำนวณ Accuracy  
            preds \= outputs.argmax(1) คำนวณการทำนายโดยการเลือกคลาสที่มีค่าสูงสุดใน outputs ซึ่งเป็นค่าของ logits ที่ได้จากการทำนายจากโมเดล  
            correct \+= (preds \== labels).sum().item() นับจำนวนการทำนายที่ถูกต้องโดยการเปรียบเทียบ preds (การทำนาย) กับ labels (ค่าจริง) และเพิ่มค่าใน correct  
            total \+= labels.size(0) เพิ่มจำนวนข้อมูลทั้งหมดใน batch ในตัวแปร total  
         6. คืนค่าผลลัพธ์เฉลี่ย  
            return test\_loss / total, correct / total

   3. ## Pre-trained Model {#pre-trained-model}

      คือ โมเดลที่ถูกฝึกมาแล้ว ด้วยข้อมูลขนาดใหญ่จากภายนอกก่อนที่จะนำมาใช้ในงานของเรา โดยที่การฝึกโมเดลนี้จะเกิดขึ้นก่อนที่เราใช้โมเดลนั้นในงานเฉพาะ (หรือ fine-tuning) ตามลักษณะงานที่เราต้องการ โดยข้อดีคือ ประหยัดเวลา, ประหยัดทรัพยากร และทำงานได้ดีกับชุดข้อมูลที่มีน้อย ซึ่ง Pre-trained Model ทำงานได้ดัใน CNN Model  
      

      1. ### นิยามโมเดล {#นิยามโมเดล-1}

         backbone \= models.resnet18(weights=models.ResNet18\_Weights.DEFAULT)  
         in\_features \= backbone.fc.in\_features  
         backbone.fc \= nn.Linear(in\_features, len(index\_to\_label))  
         pretrained\_model \= backbone.to(device)

         1. models.resnet18()  ใช้ฟังก์ชันจาก torchvision.models เพื่อนำเข้า ResNet-18 ซึ่งเป็นโมเดล CNN ที่มีโครงสร้าง Residual Networks (ResNet) ที่ได้รับความนิยม  
         2. weights=models.ResNet18\_Weights.DEFAULT  ใช้น้ำหนักที่ฝึกไว้แล้วจาก ImageNet ซึ่งช่วยให้โมเดลเริ่มต้นการฝึกได้ดีขึ้น (transfer learning)  
         3. backbone.fc.in\_features คือการดึงจำนวน input features ของ fully connected layer ใน ResNet-18, เลเยอร์ fc จะเชื่อมต่อกับลำดับสุดท้ายของฟีเจอร์ที่โมเดลได้เรียนรู้มาจาก convolutional layers ก่อนหน้า  
         4. backbone.fc \= nn.Linear(in\_features, len(index\_to\_label)):  
         5. ที่นี้เราเปลี่ยน fully connected layer (fc) ใน ResNet-18 ให้เชื่อมต่อกับจำนวนคลาสที่ต้องการทำการจำแนกจำนวนคลาสในงานของเรา โดยใช้ nn.Linear และปรับ output ให้ตรงกับงานของเรา

      2. ### นิยาม/ปรับแต่ง parameter {#นิยาม/ปรับแต่ง-parameter-1}

         1. num\_classes \= len(index\_to\_label):  
            กำหนดจำนวนคลาส (labels) โดยใช้ความยาวของ index\_to\_label ซึ่งเป็นลิสต์หรือดิกชันนารีที่เก็บชื่อคลาสทั้งหมด  
         2. batch\_size \= 64: จำนวนตัวอย่างที่ใช้ในแต่ละ batch ในการฝึก  
         3. epochs \= 7: จำนวนครั้งที่โมเดลจะทำการฝึกบนชุดข้อมูลทั้งหมด (epochs)  
         4. lr \= 0.001: อัตราการเรียนรู้ (learning rate) ที่ใช้สำหรับการอัปเดตน้ำหนัก  
         5. weight\_decay \= 5e-4: ค่าของ L2 regularization หรือ weight decay ที่ใช้ใน AdamW optimizer เพื่อป้องกัน overfitting  
         6. label\_smoothing \= 0.0: label smoothing ซึ่งเป็นเทคนิคที่ช่วยทำให้การฝึกมีความทนทานมากขึ้นโดยการบรรเทาค่าของ label ที่ตรงเกินไป ในที่นี้กำหนดเป็น 0.0 ซึ่งไม่มี label smoothing เพื่อให้การเทียบระหว่าง 2 โมเดลตรงไปตรงมามากขึ้น  
         7. feature\_extractor\_mode \= False: ค่าตัวแปรนี้จะควบคุมว่าเราจะฝึกเฉพาะ head หรือฝึกทั้งหมด ซึ่งในที่นี้เลือกฝึกทั้งหมดเพื่อให้การเทียบระหว่าง 2 โมเดลตรงไปตรงมามากขึ้น

      3. ### Train โมเดล {#train-โมเดล-1}

         \#--- Train loop \---  
         if hasattr(tqdm, '\_instances'): tqdm.\_instances.clear()  
         best\_val\_acc \= 0.0  
         best\_path \= "resnet18\_pretrained\_best.pt"  
         global\_step \= 0  
           
         for epoch in range(epochs):  
             pretrained\_model.train()  
             running\_loss \= 0.0  
             correct \= 0  
             total \= 0  
           
             for idx, (images, labels) in enumerate(tqdm(trainset\_loader)):  
                 images, labels \= images.to(device), labels.to(device)  
           
                 logits \= pretrained\_model(images)  
                 loss \= criterion(logits, labels)  
           
                 \# Log per-step loss to Comet and plotter (like your CNN)  
                 loss\_value \= loss.item()  
                 comet\_model\_2.log\_metric("loss", loss\_value, step=global\_step)  
                 loss\_history.append(loss\_value)  
                 plotter.plot(loss\_history.get())  
           
                 optimizer.zero\_grad(set\_to\_none=True)  
                 loss.backward()  
                 optimizer.step()  
           
                 running\_loss \+= loss\_value \* images.size(0)  
                 preds \= logits.argmax(1)  
                 correct \+= (preds \== labels).sum().item()  
                 total \+= labels.size(0)  
                 global\_step \+= 1  
           
             train\_loss \= running\_loss / total  
             train\_acc  \= correct / total  
           
             \# Validation  
             val\_loss, val\_acc \= evaluate(pretrained\_model, testset\_loader, criterion)  
           
             \# Epoch-level logs  
             comet\_model\_2.log\_metrics(  
                 {"train\_loss": train\_loss, "train\_acc": train\_acc,  
                  "val\_loss": val\_loss, "val\_acc": val\_acc},  
                 step=epoch  
             )  
           
             print(f"Epoch {epoch+1}: train\_loss={train\_loss:.4f} acc={train\_acc:.4f} | "  
                   f"val\_loss={val\_loss:.4f} acc={val\_acc:.4f}")  
           
             \# Save & log best checkpoint  
             if val\_acc \> best\_val\_acc:  
                 best\_val\_acc \= val\_acc  
                 torch.save({"state\_dict": pretrained\_model.state\_dict(), "num\_classes": num\_classes}, best\_path)  
                 comet\_model\_2.log\_model("resnet18\_pretrained\_best", best\_path)

         1. โค้ดนี้เป็น training loop สำหรับโมเดล ResNet-18 ที่ใช้ pretrained weights โดยจะทำการฝึกโมเดลบนข้อมูลฝึก (trainset\_loader) และประเมินผลการฝึกบนข้อมูล validation (testset\_loader) ในแต่ละ epoch รวมถึงการบันทึกผลการฝึกและการเซฟโมเดลที่มี accuracy ที่ดีที่สุดไว้

         

      4. ### Evaluate โมเดล {#evaluate-โมเดล-1}

         ใช้ฟังก์ชันเดียวกันกับ Randomly Initialized CNN model

6. # อธิบายวิธีใน train การและ dataset ที่เกี่ยวข้องและแหล่งที่มา {#อธิบายวิธีใน-train-การและ-dataset-ที่เกี่ยวข้องและแหล่งที่มา}

   1. ## วิธีในการเทรน  {#วิธีในการเทรน}

      1. ได้อธิบายในหัวข้อ “5.อธิบายโค้ด” แล้ว

   2. ## แหล่งข้อมูล (Dataset) {#แหล่งข้อมูล-(dataset)}

      1. ### Dataset {#dataset}

         1. [https://www.kaggle.com/datasets/sumn2u/garbage-classification-v2](https://www.kaggle.com/datasets/sumn2u/garbage-classification-v2)

      2. ### ลักษณะของ Dataset {#ลักษณะของ-dataset}

         1. เป็นภาพขยะในชีวิตประจำวัน ถ่ายจากมุมมองจริง (real-world images) ทำให้มีความหลากหลายของสี แสง และพื้นหลัง  
         2. ข้อมูลมีการจัดหมวดหมู่ (labeled) อย่างชัดเจน เหมาะสำหรับงานด้าน Computer Vision และ Deep Learning  
         3. แต่ละคลาสมีจำนวนตัวอย่างใกล้เคียงกัน ทำให้ไม่มีปัญหา class imbalance  
         4. ใช้สัญญาอนุญาตแบบ MIT License สามารถนำมาใช้งานทางวิชาการได้อย่างอิสระ  
         5. มีการอ้างอิงในงานวิจัย “Managing Household Waste Through Transfer Learning” ซึ่งแสดงให้เห็นถึงการใช้งานจริงในด้านระบบจัดการขยะอัจฉริยะ

      3. ### เหตุผลที่เลือกใช้ Dataset นี้ {#เหตุผลที่เลือกใช้-dataset-นี้}

         1. ครอบคลุมหมวดหมู่ของขยะที่พบในชีวิตประจำวันจริง  
         2. มีจำนวนภาพเพียงพอต่อการเทรนโมเดล CNN ให้เรียนรู้ pattern ได้ดี  
         3. มีความสมดุลของข้อมูลระหว่างคลาส ซึ่งช่วยให้การประเมินด้วย metric อย่าง Accuracy มีความน่าเชื่อถือ  
         4. สนับสนุนแนวคิด AI for Sustainability คือการนำ AI มาช่วยในด้านสิ่งแวดล้อมและการรีไซเคิล

7. # การประเมิน model {#การประเมิน-model}

   1. ## เกณฑ์การเลือก metric {#เกณฑ์การเลือก-metric}

      1. เนื่องจากชุดข้อมูล (dataset) ที่ใช้ในการฝึกและทดสอบโมเดลมีจำนวนตัวอย่างในแต่ละคลาสใกล้เคียงกัน จึงไม่มีปัญหาความไม่สมดุลของข้อมูล (class imbalance) ทำให้ Accuracy เป็นตัวชี้วัด (metric) ที่เหมาะสมในการประเมินประสิทธิภาพของโมเดล  
      2. ตารางเปรียบเทียบ metric ต่างๆ

| Metric | เหมาะกับกรณี | คำอธิบาย |
| ----- | ----- | ----- |
| Accuracy | ข้อมูลแต่ละคลาสมีจำนวนใกล้เคียงกัน | สัดส่วนตัวอย่างที่โมเดลทำนายถูกต้องทั้งหมด |
| Precision | สนใจ “ความถูกต้องของสิ่งที่โมเดลบอกว่าเป็นคลาสนั้น” | เช่น โมเดลบอกว่าเป็น “plastic” แล้วถูกจริงกี่ครั้ง |
| Recall | สนใจ “โมเดลจับคลาสนั้นได้ครบแค่ไหน” | เช่น จาก plastic ทั้งหมด โมเดลจับได้กี่เปอร์เซ็นต์ |
| F1-score | ข้อมูลไม่สมดุล หรืออยากสมดุล precision และ recall | ค่ากลางของ precision และ recall |

      

   2. ## กราฟ loss {#กราฟ-loss}

      1. Randomly Initialized CNN model  
         ![][image3]  
      2. pre-trained CNN model  
         ![][image4]  
       


       


   3. Confusion Matrix  
      ![][image5]  
   4. Per-class accuracy comparison  
      ![][image6]

      

8. # อ้างอิง {#อ้างอิง}

   1. ## Garbage Dataset {#garbage-dataset}

      1. [https://www.kaggle.com/datasets/sumn2u/garbage-classification-v2](https://www.kaggle.com/datasets/sumn2u/garbage-classification-v2)

   2. ## Waste Classification with CNN by Sashaank Sekar {#waste-classification-with-cnn-by-sashaank-sekar}

      1. [https://www.kaggle.com/datasets/techsash/waste-classification-data](https://www.kaggle.com/datasets/techsash/waste-classification-data)

   3. ## Waste Classification with CNN by Beyza Nur Nakkaş {#waste-classification-with-cnn-by-beyza-nur-nakkaş}

      1. [https://www.kaggle.com/code/beyzanks/waste-classification-with-cnn](https://www.kaggle.com/code/beyzanks/waste-classification-with-cnn)

9. # สัดส่วนงาน {#สัดส่วนงาน}

| ชื่อ-นามสกุล | รหัสนิสิต | สัดส่วนงาน |
| :---- | ----- | ----- |
| นาย ธนาธิป จินดามณี | 6610505411 | 50% |
| นาย ภากร ตันติวัฒนากุล | 6610505535 | 50% |
| รวม |  | 100% |

[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,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>

[image3]: <data:image/png;base64,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>

[image4]: <data:image/png;base64,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>

[image5]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAcYAAADNCAYAAAAi0tBeAAA/2klEQVR4Xu2dCbxNVfvHewu50aCkUGYqEa8UGSN3UObM85BUMoUImbnGS5oHzSpKKiUaDElJlEihEMmUBupNwz/rf3/r3L3Puc/e+97zrH3tc4fn9/l8P+fa+5xtD2ut757XaUoikUgkEomd0+gAiUQikUjyckSMEolEIpFERMQYkaNHj6oPP/xQfx47dkzt379fD1+/fr36v//7P/2JfPHFF5E/U8ePH9e/O3jwYLrhNHv37lWVK1emg9Plk08+oYNc89FHH9l/f/DBBxFjQvnpp5/oIDV16lQ6yE6DBg3oIFawvqz1E5mNGzeqrVu36r+//vpre939+OOPehlOnDih/z1t2jT7N5KcHWxblMkdO3bQUXZQXjLK7Nmz6SDPDBgwIN2/Ud42bNig/v3333TDaV588UXVpEkTOtjO77//Tgd5JrIOoszT/PDDD+n+bbUtXrn//vvpIFY+/fRTdeDAgXTDvvnmG71erKAubt68Wf/9+eefq02bNum/X3jhBd3e5eWIGNNy6NAhNWXKFP03CgtEV6lSJf3vEiVK6EpiVaKGDRtaP9O55ZZb9KclgC+//NIu+N9++60udH///bfq3bu3/tv63vbt2+3vb9u2Tf9tVcbPPvtM/fHHH/pviBq/i8zVV1+tVq5cqY4cOaJq166th+3cuVNPC2nbtq2uHJjG4cOHdWOFimL939YncvLkSV1pkC1btqjvv/9e/43fYj4gr7/++kv/jZ0At1x77bX6O/fee689bPDgwXraViDGn3/+WTeY2ElAypUrpz979eplf0+Ss7No0SJdZh5++GFdPlF+0Qj/8ssvuhyjTKBsWOUT39m1a5euK1a5RH1EUC5R7qxElk/UMZT5SDF26NDBli7K2f/+9z/9ezT0+P8xLyiHqI+o3/gO/o3g/8a8YR737Nljy+HPP//U0sA41E/sAH/11Vf2/4k0atRIf++JJ55QtWrV0sMwve+++07/XaZMGb0Odu/erecZdQWx6rUlJWTNmjV6/qw699tvv+nh+J01r5iOVddprHVIdxhWrVqlPzH9efPm2dO1guWbP3++/nvixInpxuW1iBjTQvdQIUYUalRMS4wovJBgpBjffvttXeGsPPvss1pEkydP1o1D0aJF9fAuXbqoUaNG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zzzzDB3EChobvw3OG2+8QQexAjFGexrBK+vXr6eD2PG7LrEtsU39ZPny5XSQRIXqCsqJnxw7dowOYgXb1++OLE6b+QnWgd8ylhV1/sknn6SDWPnjjz/oIHayQmr79u2jg0553n//fXsH6ZNPPlHbtm1TdevWJd/yTrYXo0QikUgkQSZXihF7nX73fH/66Sc6KCbxuxxffvklHcSO3z3frIjfo36Jd/yWMb+ntvH/Z5ft62ddbN26NUuWIzvUNz/rITck24px8+bNdBArjRo1Mt64+N20adPU9u3b6aiog2k899xzvk4L4d2zuNbhZznw/kzr3Zkm2bt3r6/fI2+99ZavU1Nff/213lH54Ycf6KiosnPnTn3xHadQTddlbk67du3oIFZwPc3PNXTIpEOHDr62zdNPP62vTfqZRqtWrfSpYJNpWHLH6TqT31vZuHGjrzYDNzSuW7eODmalX79+6ueffzZaDvwGdR33hpj8Prsk24nx+eefVzfeeKO+0cN072vUqFG6R4969erRUVHliy++0D0UYB5Mr8vh/P7ixYvVnXfeSUdlGhQo3GyDC8c4P2+6R963b19VvHhx9eOPP9JRUQU7J3fddZcaPHgwHRVVsP1++eUXVblyZf3vDRs2kG9knh07dujrzGj0brnlFjo6quzfv1+lpKRowaLhkIQzevRoNXv2bONrg6+88oq+oQrb2lSOuO6MMs+5BmQFv/vqq6/0zhe27aZNm+hXMg2mgZtMPvjgA31tyiS4Foc7Ht9880310ksv0dFR5fXXX9fTwGMGJoFUP//8c/1327Ztydjo8vDDD9s705CjSfB/46jXtL5mh2QrMUJGuM0WBXXp0qV0dFSByFA4hwwZQkdFFVQMFDBUkm+//ZaOjiroCuidd97RRzime03okQR70SZ7j2issNeHCoqjVtN5aN++vRYbBM8NGspBgwbp+cfevOkRI6SMnYwtW7bQUVFl6NChWvC7du0ybvxza9DjDbYPysdDDz1ER2caHMUDbFvTG5qqVKmiG9H58+cbl1P8FuXt6NGjdFRUwc5Xnz59dEPOPY2Jee7evbsuo4899phauHAh/UrUwc0iWA6THdmePXvqyya1atUy3pk/cuSI6tatm75ZhbserBw6dEiNGDEi02cTs3uyjRixMnH4vXv3br1yOZXE+u6tt96qKymOFk2ONnGL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>

[image6]: <data:image/png;base64,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a0KJF4270jURK10TStwbUVcTSlyEEvdDiStDiXsjamtCiReNu9I1EStdE0rcG1FXE0pchBL3Q4krQ4l7I2prQokXjbvSNRErXRNK3BtRVxNKXIQS90OJK0OJeyNqa0KJF4270jURK10TStwbUVcTSlyEEvdDiStDiXsjamtCiReNu9I1EStdE0rcG1FXE0pchBL3Q4krQ4l7I2prQokXjbvSNRErXRNK3BtRVxNKXIQS90OJK0OJeyNqaxKqxB944AHzwQcfmCuuuCIx7ZlnnjHvvvuueeyxxwosSYlHuHU1ocQllHiMFAO3tiaUuB+3tiairiaUuDeitiYhSvzkyZPm/vvvt9/369cvMb1KlSr2a9OmTRPTunTpYr73ve+Zc845x35Ndb5z7gWx873z/jt+LrpQtM2NW1eTi8/11NbE076Cufji1LRX1NXk4otE+3K1rYhbVxtRWxNP+9y4dTU579zvytrJ5vz/vA055/wLRe1kk5K2Ip72uXFrayLqanLBuaJtbty6mlxw7jmydrIpTlvPi/8+QERtTYqxTUg2F154ofn6668Tnk1a4mfOnDGNGze237dp0yYxvVatWvZrQYnnAlOnTnUnBUvp0qXdScFy5MgRc/ToUXdysFx22WXupGDZsmWLOX78uDs5WLp27epOCpaePXuaU6dOuZOD5MSJE2bKlCnu5GBp1KiR7ZnNFVasWOFOCpKkJQ7Qdd6nTx/bTd6hQwc77c033zTdu3c3L774orN02Pztb39zJwXL7bff7k4KFkgml0Rz5513upOCZdeuXYW600Jn2LBh7qRgGTlypDl9+rQ7OUi++eYb27WaKzzxxBP2IDBXWLt2rTspSFQSJ4QQQkj2ocQJIYSQHIUSD5Rc6nbCOUR0QxJy8OBBdxIhJI2cdRL//PPPc0KQy5Yty6kBQf379zevvPKKOzlIDhw4YEaMGOFODhK8V7FuC45GDRWcp69fv35OfL4i0FZcGhs6aCeyc+dOd1aQoK25MMg5eq9inEmuDGh0Oaskjn9Y1apV3cnB8t5775mVK1e6k4MDgvn1r39tatasaSZPnuzODg6089ixY2bu3LnBD2L67LPPzO7du+37YM2aNUELEm2DyHEfiVzYIGJ090MPPeRODg6sV6xPDGzF+zYXQFvR5o8++sjs37/fnR0M7dq1M++884557bXXTLNm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>