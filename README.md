# Data-X Honda and SHARE Mobility Project
### UC Berkeley Data-X (Industrial Engineering 135: Applied Data Science with Venture Application) Fall 2020 semester project in partnership with Honda's 99P Labs + SHARE Mobility
<br>

## Project Overview

#### Mission
To make an impact in communities hit hardest by COVID-19, for every car and every essential worker. We hope that our project helps advance the future of schedule-based fleet optimization.
 
#### Market Landscape
* Due to COVID-19's disruption of the rideshare industry, the demand for delivery and ride-sharing has shifted to accommodate both social distancing and safety protocols. This change does not necessarily mean that the demand for mobility as a service has decreased, but rather that there is a change in the use case at which people seek this service.

#### Project Objective
* For this project in collaboration with Honda's 99P Labs and SHARE Mobility, our main problem statement boiled down to the following: <br><br><b>"With this new sense of contactless delivery and social-distancing conscious movement services in mind, how can we optimize vehicle fleet management? With a set of delivery requests for a given day, how can we make sense of the various data points to best match tasks to drivers and vehicles in an organized and optimized manner?" </b><br><br>
* Not only are we addressing current issues and changes in demand, but we're also engineering solutions to adjust to this new perception of mobility as a service.

## Approach
### Data Configuration
The model has three key functions.

<b>Function 1</b>
* <b>Input:</b> The TripRequests table, the Medical Trips table and the number of vehicles. 
* <b>Output:</b> A list that contains a python dictionary where the key is the trip id and the value is the trip object, and the eariest desired pickup time.
  * The trip object has attributes such as TripID, TripType, Number of riders, Pickup Address, Dropoff Address, scheduled timestamp (desired pickup time) etc.

<b>Function 2 and 3</b>
* <b>Input:</b> the dictionary returned by the first function, the earliest desired pickup time (for function 3) and the number of vehicles. 
* <b>Output:</b> A Pandas table of matched trip requests to vehicles deployed from their respective hubs.
  * Additional information like Number of Riders, Waiting Time, Distance to Pickup, Desired Pickup Time etc. are also included in the table. 
  * The intended user is the Fleet Operations Manager.

### Model
* We created a custom model for the data APIs provided by [99P Labs](https://developer.99plabs.io/) using Nearest Neighbors (which organically developed its own clusters centered around the deployed vehicles), based on key features like <b>pickup and dropoff locations and distances, trip request time, driver-vehicle feasibility</b>, and more.
* The model (as detailed by the the two main functions listed in 'Data Configuration') can be used to find the minimum number of vehicles required to complete all the trips for a day (or to complete the highest number of trips for one day the company has had within the past two years).
 
## Files
<b>DBScan and POI Standardization.ipynb</b>
* DBScan is a density-based clustering algorithm to uncover new insights in optimizing routing. 
* Unlike conventional clustering algorithms, such as K-Means which require extensively tweaking parameters and tuning, DBScan was an optimal choice.
* Essentially, by assigning vehicles to clusters of pickup/dropoff locations we can incorporate many-to-one or many-to-many pickup and dropoff delivery possibilities.

<b>clustering_model.ipynb</b>
* In efforts to maximize profit, a clustering model was developed to minimize distance traveled by individual vehicles (based on pick-up and drop-off locations).
* A K-Means clustering was performed on the Medical Dataset, and the best k was chosen via the Elbow Method. Then, the position of the vehicles were plotted using their longitude and latitude locations. A map was also used to visualize where most of the pick-up and drop-off locations were.

 <b>Honda_API.ipynb</b>
* Since there were many data tables pulled from the API, we decided to perform correlation analysis to get a better understanding of the data at hand. Correlation matrices were only generated for tables with relevant features, such as trip requests, safety details, information about vehicle make/model (some designed to cater towards handicap features), etc.
* Each table had a mix of numerical and categorical variables. In order to spot correlations between certain categories, categorical variables (event_type, distracted = True/False, etc.) were one-hot encoded and thus analyzed in this manner.
