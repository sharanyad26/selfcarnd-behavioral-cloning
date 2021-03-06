## Overview
The project uses training data generated by the simulator as input to the neural network to generate steering angle. keras is leveraged for the implementation of the neural network. This is a regression based problem. 

* model.py (Implements data processing, splitting data sets, creates the model, training and evaluation)
* drive.py (script to drive the car)
* model.json(generated as an output by running model.py)
* model.h5(weights generated as an output by running model.py) 


## Model Architecture

Summary of the model implemented to train the data.


        ____________________________________________________________________________________________________
		Layer (type)                     Output Shape          Param #     Connected to                     
		====================================================================================================
		convolution2d_1 (Convolution2D)  (None, 78, 158, 24)   1824        convolution2d_input_1[0][0]      
		____________________________________________________________________________________________________
		convolution2d_2 (Convolution2D)  (None, 37, 77, 36)    21636       convolution2d_1[0][0]            
		____________________________________________________________________________________________________
		convolution2d_3 (Convolution2D)  (None, 17, 37, 48)    43248       convolution2d_2[0][0]            
		____________________________________________________________________________________________________
		convolution2d_4 (Convolution2D)  (None, 15, 35, 64)    27712       convolution2d_3[0][0]            
		____________________________________________________________________________________________________
		convolution2d_5 (Convolution2D)  (None, 13, 33, 64)    36928       convolution2d_4[0][0]            
		____________________________________________________________________________________________________
		flatten_1 (Flatten)              (None, 27456)         0           convolution2d_5[0][0]            
		____________________________________________________________________________________________________
		dropout_1 (Dropout)              (None, 27456)         0           flatten_1[0][0]                  
		____________________________________________________________________________________________________
		activation_1 (Activation)        (None, 27456)         0           dropout_1[0][0]                  
		____________________________________________________________________________________________________
		dense_1 (Dense)                  (None, 1164)          31959948    activation_1[0][0]               
		____________________________________________________________________________________________________
		dropout_2 (Dropout)              (None, 1164)          0           dense_1[0][0]                    
		____________________________________________________________________________________________________
		activation_2 (Activation)        (None, 1164)          0           dropout_2[0][0]                  
		____________________________________________________________________________________________________
		dense_2 (Dense)                  (None, 100)           116500      activation_2[0][0]               
		____________________________________________________________________________________________________
		dense_3 (Dense)                  (None, 50)            5050        dense_2[0][0]                    
		____________________________________________________________________________________________________
		dense_4 (Dense)                  (None, 10)            510         dense_3[0][0]                    
		____________________________________________________________________________________________________
		dense_5 (Dense)                  (None, 1)             11          dense_4[0][0]                    
		====================================================================================================
		Total params: 32213367
		____________________________________________________________________________________________________

        

---

# Conclusion
The current implementation only takes center images as input, if the addtional camera images, left and right, are taken into consideration this might improve the performance and accuracy. Also, I have oly used one of the tracks in the simulator, might help to use data from both the tracks. The neural network architecture is laid out using the layers outlined in the summary above, which is based on the NVIDIA paper, trying out VGG or GoogLeNet approaches might improve the performace and accuracy. 

I have been testing this on my personal macbook, this definitely needs a much more powerful GPU machine to train the model with a larger dataset for better results.
