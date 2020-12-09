# Data-X Honda and SHARE Mobility Project
### UC Berkeley Data-X (Industrial Engineering 135: Applied Data Science with Venture Application) Fall 2020 semester project in partnership with Honda's 99P Labs + SHARE Mobility
<br>

## Project Overview
#### Market Landscape Context
* Due to COVID-19's disruption of the rideshare industry, the demand for delivery and ride-sharing has shifted to accommodate both social distancing and safety protocols. This change does not necessarily mean that the demand for mobility as a service has decreased, but rather that there is a change in the use case at which people seek this type of service.

#### Project Objective
* For this project in collaboration with Honda's 99P Labs and SHARE Mobility, our main problem statement boiled down to the following: <br><br><b>"With this new sense of contactless delivery and social-distancing conscious movement services in mind, how can we optimize vehicle fleet management? With a set of delivery requests for a given day, how can we make sense of the various data points to best match tasks to drivers and vehicles in an organized and optimized manner?" </b><br><br>
* Not only are we addressing current issues and changes in demand, but we're also putting in the effort to model our engineering solutions to adjust to this new perception of mobility as a service.

## Approach
<b>Data Configuration</b>
* There are two key functions.
* <b>For the first function, the input is:</b> The TripRequests table, the Medical Trips table and the number of vehicles. 
* <b>The Output is:</b> A python dictionary where the key is the trip id and the value is the corresponding trip object.
  * The trip object has attributes such as TripID, TripType, Number of riders, Pickup Address, Dropoff Address, scheduled timestamp (desired pickup time) etc.
* <b>For the second function, the input is:</b> the dictionary returned by the first function and the number of vehicles. 
* <b>The Output is:</b> A panda table of matched trip requests to vehicles (vehicles used for a given day, deployed from their respective hubs).
  * Additional information like Number of Riders, Waiting Time, Distance to Pickup, Desired Pickup Time, and also included in the table. 
  * The intended user is the Fleet Operations Manager.
  
<b>Model</b>
* We created a custom model for the data APIs provided by [99P Labs](https://developer.99plabs.io/) using Nearest Neighbors (which organically developed its own clusters centered around the deployed vehicles), based on key features like <b>pickup and dropoff locations and distances, trip request time, driver-vehicle feasibility</b>, and more.
* We first started with a simple model by relaxing these restrictions, limiting our training dataset, and developing around the goal of just maximizing the total number of trip requests that can be fulfilled in a given day while minimizing the average distance traveled.
* After we were able to get a minimal model running, we integrated ideal restrictions (as listed above) for a more realistic and optimized fleet management system.
* Different number of vehicles could be entered into the model and the metrics below could be used to compare the result of each entry. 
  * The metrics used to measure the performance of the model are: the average distance to pickup, the drivers’ average waiting for the next nearest pickup, the number of assigned trips and the number of unassigned trips for the model. The ideal situation is to minimize the average distance to pickup, the average waiting time for the next nearest pickup and the number of unassigned trips for the model.
* The model can be used to find the minimum number of vehilces required to complete all the trips for a day (or to complete the highest number of trips for one day the company has within the past two years).
 
## Files
<b>DBScan and POI Standardization.ipynb</b>
* <insert information here>
 
 <b>Honda_API.ipynb</b>
* Since there were many data tables pulled from the API, we decided to perform correlation analysis to get a better understanding of the data at hand. Correlation matrices were only generated for tables with relevant features, such as trip requests, safety details, information about vehicle make/model (some designed to cater towards handicap features), etc.
* Each table had a mix of numerical and categorical variables. In order to spot correlations between certain categories, categorical variables (event_type, distracted = True/False) were one-hot encoded and thus analyzed in this manner.

<b>clustering_model.ipynb</b>
* In efforts to maximize profit, a clustering model was developed to minimize distance travelled by individual vehicles. 
* A K-Means clustering was performed on the Medical Dataset, and the best k was chosen via the Elbow Method. Then, the position of the vehicles were plotted using their longitude and latitude locations. A map was also used to visualize where most of the pick-up and drop-off locations were.
* After careful implementation, we decided that it would be difficult for the K-Means clustering algorithm to take into account other contraints such as time. Thus, we decided to stick with the continuing development of the custom model mentioned above.
