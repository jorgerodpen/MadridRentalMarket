# Madrid rental market
## Predicting the rent in Madrid 
- Created a model that estimates the cost of the rent (relative error ~15%) to help tenants and owners coming up with a reasonable price.
- Scraped around 10k properties in Madrid using Scrapy. The Spider is in [this repo](https://github.com/jorgerodpen/Fotocasa-Scrapy).
- Engineered features from the extra elements in the description of the property.
- Optimised Linear, Ridge, Lasso and Random Forest Regressors using a grid search.
- Built a user interface using Flask and Heroku that can be seen [here](https://calculadora-alquiler-madrid.herokuapp.com/). 

## Packages
**Python Version**: 3.8.3

**Packages used**: pandas, numpy, statsmodels, scikit-learn, sklearn_dummies, matplotlib, seaborn, flask.

**Flask productionization tutorials**: https://blog.cambridgespark.com/deploying-a-machine-learning-model-to-the-web-725688b851c7 and https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2

**sklearn_dummies**: https://sklearn-dummies.readthedocs.io/en/latest/#

## Web scraping
To see more info go to [Fotocasa-Scrapy](https://github.com/jorgerodpen/Fotocasa-Scrapy)

## Cleaning the data
- Extracted the *District* and the *Borough* from the *Neighborhood* column. 
- Inputed missing values of *Antiquity* by the mode in each borough and then district.
- Inputed missing values in *Rooms* and *Bathrooms* with 1s (considering a minimum of 1 room and 1 bathroom)
- Inputed missing values of *Size* by the mean size in each borough and then district. 
- Inputed missing values of *Furnished* and *Elevator* with 0 
- Extracted extra features from the *Extra* column: 
	- Air conditioner (y/n), Community zone (y/n), Concierge (y/n), Equipped kitchen (y/n), Ensuite (y/n), Terrace (y/n)
- Missing values from *Energy Consumption* were inputed with non-missing values from *Emissions*
- Missing values for floor were inputed using k-neighbors classifier

## Exploratory data analysis
The following choropleth map shows the rent cost's distribution by borough in Madrid: 

<img src="https://github.com/jorgerodpen/MadridRentalMarket/blob/main/boroughs.png" width="400">

Northern boroughs have higher rent cost than southern boroughs. The most common type of property are flats (**Piso** in Spanish), but these are not the most expensive properties, which are attached houses (**Casa adosada** in Spanish), although this type of properties are very rare in Madrid's rental market as shown in the graph bellow: 

<img src="https://github.com/jorgerodpen/MadridRentalMarket/blob/main/type.png" width="400">

Size and number of bathrooms are highly correlated with the final rent cost. Other variables such as the number of rooms and wether the bathroom is ensuite or have also a relatively high correlation. 

<img src="https://github.com/jorgerodpen/MadridRentalMarket/blob/main/correlation.png" width="400">

## Model building
Created a pipeline that first transforms categorical data to dummy variables and then models the data. 

First, a linear regression with al variables was created to see the p-values for each coefficient. Multicollinearity and the effect of the sparse data was observed. 

The data was splitted 20% test set and 80% training set. To measure the model performance two type of errors were used: relative error to see the model performance and mean absolute error for hyper-parameter selection. 

Four models were used:
- Multiple linear regression: It was used as a baseline for the model.
- Ridge regression: Because the multicollinearity between variables. 
- Lasso regression: Because of the sparsity of the data.
- Random forest: Because of the sparsity and the multicollinearity of the data, random forest are well-known because they tend to overfit less. 

## Model performance
- Multiple linear regression: 18-20% error
- Ridge regression: 18-19% error
- Lasso regression: 18-19% error
- Random forest: 15% error

## Productionalization
The app was the deploying using *Flask* to a web server called *Heroku* so that it can be used by owners and tennants to come up with a reasonable price. 

The app can be seen and used here https://calculadora-alquiler-madrid.herokuapp.com/