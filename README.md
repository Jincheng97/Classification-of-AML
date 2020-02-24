# Classification-of-AML
## Description of Project
This is the early term project of BMED 6517, Georgia Institute of Technology. Our group members are Jincheng Zhu, Yuewen Zheng and Hanchen Wang. The goal of this project is to predict patient's AML or normal status from patient blood samples profiled by flow cytomery.  
## Data
The data are drawn from 359 subjects, among whom 316 are normal while 43 are AML. For each subject, one blood sample is taken and split into 8 tubes. For each tube, 7 channels are measured (FSC, SSC, 5 protein markers). The 5 protein markers for each tube measure different kinds of proteins. (In total 5 * 8 = 40 kinds of proteins are measured.)  
Normal/AML class labels of 179 samples are given. The task is to predict the class labels of the remaining 180 samples.  
All data can be downloaded from http://pengqiu.gatech.edu/MLB/CSV.zip.  
**Noting that there are more than 10,000 rows of data in each of the 2872 csv files, which is far more than enough, and could slow down the program severely, I used only a part of them to make a smaller dataset. Also, in order to make an unbiased smaller dataset, I collected 1000 rows from each csv file which comes from a normal subject, and 7000 rows from each csv file which comes from an AML subject.** In total, 317,000 rows of data was collected, among which 161,000 rows of data was collected from 23 AML subjects amd 156,000 rows of data was collected from 156 normal subjects.  
p.s. I used Z-normalization on the first column "FS Lin", as the value of this column is much larger than the others.

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

Please run NeuralTraining.ipynb first to train the model. The model is saved to model.h5 and model_weights.h5. Then run NeuralTesting.ipynb to apply the testing data to the saved model to get the results. You can also just use the model file trained by myself, which can be loaded in NeuralTesting.ipynb. It takes **about 60 minutes** to sample from the csv files and train the neural network model.

## Method and Result
**I used a merged 3-layer neural network for classification.** Shown below is the network structure. **Each input is one row of data (7 features) from one of the 8 csv files.** For example, for the first training step, input1 could be the first row of "0001.csv", input2 could be the first row of "0002.csv", and input8 could be the first row of "0008.csv". For the second training step, take the second rows of the 8 csv files.  
![NN model structure](/model.png)
**The training accuracy is about 94% while the validation accuracy is about 89%.**  
|  | Pred: normal | Pred: AML |
| --- | --- | --- |
| Truth: normal | 146,702 | 14,298 |
|Truth: AML | 5,750 | 150,250 |

- Accuracy: 0.936757097791798  
- F-measure:0.9374571047081871  
- Balanced accuracy: 0.9371667861124384  
- MCC: 0.8748619424601002  
  
**In order to make a prediction on each of the 180 unknown subjects, I collected 1,000 rows of data from their 8 csv files respectively, and use each of the rows to make a vote, then predict based on the majority of votes.** For example, for subject No. 180, I fed the first row of data in from "1433.csv" to "1440.csv" (8 files) to the classifier. The result is that the normal_score for this row is 1597.8376 while the AML_score is 7.293128. Thus, the first row votes "normal" for subject No. 180. Then, I fed the 8 second rows to the classifier and get another vote. Keep doing this for the first 100 rows of the 8 csv files of subject No. 180. If there are more "normal" votes than "AML" votes, subject No. 180 should be predicted as "normal". (Vice versa.) I also defined a value "confidence" to represent the portion of AML votes among all votes.  
**Among the 180 unlabeled subjects, my prediction is that 20 of them are AML while the others are normal.** Please refer to 'AMLPrediction.csv' file for detailed results.  
- Subject 203 is AML. Confidence: 0.979
- Subject 205 is AML. Confidence: 0.991
- Subject 211 is AML. Confidence: 0.991
- Subject 219 is AML. Confidence: 0.9299999999999999
- Subject 221 is AML. Confidence: 0.993
- Subject 227 is AML. Confidence: 0.994
- Subject 236 is AML. Confidence: 0.654
- Subject 239 is AML. Confidence: 0.7070000000000001
- Subject 250 is AML. Confidence: 0.542
- Subject 261 is AML. Confidence: 0.9390000000000001
- Subject 262 is AML. Confidence: 0.999
- Subject 269 is AML. Confidence: 0.987
- Subject 284 is AML. Confidence: 0.964
- Subject 285 is AML. Confidence: 0.956
- Subject 299 is AML. Confidence: 0.991
- Subject 314 is AML. Confidence: 0.998
- Subject 326 is AML. Confidence: 0.911
- Subject 337 is AML. Confidence: 0.984
- Subject 344 is AML. Confidence: 0.733
- Subject 348 is AML. Confidence: 0.999
