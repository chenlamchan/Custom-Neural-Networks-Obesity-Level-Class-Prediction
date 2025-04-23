# Custom-Neural-Networks-Obesity-Level-Prediction

About:

This project is to build a classification prediction model to predict the classes of obesity based on the data of eating habits and physical conditions given as input.

### Dataset:
Details of the dataset selected for this application: 

**Name of dataset**: Estimation of Obesity Levels Based On Eating Habits and Physical Condition 

**Source**: UCI Machine Learning Repository 
(https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition) 

**Instances**: 2111 rows, 17 columns  

**Description of dataset**: Based on the information given on the source, selected dataset consists of 2111 rows, where each row corresponds to the eating habit and physical condition of one individual from the countries of Mexico, Peru and Colombia.

---

### Task: 
To build a classification prediction model to predict the classes of obesity based on the data of eating habits and physical conditions given as input.  

**Input feature**: 16 features 

feature name = [ Gender, Age, Height, Weight, family_history_with_overweight, FAVC, FCVC, NCP, CAEC, SMOKE, CH2O, SCC, FAF, TUE, CALC, MTRANS] 

**Target feature**: Obesity Level, 

classes = ['Normal_Weight', 'Overweight_Level_I', 'Overweight_Level_II', 'Obesity_Type_I', 'Insufficient_Weight', 'Obesity_Type_II', 'Obesity_Type_III']

![dataset_info](img/dataset.png)


### Model Development

Model used: Multilayer Perceptron (MLP) 
- MLP can learn high level and nonlinear patterns from the data.  
- Can be used solve a multi-class classification problem as well. 
- Able to reduce the extensive time-consuming manual feature engineering task. 

Table below shows the parameters defined in the model; justification will be discussed in the next section. 

![model_info](img/model.png)

a. Hidden layer: 4 layers with 16 neurons per layer.  
Activation function: relu 
Justification:

- For activation function, relu is selected as it is simple while able to avoid the vanishing gradient problem that slow down or stop the learning process. 
- For the number of hidden layer and neurons, they are selected based on the experiment to  determine the best combination of parameters by choosing the model that has the highest validation accuracy during training. 
- Refer to table below for the experiment log, strategy adopted as follow: 

**Experiment to search Optimal Parameter (Brute Force Search)**: 
o As a start, simple model is adopted by creating 1 hidden layer and nodes to be set half the number of features. 
o Then the model is trained to get it average maximum validation accuracy of training for a repeat of 3 times. Average of the average is computed as the final metric to compare between each model. 
o Next, continue to increase the number of nodes per layer slowly and if there is improvement on the validation accuracy. If minimal to no improvement observed, then increase the number of hidden layer and repeats the experiment. 
o At the same time, the epoch where the model stopped learning also being recorded to  monitor if the epoch is sufficient for model to learn. 
o As a result, hidden layer of 4 with neurons per layer of 16 (experiment no.8) is found  to be having highest average validation accuracy before it starts to degrade with neurons per layer of 20. (As shown in line chart below) 

![exp_info](img/table1_exp.png)

