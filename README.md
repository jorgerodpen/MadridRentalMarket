# Madrid rental market
## Predicting the rent in Madrid 
- Created a model that estimates the cost of the rent (relative error ~14%) to help tenants and owners coming up with a reasonable price.
- Scraped around 10k properties in Madrid using Scrapy. The Spider is in [this repo](https://github.com/jorgerodpen/Fotocasa-Scrapy).
- Engineered features from the extra elements in the description of the property.
- Optimised Linear, Ridge, Lasso and Random Forest Regressors using a grid search.
- Built a user interface using Flask and Heroku that can be seen [here](https://calculadora-alquiler-madrid.herokuapp.com/). 

## Packages
**Python Version**: 3.8.3

**Packages used**: pandas, numpy, statsmodels, scikit-learn, sklearn_dummies, matplotlib, seaborn, flask.

**Flask productionization tutorials**: https://blog.cambridgespark.com/deploying-a-machine-learning-model-to-the-web-725688b851c7 and https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2

## Web scraping
To see more info go to [Fotocasa-Scrapy](https://github.com/jorgerodpen/Fotocasa-Scrapy)