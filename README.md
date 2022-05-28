### PROJECT-ENGAGE
In my project I am using the dataset given in the acehacker site itself.
CONTENTS:

1)DATA PROCESSING:

  -1.1) CLEANING OF DATA
  
  -1.2) DENSITY PLOT
  
  2) DATA VISUALIZATION:

   -2.1)ANALYZYING NON NUMERICAL DATA
   
   -2.2)ANALYZYING THE NUMERICAL DATA:-
   
        *2.2 a) DATA PROCESSING
        
        *2.2 b)CORELATION
        
   -2.3)FEATURE TO FEATURE RELATION
   
   -2.4)Quantitative to Quantitative relationship
   
   -2.5)Categorical to Quantitative relationship
   
3) APPLYING REGRESSION MODELS:

  -3a) MULTIPLE LINEAR REGRESSION
  
  -3b) DECISION TREE REGRESSION
  
  -3c) RANDOM FOREST REGRESSION
  
  -3d) SUPPORT VECTOR MACHINE
  
4) GROUPING CARS:

  -4.1) Grouping different models of cars on the basis of luxury features and their ex-showroom price
  
  -4.2) Grouping different models of cars on the basis of thier numerical features
  
  
 IN MY JUPYTER NOTEBOOK I WRITTEN CODE FOR ALL THE GRAPHS THAT I HAVE ADDED HERE!
  
# 1)DATA PROCESSING: 
After including libraries and importing dataset we will begin with cleaning of data.

## 1.1) CLEANING OF DATA-
By closely looking at the dataset we can see that many columns have same values throughout, like for Fuel_System it is Injection. So it is better to remove these features.

We can also see that a lot of data is missing. So our next step will be to remove features which have missing value greater than 30%.

If you closely look at these features, we can see that these can be described as luxury features as these are not present in every car, but the greater the price, the greater these features will be available. So we will store these features in a new dataset 'DF'.

Now if we look at our dataset, we can see that only Ex-showrrom_Price can be treated as dependent varaible. So we will shift it to the last column.

## 1.2) DENSITY PLOT-
By looking at the density plot of a feature we can find out the probability of finding a getting a value.
We are plotting the density plot of Ex-showrrom_Price so we can see how it is distruibuted. We can also find the probability of getting a value of Ex-showrrom_Price by looking at this graph.

![a1](https://user-images.githubusercontent.com/105349293/170811814-d794d9a6-9d27-461c-aa97-747561fbe880.png)

WHY ARE WE PLOTTING THIS?

The main reason why we are plotting this graph is to find the nature of its distribution so when we fill the missing data, we can take a hint that which filler is to be used. Like if we have skewed data, then we will use median as filler.
## OBSERVATIONS:
-We see that the above graph is skewed, so maybe the appropriate distribution can be log or log normal distribution.

-Here density represents frequency of Ex-Showroom_Price

If we try to use describe on our dataset, we will see that a few values have appered. But we know there is a lot of numerical data which is the form of strings. So we will convert these strings into dtype float and then fill the missing values.
So we will go on step by step. 

# 2) DATA VISUALIZATION

## 2.1) ANALYZYING NON NUMERICAL DATA-
When we describe the complete dataset, we can see that maximum models are of maruti suzuki company.

In non numerical features only a few features have non null elements. So we will plot these festures and see what we can find out.

NOTE: We plot 'Make AND Ex-Showroom_Price' ; 'Body_Type AND Ex-Showroom_Price' and 'Drivetrain AND Ex-Showroom_Price'.
While plotting Body_Type AND Ex-Showroom_Price we saw that we could not deduce much from boxplot so we used catplot instead.
## OBSERVATIONS:
-Lamborghini,Bentley,Ferrari,Aston Martin,Bugatti produces most expensive cars( Rs. 3,00,00,000 and above)

-Volve Make, Jaguar,BMW,Maserati,Audi,Lexus make comparitevly less expensive luxury cars.

-Other companies like Tata,Maruti etc produce budget models with lower prices.

-Sports model are expensive in prices followed by convertible and coupe body style

-Convertible has only standard edition with expensive cars

-rwd wheel drive vehicle have expensive prices

## 2.2) ANALYZYING THE NUMERICAL DATA-
Before we analyze our numerical data we need to clean the data and fill missing values.

## 2.2 a) DATA PROCESSING:
Here we have three classes make,modeland varaint. So lets convert them into 1 ,i.e model and remove others and then apply one hot coding on model to convert it into numerical data.

Now we see that most of our numerical data is in form of strings. So we will convert them into dtype float.

-REMOVING STRINGS:

So here we will remove the strings and then convert the numerical data from dtype object to float. eg- We have displacements as 624 cc; so here we will remove ' cc' from it and then convert it into float type.

-CONVERTING THEM INTO FLOAT DType:

We will convert them into dtype flote using astype.

-CREATING A NUMERICAL DATASET:

Now we will create a new dataset as 'dataset_num' which will contain all numerical data.
-REPLACING NAN WITH MEDIAN;

Since we are done with making a numerical dataset. Now we will replace the missing values in this dataset with median. Here we are replacing nan with median since this is a bigdata and when we plotted the density graph of ex-showroom_price we saw that the graph was skewed. And we know that for skewed graph, median filler is preferrable

## 2.2 b)CORELATION:
Generally we use bivarete plots to find relation between different features. But swince we have a lot of features I thought using corelation will be a better way to find which features are strongly related to the dependent variable.
So we conclude that there are 2 strongly correlated values with Ex-Showroom_Price:
Cylinders       0.817001
Displacement    0.793142

Then I created a dataset containing just the attributes 'df_attr' , i.e it doesnot contains model of cars and tried to plot a bivarte plot for this dataset.
## OBSERVATION
We can clearly identify some relationships. Most of them seems to have a linear relationship with the exshowroom price and if we look closely at the data we can see that a lot of data points are located on x = 0 which may indicate the absence of such feature in the cars like airbags. So now lets remove these 0 values and repeat the process of finding correlated values:

Even after further cleaning our data i found out that displacement and cylinders are strongly corelated to the ex showroom price.

## 2.3)FEATURE TO FEATURE RELATION-
Trying to plot all the numerical features in a seaborn pairplot will take us too much time and will be hard to interpret. We can try to see if some variables are linked between each other and then explain their relation.
So i created a heat map which looks like this:
![a2](https://user-images.githubusercontent.com/105349293/170816228-8c8ac2a6-b41f-47f4-b14a-eaba64dc4289.png)
## OBSERVATIONS:
A lot of features seems to be correlated with each other but some of them such as Displacement/Cylinder may just indicate a price inflation over the years. As for Length/Width, if the length of the car is increased then the width is also to be increased to maintain the shape of the car and similar is the case with Length/Wheelbase .

Now for the ones which are less obvious we can see that:

-There is a strong negative corelation between doors and cylinders of the car. But I really can't explain what it is.

-There is an interesting corelation between Fuel_Tank_Capacity and Length; Fuel_Tank_Capacity and Kerbs_Weight; Fuel_Tank_Capacity and Displacement, well this makes sense though.

We can also relate Kerbs_Weight with Gross_vehicle_Weight

It is interesting to note that Highway_Milage has negative corelation with Displacement,Fuel_Tank_Capacity and Length.

There is of course a lot more to discover but I can't really explain the rest of the features except the most obvious ones.

We can conclude that, by essence, some of those features may be combined between each other in order to reduce the number of features (like: Fuel_Tank_Capacity,Kerbs_Weight,Length,Displacement) and others indicates that people expect multiples features to be packaged together.

## 2.4)Quantitative to Quantitative relationship-
Let's now examine the quantitative features of our dataframe and how they relate to the Ex-Showroom_Price which is also quantitative (hence the relation Quantitative -> Quantitative)
Now we know that all the elements in df_attr are quantitative elements. And we have already analysed these features.
So lets analyze Displacement and Cylinders with Ex-showroom_Price
![a3](https://user-images.githubusercontent.com/105349293/170816379-dcc40b80-7663-420f-a89a-be79c94a0a4a.png)
From the above graph we can conclude that cylinders have a bigger spread area than displacement. So we can conclude that if more cylinders are there then the cost will be more and cylinders will affect the cost more than displacement.

## 2.5)Categorical to Quantitative relationship-
Since all of the features in df_attr were quantitative elements so now all the remaining elements are categorical data.
Here I have converted Ex-showroom_Price to dtype str so i can analyze it with categorical data
Now here we will begin by creating a new dataset 'dataset_categorical' , which will contain all feature of dtype object.
Here we can only plot a few of them as many of them have missing values and since these are strings we cannot fill them.

- FROM PLOT Ex-showroom_Price VS Fuel_type we can see that fuel price is influencing exshowroom price like models with CNG,Electric fuel type will have less price
- From PLOT POWER VS MODEL we see how price rises when power is increased. Also we see that for a particular model, all its varaint have same power. 

## CONCLUSION-
Till now we saw that the ex-showroom price is strongly corelated with cylinders and displacement. But it is interesting to note that for a particular model say TATA-Nano Genx, its different varaints have same cylinders and displacement(ground clearance). But their price varies on the basis of milage,ARAI_Certified_Mileage_for_CNG, 3_Point_Seat-Belt_in_Middle_Rear_Seat, Ambient_Lightning, Cargo/Boot_Lights, Drive_Modes, High_Speed_Alert_System, Lane_Watch_Camera/_Side_Mirror_Camera, Passenger_Side_Seat-Belt_Reminder, Voice_Recognition, Walk_Away_Auto_Car_Lock, Compression_Ratio, Other_Specs, Other_specs, Android_Auto, Apple_CarPlay, Tyre_Pressure_Monitoring_System, Recommended_Tyre_Pressure, Heated_Seats, Paddle_Shifters, Engine_Type, USB_Ports, Heads-Up_Display, Welcome_Lights, Battery, Electric_Range.

Now these were the features which we removed in the beginning because they had more than 30% missing values.
-So we conclude that when we are comparing same model and different varaints, the price varies on the basis of the above features.
-When we are comparing different models then the price is affected by majorly cylinders and displacment in adition to other features.

As the price of the car increases, so does its features.

# 3) APPLYING REGRESSION MODELS
We can also use our model to predict the ex-showroom price of a car with help of this dataset. So lets apply some machine learning models and compare which model gives better results.

Here I didnt apply linear regression model and polynomial linear regression model because the dataset is complex and we have more that one independent variable.

## IMPORTING DATASET
HERE WE WILL USE 'dataset_num' AS OUR DATASET.
x array will consist of all the independent variables in form of array. So we will drop 'Ex-showroom_Price' from it.
y array will consist of dependent variable , i.e 'Ex-showroom_Price'

## Splitting the dataset into the Training set and Test set
We will divide our dataset into training dataset and test dataset. 
Test set is going to be the new dataset on which we will evaluate our model which means that we will train our data on train set

Since I am using r squared method to check accuracy, I will apply feature scalling only for SUPPORT VECTOR MACHINE MODEL, as for other models it increases the chance of error.

## 3a) MULTIPLE LINEAR REGRESSION
I will use backward elimination method.

BACKWARD ELIMINATION-

STEP 1) Select a significance level to stay in the model (eg SL=0.05)-default

STEP 2) Fit the full model with all possible predictors.

(NOW START ELIMINATING)

STEP 3) Consider the predictor with the highest P-value. If P>SL go to step 4, else go to FIN. (i.e model ie ready)

STEP 4) Remove the predictors.

STEP 5) Fit the model with the remanining predictors.

STEP 6) Repeat Step 3.

REPEAT THIS PROCESS TILL THE HIGHEST P-VALUE IS LESS THAN SL.


I have used sklearn libraries as thy cover these calculations.
After applying this model we see that accuracy score was:0.7045010813859726

## 3b) DECISION TREE REGRESSION
-Once the code is run, the scatterplot will be split up into two segments. So an algorithm will create splits using the data.

-Now how and where the splits are conducted is determined by the algorithm and it actually involves looking at something called the information entropy.

-The algorithm can handle this data and it is finding the optimal splits of our dataset into these leaves and the final leaves are called terminal leaves.

![a3](https://user-images.githubusercontent.com/105349293/170817854-db4dd08b-d4a1-4d07-8c09-ac1ea6e49323.jpeg)

After applying this model we see that accuracy score was:0.8982186246276317

## 3c) RANDOM FOREST REGRESSION
Random Forest regression is a version of ensemble learning.

STEP 1)Pick at random k points from the training set.

STEP 2)Build the decision tree associated to these k data points

STEP 3)Choose the number Ntree of trees you want to build and repeat step 1 and 2.

STEP 4)For a new data is it data point, make each one of your Ntree trees predict the value of Y to further data point in question and assign the new data point the average across all of the predicted  Y values, i.e, finally you use all of the all of this to predict so far and and you make each one of your entries predict the value of Y for the data point in question and assign the new date appoint the average of the predicted Y values.


After applying this model we see that accuracy score was:0.9335385231311853

## FEATURE SCALLING
Since only support vector machine requires feature scalling so I have applied this after these regression models.

Features scaling simply consists of scaling all the variables or features to take value in same scale. We do this to prevent one feature to dominate the others.

Features scaling is a technique used to get the mean and standard deviation of your features in order to perform the scaling.
So if it is applied before the split then it will actually get the mean and standard deviation of all the values including the ones in the test set.Since the test it is supposed  to be new for the model applying it before will be will be like leakage of information on the test set.
So we create a new array Y and convert it into array and split it and then apply feature scalling for SUPPORT VECTOR MACHINE MODEL.

## 3d) SUPPORT VECTOR MACHINE
In this model we have to apply feature  scaling because in SVR model there is not this explicit explicit equation of the dependent variable with respect to features and mostly there are not those coefficient multiplying each of the features and therefore not compensating with lower values for the features taking higher values.
The SVR has an implicit equation of the dependent variable with respect to features so we don't have such coefficient and we will have to apply features scalling.

After applying this model we see that accuracy score was:0.704597806735551
 
## OBSERVATIONS:
So here we see that our random forest regression model gives the best result. So we can conclude that from buisness point of view when we are just looking for higher preformance with less need for interpretation we can use RANDOM FOREST REGRESSION MODEL.


# 4) GROUPING CARS
Lets try to group these cars on the basis of their similar features.

Since it a big dataset, I have used K-Means clustering.

STEP 1)Choose the number k of clusters.

STEP 2)Select a random key points the centroid (not necessarily from the data set)

STEP 3)Assign each data point to the closest centroid- that forms K clusters.

STEP 4)Compute and place the new centroid of each cluster.

STEP 5)Reassign each data point to the new closest centroid.If any reassignment took place go to step four, otherwise go to FIN.

## 4.1) Grouping different models of cars on the basis of luxury features and their ex-showroom price
Now lets first group cars on the basis of their model,ex-showroom price and features like milage,etc which we initially dropped in input 4 because there were less than 30% in number(luxury features) so for this we will use the 'DF' dataset which we had initially created.

So now we have a list of luxury features but we also need to add model and ex-showroom_price.

But since we cant directly add these these features in 'DF' dataset so we will make an array of 'DF' dataset, an array of Ex-showroom_Price and an array of model features and then we will merge these arrays horizontally as they all are of shape(12,76,...)

So I created an * array XX-array of models; shape- (1276,263)

                * array Y-array of exshowrrom prices; shape-(1276,1)
                
                * array xx-array of fluxury features; shape-(1276, 24)
               
                
 The 'xx' array consisted of many strings and some features had different values throughout the datset. So i removed these features as they will not help in clustering of dataset. And i replaced the missing values(nan) with 0 and yes with 1.
 
 Then I merged the above three arrays horizontally as they have 1276 as a common dimension.(two at a time)
 
 VISVAULISATION OF CLUSTERS:
<img width="1095" alt="a4" src="https://user-images.githubusercontent.com/105349293/170819585-425b1b09-1126-41db-bd67-013d21b2c787.png">

## OBSERVATIONS:
So on the basis of above graphs we can conclude that the cars in the given dataset can be grouped into 3 clusters. I guess which can be economical cars, budget luxury cars and luxury cars.

## 4.2) Grouping different models of cars on the basis of thier numerical features
For grouping on the basis of numerical data we will use 'dataset_num' as dataset.
 
VISVAULISATION OF CLUSTERS
<img width="1095" alt="a5" src="https://user-images.githubusercontent.com/105349293/170819656-80727a6c-8aba-4043-9a1e-af9d42eed1ff.png">

## OBSERVATIONS
Also there is no point of applying clustering on numerical data as none of the values will be similar so we cant group data..
And similarly we cannot apply clustering on categorical data as it will contain a lot of different strings so even if we remove those strings , we wont be able to group cars.
