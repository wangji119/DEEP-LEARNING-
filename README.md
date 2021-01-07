# Machine Learning and Transportation
The purpose of this project is image classification.  
All folder names and file names in the project should not be changed. The folder data_set is the directory used to store the training samples, and it should be placed in the C:/Users. 
In this project, we compared two networks, RESNET and GoogleNet. The following picture shows the main structure of ALL ResNets：  
![RESNET](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/resnet34/RESNET.png)   

And the following picture shows the overall structure of GoogleNet：

![GoogleNet](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/resnet34/GoogleNet.png)



The steps for using data_set of RESNET are as follows:
------------------------
(1)Create a new folder "flower_data" under the data_set folder;  
(2)Click on the link to download the flower classification dataset:(http://download.tensorflow.org/example_images/flower_photos.tgz)；  
(3)Unzip the dataset into the flower_data folder;  
(4)Execute the "split_data.py" script to automatically split the dataset into a training set train and a validation set val.  

Here we use the 34-layer structure.

The following picture shows the structure of the basic block.

![BASICBLOCK](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/resnet34/BASICBLOCK.png)

e.g.: In the 34-layer residual structure, in conv2.x it is in 56x56x64  format, but in conv3.x it is in 28x28x128 format, so in conv3.1 the  dashed residual structure is used to downsample into the conv3.x format.

![DASHBLOCK](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/resnet34/DASHBLOCK.png)

We first define a class named BasicBlock which inherited from nn.Module.

Then we defined the convolution layer 1 using nn.conv2d. kener_size=3  can be seen in the basic block which is 3x3,64. bias=False means we used batchnormalization (bn). 

Then we defined the batchnormalization layer.

We used relu. 

The second convolutional layer is set up as described above 

Then we defined forward propagation function "forward". 

First input x, which is assigned to the shortcut output to the output value identity. 
if self.downsample is not None， identity = self.downsample(x). 【"dashed" residual structure】

Complete the forward propagation process based on the picture of the basic block.

For RESNET, the results of the three rounds of iterations are shown in the following figure:

![resnet iterations](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/resnet%20iterations.png)

For GoogleNet, the results of the 30 rounds of iterations are shown in the following figure:

![googlenet iterations](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/googlenet%20iterations.png)

The comparison shows that the results of RESNET after three iterations are comparable to the results of GoogleNet after 30 iterations. Therefore, we choose RESNET.

At last, we chose one picture of tulip from the network to test the performance of RESNET and GoogleNet.

![tulip](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/resnet34/tulip.jpg)

The result show that the RESNET thought it had 99.98 possibility to be tulip and GooglNet believes it has a 99.83% chance of being a tulip.

 It means RESNET has good performance in image classification.

We also visualized the results of RESNET.

The following figure shows how to access the visualization interface:

![进入可视化](https://github.com/fujunpeng/machine_learning_and_transportation_2020_project2/blob/main/figure/Visualization.png)



We have selected three images separately for prediction. It can be seen that the probability of successful prediction after one iteration is not high.

![一次迭代结果](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/1%20iterations.png)

After 4 iterations, the recognition results for daisies and tulips are unsatisfactory, while the recognition results for roses are very satisfactory.

![4次迭代结果](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/4%20iterations.png)



As the number of iterations increases, the recognition success rate for daisies and roses is very high after 20 iterations.

![20次迭代结果](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/20%20iterations.png)

After 30 iterations, the desired results were achieved for both daisies and roses, and the recognition of tulips was still unsatisfactory.

![30次迭代结果](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/30%20iterations.png)

The reason for the above results is that the features of roses are obvious and the background is not complicated; the features of daisies are obvious but the background is complicated, which affects the recognition result; the features of tulips are not obvious and the background is complicated, which makes the recognition result very poor. 

Here is the accuracy curve:

![accuracy](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/accuracy.png)

Here is the learning_rate curve:

![learning_rate](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/learning_rate.png)

Here is the train_loss curve:

![train_loss](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/train_loss.png)

We also visualized the weight changes. The following are two-dimensional and three-dimensional plots of the weight changes.

![二维权重变化](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/Two-dimensional.png)

![三维权重变化](https://raw.githubusercontent.com/fujunpeng/machine_learning_and_transportation_2020_project2/main/figure/Three-dimensional.png)
