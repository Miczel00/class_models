# class_models
In recent years, we have noticed a steady increase in the number of synthetic chemicals on the industrial market. The increasing number of chemicals entering the market in a way forces the need to develop effective methods for assessing chemical hazards, including their effects on human health, animal health and various components of the environment. Unfortunately, not all chemicals have been thoroughly tested for their toxicity and possible environmental impact. Conventional methods, including experimental studies using laboratory animals, are expensive, time-consuming, and ethically controversial. For this reason, machine learning methods based on classification methods, among others, are increasingly being used as alternative methods for assessing chemical risks. 
The research topic is the comparison of the effectiveness of selected machine learning techniques for classifying organic chemical compounds with different structural structures on the basis of acute toxicity to the Japanese ricefish (Latin: Oryzias latipes). 
The results of the study may contribute to the development of more efficient methods for preliminary chemical hazard assessment that are both more economical and environmentally friendly.

# Dataset used in my own research
The acute toxicity data on Oryzias latipes that I used in my thesis project, which I used to develop classification models, were taken from a publicly available database provided by Japan's Ministry of the Environment [15]. This ministry conducts extensive research on the effects of various chemicals on aquatic organisms, including Oryzias latipes. In the database in question, experimental 96-hour median lethal concentration (LC50) values are available for 384 organic compounds of varying structures (e.g., alcohols, aliphatic and aromatic hydrocarbons, alkyl and aryl halides, aldehydes, ketones, amides). The LC50 value is a commonly used indicator of the toxicity of chemicals and represents the concentration of a substance that causes the death of 50% of the population of test organisms after 96 hours of exposure.

# Modeling methods
An essential part of the modeling process is proper data preparation, which consists of autoscaling and dividing the input data set into a training set (T) and a validation set (V). I autoscaled the data with the StandardScaler function from the sklearn library available for the Python language...:

scaler = StandardScaler()
x_train = scaler.fit_transform(x_train)
x_test = scaler.transform(x_test)

As a result of the split, the input data (384 compounds) was divided into a training set of 256 compounds and a validation (test) set of 128 compounds. The two sets were unbalanced, as they differed in the number of compounds representing the classes "highly toxic" and "non-toxic or low-toxic"

# Selection of hyperparameters
The selection of appropriate parameters for classification algorithms plays a key role in achieving optimal classification results. There are many methods for parameter selection, such as GridSearchCV, RandomizedSearchCV, and optimization using metaheuristic algorithms. In my own research, I used the GridSearchCV algorithm for each classification modeling method. This is a popular parameter selection technique that involves testing all possible combinations of parameters within a specified range. To use the GridSearchCV technique to perform a parameter grid search for all classification models. 
For each method, the GridSearchCV parameters varied depending on what hyperparameters the classification model could take. The implementation of each model was done using the scikit-learn library in Python.

# Statistics describing the fit of the obtained classification models

| Model | Set          | Accuracy | Precision | Sensitivity | Statistic-F | MCC         | Specificity |
|-------|--------------|----------|-----------|-------------|-------------|-------------|-------------|
| SVM   | Training set | 0.89     | 0.89      | 0.93        | 0.91        | 0.76        | 0.82        |
|       | Test set     | 0.75     | 0.79      | 0.81        | 0.80        | 0.47        | 0.66        |
| k-NN  | Training set | 0.71     | 0.74      | 0.79        | 0.77        | 0.39        | 0.59        |
|       | Test set     | 0.78     | 0.80      | 0.85        | 0.83        | 0.54        | 0.68        |
| RF    | Training set | 0.93     | 0.95      | 0.94        | 0.94        | 0.86        | 0.93        |
|       | Test set     | 0.75     | 0.79      | 0.81        | 0.80        | 0.47        | 0.66        |

