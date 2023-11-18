![](https://www.science.org/do/10.1126/science.aal1058/full/iStock-638581314_16x9-1644902880473.jpg)
# Predicting Heart Attacks with Machine Learning


Identifying the risk factors and predicting heart attacks before they happen is a crucial medical application that can be used to save lives! In this project, I explore the possibility of leveraging the latest machine learning advancement for this particular task. For this task, two different datasets are explored. The first dataset is a synthetic dataset generated by ChatGPT and the second dataset contains information of real patients

## Synthetic Dataset

This is the first dataset used for analysis. It is important to note that since this dataset is synthetically generated, there is no meaningful correlation between the features and the risk of heart attack and any machine learning model trained on this dataset will not be able to find meaningful relationships in the data to do better than "random guessing". As I will discuss later in this project, this does not mean that a machine learning model cannot "overfit" on this randomly generated dataset. Deep learning models with lots of parameters have the capacity to just memorize the training dataset and make almost perfect predictions on the training set, without being able to generalize to unseen data points. This dataset contains some notable features including the following:

* Age
* Cholesterol
* Heart Rate
* Diabetes
* Family History
* Smoking
* Obesity
* Alcohol Consumption
* Exercise Hours Per Week
* Previous Heart Problems
* Medication Use
* Stress Level
* Sedentary Hours Per Day
* Income
* BMI
* Triglycerides
* Physical Activity Days Per Week
* Sleep Hours Per Day
* Heart Attack Risk
* systolic
* diastolic
* Sex
* Diet
* Country
* Continent
* Hemisphere

In order to use this dataset for modeling I preprocessed this dataset by one-hot encoding categorical features and z-score normalizing numerical features. The data then is randomly split into train and validation sets.

### Deep Learning Modeling
A deep neural network model is created by using the TensorFlow's Keras library, containing of several dense layers with ReLU activations between them and a final dense layer with the sigmoid activation for the binary classification task at hand. This model is trained on the input features described above to predict the target label (heart attack risk). Since this dataset is synthetically generated by a random coing flip, it is impossible for any model to behave better than a random guess algorithm, but as shown below, a deep learning model is capable of "overfitting" even on a randomly generated dataset. Please see below training loss and accuracy graphs for training and validation sets accross epochs.

![image](https://github.com/MahsaBakhtiari/Heart_Attack-prediction/assets/125718782/370444f1-aa14-4a31-b6d3-ec05ee01df99)
)

## Real Dataset

The real challenge would be to train a machine learning model on a real dataset grabbed from real patients. For this purpose we use a heart attach risk dataset that contains real information from ~300 people and the following features for each person:

* Age
* Sex
* exang: exercise induced angina (1 = yes; 0 = no)
* ca: number of major vessels (0-3)
* cp: Chest Pain type chest pain type
  * Value 1: typical angina
  * Value 2: atypical angina
  * Value 3: non-anginal pain
  * Value 4: asymptomatic
* trtbps: resting blood pressure (in mm Hg)
* chol: cholestoral in mg/dl fetched via BMI sensor
* fbs: (fasting blood sugar > 120 mg/dl) (1 = true; 0 = false)
* rest_ecg: resting electrocardiographic results
  * Value 0: normal
  * Value 1: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV)
  * Value 2: showing probable or definite left ventricular hypertrophy by Estes' criteria
* thalach: maximum heart rate achieved
* target: 0= less chance of heart attack 1= more chance of heart attack

### Visualisation

The pair chart shows that the combination of thalachh(resting blood pressure) and age together and thall(Thal rate) by itself separates the two target labels efficiently. 
![](https://github.com/MahsaBakhtiari/Heart_Attack-prediction/blob/main/RealData/Plots/pairPlot.png)
 
Plotting the histogram of features shows their distributions.
![](https://github.com/MahsaBakhtiari/Heart_Attack-prediction/blob/main/RealData/Plots/distribution.png)

The boxplot shows the outliers of numerical features. As shown below, there are not as many outliers to intervene with the results.
![](https://github.com/MahsaBakhtiari/Heart_Attack-prediction/blob/main/RealData/Plots/boxPlot.png)

As shown below there is a high correlation between some features, for example, age and halacha (maximum heart rate achieved), that is expected; however, considering the primary modeling technique used for this project(deep learning) and a low number of features, we can afford to use all the features we have.
![](https://github.com/MahsaBakhtiari/Heart_Attack-prediction/blob/main/RealData/Plots/correlation.png)

### Deep Learning Modeling
A deep learning model was trained to predict heart attack risk using the features above. This model has six dense layers with reLu activation and a final dense layer with  a sigmoid activation function that outputs the probability of heart attack. This model was trained with binary cross entropy loss and Adam optimizer with the learning rate of 1e-4 and  weight decay of 1e-2 to help with overfitting. 
The model achieved 87% accuracy on  both the train and test sets. 
![](https://github.com/MahsaBakhtiari/Heart_Attack-prediction/blob/main/RealData/Plots/train_test_validations.png)

### Random Forest Model

A random forest classifier was trained on the real data and achieved the same accuracy as the NN model. The most important features are shown below. 

![](https://github.com/MahsaBakhtiari/Heart_Attack-prediction/blob/main/RealData/Plots/featureimportance.png)








## References

*(Real Data) https://www.kaggle.com/datasets/rashikrahmanpritom/heart-attack-analysis-prediction-dataset/code 

*(Synthetic Data) https://www.kaggle.com/datasets/iamsouravbanerjee/heart-attack-prediction-dataset
