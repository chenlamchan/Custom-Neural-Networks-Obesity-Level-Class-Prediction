# Custom-Neural-Networks-Obesity-Level-Prediction

About:

This project is to build a classification prediction model to predict the classes of obesity based on the data of eating habits and physical conditions given as input.

### Dataset:
Details of the dataset selected for this application: 

**Name of dataset**: Estimation of Obesity Levels Based On Eating Habits and Physical Condition </br> 
**Source**: UCI Machine Learning Repository 
(https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition) </br> 
**Instances**: 2111 rows, 17 columns  </br> 
**Description of dataset**: Based on the information given on the source, selected dataset consists of 2111 rows, where each row corresponds to the eating habit and physical condition of one individual from the countries of Mexico, Peru and Colombia.

---

### Task: 
To build a classification prediction model to predict the classes of obesity based on the data of eating habits and physical conditions given as input.  

**Input feature**: 16 features; </br> 
feature name = [ Gender, Age, Height, Weight, family_history_with_overweight, FAVC, FCVC, NCP, CAEC, SMOKE, CH2O, SCC, FAF, TUE, CALC, MTRANS] 

**Target feature**: Obesity Level; </br> 
classes = ['Normal_Weight', 'Overweight_Level_I', 'Overweight_Level_II', 'Obesity_Type_I', 'Insufficient_Weight', 'Obesity_Type_II', 'Obesity_Type_III']

| Variable | Description | Data Type | Unique Value for Categorical Variable | Missing Value |
| :--- | :--- | :--- | :--- | :--- |
| **Gender** | Gender | Categorical | ['Female', 'Male'] | No |
| **Age** | Age | Continuous | - | No |
| **Height** | Height, in m | Continuous | - | No |
| **Weight** | Weight, in kg | Continuous | - | No |
| **family_history_with_overweight** | Has a family member suffered or suffers from overweight? | Binary | ['yes', 'no'] | No |
| **FAVC** | Do you eat high caloric food frequently? | Binary | ['no', 'yes'] | No |
| **FCVC** | Do you usually eat vegetables in your meals? | Integer | - | No |
| **NCP** | How many main meals do you have daily? | Continuous | - | No |
| **CAEC** | Do you eat any food between meals? | Categorical | ['Sometimes', 'Frequently', 'Always', 'no'] | No |
| **SMOKE** | Do you smoke? | Binary | ['no', 'yes'] | No |
| **CH2O** | How much water do you drink daily? | Continuous | - | No |
| **SCC** | Do you monitor the calories you eat daily? | Binary | ['no', 'yes'] | No |
| **FAF** | How often do you have physical activity? | Continuous | - | No |
| **TUE** | How much time do you use technological devices such as cell phone, videogames, television, computer and others? | Integer | - | No |
| **CALC** | How often do you drink alcohol? | Categorical | ['no', 'Sometimes', 'Frequently', 'Always'] | No |
| **MTRANS** | Which transportation do you usually use? | Categorical | ['Public_Transportation', 'Walking', 'Automobile', 'Motorbike', 'Bike'] | No |
| **NObeyesdad** | Obesity level | Categorical | ['Normal_Weight', 'Overweight_Level_I', 'Overweight_Level_II', 'Obesity_Type_I', 'Insufficient_Weight', 'Obesity_Type_II', 'Obesity_Type_III'] | No |


## Model Development

Model used: **Multilayer Perceptron (MLP)** 
- MLP can learn high level and nonlinear patterns from the data.  
- Can be used solve a multi-class classification problem as well. 
- Able to reduce the extensive time-consuming manual feature engineering task. 

Table below shows the parameters defined in the model; justification will be discussed in the next section. 

| Parameters | Values |
| :--- | :--- |
| **Number of Hidden Layer** | 4 |
| **Number of neurons per layer** | 16 |
| **Activation function of hidden layer** | Relu |
| **Output Layer neurons** | 7 |
| **Activation function of output layer** | Softmax |
| **Learning rate** | Determined by optimiser (‘adam’) |
| **Loss function** | SparseCategoricalCrossentropy |
| **Early Stopping** | 10 |
| **Batch size** | 8 |

**a. Hidden layer: **4** layers with **16** neurons per layer.**  
Activation function: relu </br>
Justification:
- For activation function, relu is selected as it is simple while able to avoid the vanishing gradient problem that slow down or stop the learning process. 
- For the number of hidden layer and neurons, they are selected based on the experiment to  determine the best combination of parameters by choosing the model that has the highest validation accuracy during training. 
- Refer to table below for the experiment log, strategy adopted as follow: 

**Experiment to search Optimal Parameter (Iterative Brute Force Search)**: 

- As a start, simple model is adopted by creating 1 hidden layer and nodes to be set half the number of features. </br> 
- Then the model is trained to get it average maximum validation accuracy of training for a repeat of 3 times. Average of the average is computed as the final metric to compare between each model. </br> 
- Next, continue to increase the number of nodes per layer slowly and if there is improvement on the validation accuracy. If minimal to no improvement observed, then increase the number of hidden layer and repeats the experiment. </br> 
- At the same time, the epoch where the model stopped learning also being recorded to  monitor if the epoch is sufficient for model to learn. </br> 
- As a result, hidden layer of 4 with neurons per layer of 16 (experiment no.8) is found  to be having highest average validation accuracy before it starts to degrade with neurons per layer of 20. (As shown in line chart below) </br> </br>

Optimal Params (Hidden Layer): </br>
![param_info](img/params_search_result.png)

Experiment log:</br> 
| Experiment No. | Hidden Layer | Nodes per layer | Description | Final Epoch No. | Training Accuracy | Validation Accuracy (3 repeats/each trial) | Average Validation Accuracy | Differences |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | 1 | 8 | EarlyStopping = 5<br>epoch = 300 | 180<br>258<br>300 | 0.7104 +/- 0.0216<br>0.7443 +/- 0.0212<br>0.7178 +/- 0.0335 | 0.7095 +/- 0.0216<br>0.7568 +/- 0.0212<br>0.7173 +/- 0.0335 | 0.7095 | - |
| **2** | 1 | 12 | EarlyStopping = 5<br>epoch = 300 | 136<br>166<br>119 | 0.7299 +/- 0.0224<br>0.7615 +/- 0.0155<br>0.7491 +/- 0.0111 | 0.7376 +/- 0.0224<br>0.7601 +/- 0.0155<br>0.7635 +/- 0.0111 | 0.7376 | 3.96% |
| **3** | 1 | 16 | EarlyStopping = 5<br>epoch = 300 | 164<br>120<br>90 | 0.7364 +/- 0.0368<br>0.7364 +/- 0.0205<br>0.7138 +/- 0.0294 | 0.7297 +/- 0.0368<br>0.7410 +/- 0.0205<br>0.7151 +/- 0.0294 | 0.7297 | -1.07% |
| **4** | 2 | 12 | EarlyStopping = 5<br>epoch = 300 | 160<br>198<br>134 | 0.7423 +/- 0.0325<br>0.8047 +/- 0.0432<br>0.7739 +/- 0.0086 | 0.7376 +/- 0.0325<br>0.7962 +/- 0.0432<br>0.7658 +/- 0.0086 | 0.7376 | 1.08% |
| **5** | 2 | 16 | EarlyStopping = 5<br>epoch = 300 | 117<br>129<br>124 | 0.7671 +/- 0.0193<br>0.7906 +/- 0.0191<br>0.7784 +/- 0.0309 | 0.7680 +/- 0.0193<br>0.7894 +/- 0.0191<br>0.7725 +/- 0.0309 | 0.7680 | 4.12% |
| **6** | 3 | 16 | EarlyStopping = 5<br>epoch = 300 | 108<br>126<br>114 | 0.7861 +/- 0.0100<br>0.7999 +/- 0.0302<br>0.7776 +/- 0.0526 | 0.7804 +/- 0.0100<br>0.7917 +/- 0.0302<br>0.7849 +/- 0.0526 | 0.7857 | 2.30% |
| **7** | 3 | 20 | EarlyStopping = 5<br>epoch = 300 | 111<br>100 | 0.7759 +/- 0.0329<br>0.8129 +/- 0.0078<br>0.7880 +/- 0.0270 | 0.7815 +/- 0.0329<br>0.8142 +/- 0.007<br>0.7736 +/- 0.0270 | 0.7898 | 0.52% |
| **8** | **4** | **16** | **EarlyStopping = 5**<br>**epoch = 300** | **135**<br>**131**<br>**101** | **0.8005 +/- 0.0382**<br>**0.8019 +/- 0.0531**<br>**0.7903 +/- 0.0212** | **0.8153 +/- 0.0382**<br>**0.8052 +/- 0.0531**<br>**0.8063 +/- 0.0212** | **0.8089** | **2.43%** |
| **9** | 4 | 20 | EarlyStopping = 5<br>epoch = 300 | 60<br>100<br>90 | 0.7787 +/- 0.0298<br>0.7906 +/- 0.0129<br>0.7945 +/- 0.0063 | 0.7804 +/- 0.0298<br>0.7905 +/- 0.0129<br>0.8007 +/- 0.0063 | 0.7905 | -2.27% |
| **10** | 5 | 16 | EarlyStopping = 5<br>epoch = 300 | 92<br>59<br>69 | 0.7708 +/- 0.0148<br>0.7655 +/- 0.0018<br>0.7779 +/- 0.0128 | 0.7950 +/- 0.0148<br>0.7703 +/- 0.0018<br>0.7860 +/- 0.0128 | 0.7838 | -0.86% |


**b. Output Layer: 1 layer with 7 neurons; Activation function: softmax** </br>
Justification:

- In output layer, 7 neurons are set due to the number of classes to be predicted is 7 classes.  
- Softmax activation function is used for the purpose of multi-class classification task as it would 
be able to produce output as the probabilities for each class. </br>

**c. Learning rate: Utilise Adaptive Moment Estimation (adam)** </br>
Justification: 
- To save time and effort on experimenting, an optimizer is selected to adjust the learning rate 
dynamically based on the historical gradient magnitudes.</br></br>

**d. Loss function: Sparse Categorical Cross Entropy** </br>
Justification:
- As this is a multiclass classification problem, categorical cross entropy is selected as the loss 
function to minimise the difference between true and predicted distributions by penalizing 
incorrect predictions effectively. Sparse type is used to in the target variable, it is provided as 
integers instead of one-hot encoded vectors. </br></br>

**e. Batch_size = 8, Early_Stopping = 10**  </br>
Justification: 
- To improve the model by enhancing the learning of model.

**Experiment to improve model (Iterative Brute Force Search)**: 
- After the optimal number of layers and neurons per layer are found, experiment was  done to enhance the training of the model. 
- Batch_size parameter was used in training to allow more weight updates of the model. 
- Early stopping criteria is added in training to preserve the resource of training and stopped automatically when there are 10 iterations with no significant improvement in 
its learning. </br></br>

Optimal Params (Early Stoping,Batch Size): </br>
![param_info](img/params_search_result2.png)

Experiment log:</br> 
| Experiment No. | Hidden Layer | Nodes per layer | Description | Final Epoch No. | Training Accuracy | Validation Accuracy | Average Validation Accuracy | Differences |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Benchmark** | 4 | 16 | EarlyStopping = 5<br>epoch = 300 | 135<br>131<br>101 | 0.8005 +/- 0.0382<br>0.8019 +/- 0.0531<br>0.7903 +/- 0.0212 | 0.8153 +/- 0.0382<br>0.8052 +/- 0.0531<br>0.8063 +/- 0.0212 | 0.8089 | - |
| **13** | 4 | 16 | EarlyStopping = 5<br>epoch = 300<br>Batch_size=8 | 64<br>71<br>59 | 0.7996 +/- 0.0191<br>0.8112 +/- 0.0038<br>0.7804 +/- 0.0169 | 0.8142 +/- 0.0191<br>0.8277 +/- 0.0038<br>0.8074 +/- 0.0169 | 0.8164 | 0.93% |
| **14** | **4** | **16** | **EarlyStopping = 10**<br>**epoch = 300**<br>**Batch_size=8** | **118**<br>**93**<br>**107** | **0.8566 +/- 0.0042**<br>**0.8321 +/- 0.0239**<br>**0.8242 +/- 0.0184** | **0.8671 +/- 0.0042**<br>**0.8592 +/- 0.0239**<br>**0.8356 +/- 0.0184** | **0.8540** | **4.60%** |
| **15** | 4 | 16 | EarlyStopping = 10<br>epoch = 300<br>Batch_size=16 | 123<br>169<br>156 | 0.8391 +/- 0.0012<br>0.8326 +/- 0.0321<br>0.8400 +/- 0.0140 | 0.8615 +/- 0.0012<br>0.8390 +/- 0.0321<br>0.8491 +/- 0.0140 | 0.8499 | -0.48% |

## Code Execution
 Classification Steps </br>
These are the steps to be performed in classification </br>
Step 1: Data Cleaning </br>
Sanity checks on the data has been performed:
- Missing value: No missing values are found. 
- Inconsistent value: There is no inconsistency found in the categorical value. 
- Extreme value: No abnormal extreme value found in numerical variables. </br>

Step 2: Feature Engineering (Data Encoding) </br>
The categorical variables below are encoded to numerical values:

| Variables | Encoding |
| :--- | :--- |
| **Gender** | Female: 0<br>Male: 1 |
| **family_history_with_overweight**<br>**FAVC**<br>**SMOKE**<br>**SCC** | no: 0<br>yes: 1 |
| **CAEC**<br>**CALC** | no: 0<br>Sometimes: 1<br>Frequently: 2<br>Always: 3 |
| **MTRANS** | Walking: 0<br>Public Transportation: 1<br>Bike: 2<br>Motorbike: 3<br>Automobile: 4 |
| **NObeyesdad** | Insufficient Weight: 0<br>Normal_Weight: 1<br>Overweight_Level_I: 2<br>Overweight_Level_II: 3<br>Obesity_Type_I: 4<br>Obesity_Type_II: 5<br>Obesity_Type_III: 6 |

Step 3: Feature Selection </br>
In this study, all of the features will be selected as input to the prediction model. 

Step 4: Training & Test Dataset Split </br>
In this stage, the dataset will be split into training set and test set with test size 
of 30%. Train_test_split function from scikit-learn library is utilized for the data split. 
Stratify split is used and based on the target class to ensure the training and testing set 
has the similar class distribution. Training dataset will be used in model training, while 
testing dataset will be used in model evaluation. </br>

Step 5: Model Training </br>
In this stage, experiment to search for the optimal parameter for model and the 
enhance learning of model to be conducted. Detailed as discussed in section 3.0. After 
the model parameters are determined and fixed, a final training iteration of model will 
be conducted for 20 epochs. This is to get the best model out of the training, by saving 
the best model through enabling the ModelCheckpoint function from tensorflow keras. </br>

Step 6: Model Evaluation </br>
In this stage, the best model will be loaded and used to predict the input data, 
the testing dataset. Then, the accuracy score and classification report will be computed 
to quantify the performance of the prediction model. </br>

## Result 
The accuracy of this model measured using the test dataset is 87.22%. 
And the table below shows the classification report of the prediction model.

| Class | Precision | Recall | F1-Score | Support |
| :--- | :--- | :--- | :--- | :--- |
| **0** | 0.90 | 0.95 | 0.92 | 82 |
| **1** | 0.91 | 0.67 | 0.77 | 86 |
| **2** | 0.69 | 0.77 | 0.73 | 87 |
| **3** | 0.75 | 0.77 | 0.76 | 87 |
| **4** | 0.90 | 0.94 | 0.92 | 106 |
| **5** | 0.98 | 0.97 | 0.97 | 89 |
| **6** | 0.99 | 1.00 | 0.99 | 97 |
| | | | | |
| **Accuracy** | | | **0.87** | 634 |
| **Macro Avg** | 0.87 | 0.87 | 0.87 | 634 |
| **Weighted Avg** | 0.88 | 0.87 | 0.87 | 634 |

Based on the classification report, class 0 ('Insufficient_Weight'), 4 ('Obesity_Type_I'),5 ('Obesity_Type_II') and 6 ('Obesity_Type_III') show a very good performance, with F1-scores above 0.90. There is room for improvement in terms of the class 1 ('Normal_Weight'), class 2 ('Overweight_Level_I') and 3 ('Overweight_Level_II').  Further investigation of the prediction on class 1,2,3 is required such as to conduct exploratory data analysis on the interaction between these 3 classes. There could be overlapping features or insufficient representation in the training data. 
