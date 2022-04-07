# The Diamond Price teller 

<p align="center"><img src="https://www.ardeaprints.com/p/172/dog-jack-russell-terrier-dressed-fortune-teller-13483864.jpg"></p>



### :raising_hand: **Hello and welcome to the diamond price teller** 
In this repository I am going to share and explain how I have faced the challenge of prediction of diamond prices in the kaggle competition of Ironhack: https://www.kaggle.com/competitions/dataptmad1121/leaderboard.

The goal is simple, find the best model that will predict the prices of a dataset of diamonds based on the already available data.


### :bookmark_tabs: **Step1: Data available**
The data provided in the competition has been: 

<ol>
  <li>diamonds_train.db - the training set</li>
  <li>diamonds_test.csv - the test set</li>
  <li>sample_submission.csv - a sample submission file in the correct format.</li>
  <li>Fourth item</li>
</ol>

This data can be found under the data folder. 

In order to read the diamonds_train and obtain the diamonds_train.csv that will be read from the notebooks afterwards, DBeaver has been used 

<p align="center"><img src="./images/DBeaver.png"></p>


### :running: Step 2: First attempt or keeping things simple

In order to understand the baseline, I started testing the first most simple estimation possible: 
- Model: LinearRegression 
- Categorical variables transformed to numerical ones via pd.get_dummies
- Scaled the data using scaler.fit_transform

The steps followed are detailed in notebook  :page_with_curl: 1_First_attempt under :open_file_folder:notebook folder. 

And just like that :tada::

<p align="center"><img src="./images/first_attempt.png"></p>


### :surfer: Step 3: Different models - winner RandomForestRegressonr

The next thing I did was to test different models and evaluate the impact it had on my error calculated as rmse: 

*Models tested* 

model1 = LinearRegression()
model2 = linear_model.Lasso()
model3 = ElasticNet()
model4 = Ridge()
model5 = SVR()
model6 = SGDRegressor()
model7= RandomForestRegressor(max_depth=12)
model8= ExtraTreesRegressor(n_estimators=15)


Also, *hyperparams* where also modified on a different range of values as max_depth or n_estimators

<p align="center"><img src="./images/models.png"></p>

The steps followed are detailed in notebook  :page_with_curl: 2_Different_models under :open_file_folder:notebook folder. 

And just like that:bomb::

<p align="center"><img src="./images/models_kaggle.png.png"></p>

The difference was almost none and in some cases the error even increased. 
I decided to move on using the model that reduced to the maximum my error, from a value of aprox 1600 to 1200: :purple_heart: *RandomForestRegressor* :purple_heart:



### :bath: Step 4: Data cleaning 

Following the model selection, a common step to take is to analyse the data to remove outliers, values that do not make sense or values that are repeating the same information (very high correlation). 

Some of the data cleaning I tested:

- Remove highly correlated features: x,y,z 
- Plot different combination of features and manually remove outliers

The steps followed are detailed in notebook  :page_with_curl: 3_Data_cleaning under :open_file_folder:notebook folder. 


```
:bulb: The sad truth was that the estimations were worse 
which made me realise that I was facing an *underfitting model*
and decided to continue without any cleaning in my dataset. 
        
```
<p align="center"><img src="https://media.istockphoto.com/photos/muddy-golden-retriever-picture-id492264227?k=20&m=492264227&s=612x612&w=0&h=jc8C1jpWKc6jr2uDgb6Q-Q7QKb7G9Dhtvnx1pa1W6VA="></p>



### :hammer: Step 5: Adding features 

After realising that I was in an underfitting situation with my model, I decided to test different combination of my features and identify if some of those relationships might help my model predict better.  

Here I found a really unexpected surprise!

<p align="center"><img src="./images/feature_creation.png.png"></p>

```
:bulb: In this step one engineered feature made my error reduce from an average of 1000 to 600
This feature was Clarity-Color which makes sense that some relationship between both might be relevant.  
        
```
The steps followed are detailed in notebook  :page_with_curl: 4_Adding_features under :open_file_folder:notebook folder.



### :factory: Step 6: test, test and test! 

What comes next was just a chaotic process trying different possibilities keeping in mind that:
- I was in an underfitting situation 
- That cleaning my dataset was not helping
- Adding new relationship between features was helpful
- Testing hyperparameters had small impact (range of 10x)



And that is how the two final models have been chosen :smiley:.




















