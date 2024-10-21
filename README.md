# Final-Project-Statistical-Modelling-with-Python

<img width="287" alt="bike_guy" src="https://github.com/user-attachments/assets/2ecc54ea-ce2a-41c2-8878-527e972960cc">

## Project/Goals

The CityBikes api was accessed to find the location of city bike stations in Vancouver, BC. The Yelp and Foursquare apis were then accessed to find all cafes within a 1000m radius of the city bike stations. This project was created to use the returned data and determine if there is a relationship between the number of bikes currently in use (empty spots) and the number of cafes within a 1000m radius. 

## Process
### Gathering data

The [CityBikes](https://citybik.es/), [Foursquare](https://developer.foursquare.com/places). and [Yelp](https://docs.developer.yelp.com/docs/fusion-intro) apis were used to gather data. From CityBikes, I pulled the location of all available bike stations in Vancouver, BC. This data included the latitude and longitude of the location, the number of available bikes, and the empty bike spaces. Yelp and Foursquare were then used to make multiple api calls to find cafes in Vancouver based on the latitude and longitude of each bike station. This returned a wide variety of information for each cafe; however, for this project the number of cafes, average cafe rating, and number of reviews were used.

Each api call provided a response in JSON format. These responses were then parsed in dataframes using pandas. Once in the dataframes, EDA was performed do keep only data that was deemed relevant for the project. The quality of each dataset was reviewed and it was ultimately determined that the Yelp and Citybikes data would be used moving forward as Yelp returned the most relevant information (some EDA shown in the yelp_foursquare_eda notebook).

### Building the model

The yelp and CityBikes dataframes were joined using the city bikes' station ID. This allowed me to group the data by bike station and return the relevant number of cafes within 1000m of the bike station. At this point the data was saved as model_data to be used in a regression model.

This model was created to test if there is a relationship between the number of bikes at a bike station, and the number of cafes within 1000m of that station. Below is a pair plot of the variables used in the model:

![pairplot](https://github.com/user-attachments/assets/d384fcf4-46e1-4a16-abf8-afd70ca4f067)

A linear regression model was set up using the total number of bikes at a station as the independent variable, and the number of cafes within a 1000m radius as the dependent variable. This returned very poor results (R-squared: 0.05, p-value: 0.275) so the model was run two more times using the empty slots, and available bikes as the dependants.

## Results

<img width="728" alt="empty_slots_results" src="https://github.com/user-attachments/assets/39e454e7-dbc7-47c1-bb61-93761470e92c">

Empty slots ended up being the 'best of the worst' for this model. However, with an R-squared value of 0.024 and a p-value of 0.013, we can still not reject the null hypothesesis of this model. At this time, with the fairly limited data used, the empty slots of a city bikes station is not a good predictor of the number of cafes in an area. Logically this makes sense, as there are many more important factors to a potential cafe owner than the available bikes for rent nearby.

## Challenges 
As this was my first time using python to call an api, the formatting of the calls was a bit tricky to set up. After spending time reviewing the relevant documentation, things became a bit more clear. This process really opened my eyes to the importance of good documentation.

Once the JSON responses were received, I had a bit of a difficult time parsing the data into a pandas dataframe. The data was quite nested which proved to be a bit of a challenge. Once I was able to understand the keys contained in each response, the flow into creating a dataframe made more sense and I was able to more easily repeat this process with subsequent api calls. 

## Future Goals

I would like to repeat this project using a different data set for the dependant variables. Accessing some more relevant data such as population density or household income will be my next avenue of research. I believe this data will be a better predictor of the cafes in an area. Also, I would like to include the average rating of the cafes to see if their is any relationship better income and the 'quality' of cafes in an area.
