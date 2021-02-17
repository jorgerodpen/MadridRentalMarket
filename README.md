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