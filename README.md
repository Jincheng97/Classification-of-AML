# Classification-of-AML
## Description of Project
This is the early term project of BMED 6517, Georgia Institute of Technology. Our group members are Jincheng Zhu, Yuewen Zheng and Hanchen Wang. The goal of this project is to predict patient's AAML or normal status from patient blood samples profiled by flow cytomery.  
## Data
The data are drawn from 359 subjects, among whom 316 are normal while 43 are AML. For each subject, one blood sample is taken and split into 8 tubes. For each tube, 7 channels are measured (FSC, SSC, 5 protein markers). The 5 protein markers for each tube measure different kinds of proteins. (In total 5 * 8 = 40 kinds of proteins are measured.)  
Normal/AML class labels of 179 samples are given. The task is to predict the class labels of the remaining 180 samples.  
All data can be downloaded from http://pengqiu.gatech.edu/MLB/CSV.zip.  
## Tips for running the codes
After downloading all data, please put all csv files and ipynb files in file folders with a structure shown below.  
In the project file folder there are
- .\Classification-of-AML\  
	- NeuralTraining.ipynb  
	- NeuralTesting.ipynb  
	- (model_weights.h5)  
	- (model.h5)  
	- AMLTraining.csv  
	- .\CSV\  
		- 0001.CSV  
		- 0002.CSV  
		...  
		...  
		...  
		- 2872.CSV  
Please run NeuralTraining.ipynb first to train the model. The model is saved to model.h5 and model_weights.h5. Then run NeuralTesting.ipynb to apply the testing data to the saved model to get the results.
## Method and Result
I used a merged 3-layer neural network for classification. Shown below is the network structure.  
![NN model structure](/model.png)
The training accuracy is about 94% while the validation accuracy is about 89%.  
Among the 180 unlabeled subjects, my prediction is that 20 of them are AML while the others are normal. Please refer to 'AMLPrediction.csv' file for detailed results.
