# Classification-of-AML
## Description of Project
This is the early term project of BMED 6517, Georgia Institute of Technology. Our group members are Jincheng Zhu, Yuewen Zheng and Hanchen Wang. The goal of this project is to predict patient's AAML or normal status from patient blood samples profiled by flow cytomery.  
## Data
The data are drawn from 359 subjects, among whom 316 are normal while 43 are AML. For each subject, one blood sample is taken and split into 8 tubes. For each tube, 7 channels are measured (FSC, SSC, 5 protein markers). The 5 protein markers for each tube measure different kinds of proteins. (In total 5 * 8 = 40 kinds of proteins are measured.)  
Normal/AML class labels of 179 samples are given. The task is to predict the class labels of the remaining 180 samples.  
All data can be downloaded from http://pengqiu.gatech.edu/MLB/CSV.zip.  
**Noting that there are more than 10,000 rows of data in each of the 2872 csv files, which is far more than enough, and could slow down the program severely, I used only a part of them to make a smaller dataset. Also, in order to make an unbiased smaller dataset, I collected 1000 rows from each csv file which comes from a normal subject, and 7000 rows from each csv file which comes from an AML subject. In total, 317000 rows of data was collected, among which 161000 rows of data was collected from 23 AML subjects amd 156000 rows of data was collected from 156 normal subjects.**

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

Please run NeuralTraining.ipynb first to train the model. The model is saved to model.h5 and model_weights.h5. Then run NeuralTesting.ipynb to apply the testing data to the saved model to get the results. It takes about 75 minutes to sample from the csv files and train the neural network model.

## Method and Result
I used a merged 3-layer neural network for classification. Shown below is the network structure.  
![NN model structure](/model.png)
The training accuracy is about 94% while the validation accuracy is about 89%.  
|  | Pred: normal | Pred: AML |
| --- | --- | --- |
| Truth: normal | 146702 | 14298 |
|Truth: AML | 5750 | 150250 |

- Accuracy: 0.936757097791798  
- F-measure:0.9374571047081871  
- Balanced accuracy: 0.9371667861124384  
- MCC: 0.8748619424601002  
  
Among the 180 unlabeled subjects, my prediction is that 20 of them are AML while the others are normal. Please refer to 'AMLPrediction.csv' file for detailed results.  
- Subject 203 is AML. Confidence: 0.97  
- Subject 205 is AML. Confidence: 0.99  
- Subject 211 is AML. Confidence: 1.0  
- Subject 219 is AML. Confidence: 0.92  
- Subject 221 is AML. Confidence: 0.96  
- Subject 227 is AML. Confidence: 1.0  
- Subject 236 is AML. Confidence: 0.63  
- Subject 239 is AML. Confidence: 0.77  
- Subject 250 is AML. Confidence: 0.5  
- Subject 261 is AML. Confidence: 0.9  
- Subject 262 is AML. Confidence: 1.0  
- Subject 269 is AML. Confidence: 0.96  
- Subject 284 is AML. Confidence: 0.98  
- Subject 285 is AML. Confidence: 0.94  
- Subject 299 is AML. Confidence: 0.99  
- Subject 314 is AML. Confidence: 0.99  
- Subject 326 is AML. Confidence: 0.97  
- Subject 337 is AML. Confidence: 0.9299999999999999  
- Subject 344 is AML. Confidence: 0.77  
- Subject 348 is AML. Confidence: 1.0
