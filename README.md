# Data-X Honda and SHARE Mobility Project
### UC Berkeley Data-X (Industrial Engineering 135: Applied Data Science with Venture Application) Fall 2020 semester project in partnership with Honda's 99P Labs + SHARE Mobility
<br>

## Project Overview

#### Mission
As a team, our drive for creating these notebooks were changing perspectives on traditional MaaS services such as ridesharing. New times call for new changes — we saw where we fit. Our mentors at Honda's 99P Labs and mobility startup, SHARE Mobility, handed an initial problem statement but it grew into something more. Our tools: industry-standard ML techniques and innovating on the go. Our team: diverse thinkers and learners of entreprenurial skills from Fortune 500 advisors to 75-patent-holders and to leading experts in Computer Science. Our drive: making an impact in communities hit hardest by COVID-19, for every car and every essential worker. We are in challenging times now and we hope that our project, however naive and small, helps advance the future of schedule-based fleet optimization and inspire the next generation of students who are looking to build, design and innovate.
 
#### Market Landscape Context
* Due to COVID-19's disruption of the rideshare industry, the demand for delivery and ride-sharing has shifted to accommodate both social distancing and safety protocols. This change does not necessarily mean that the demand for mobility as a service has decreased, but rather that there is a change in the use case at which people seek this type of service.

#### Project Objective
* For this project in collaboration with Honda's 99P Labs and SHARE Mobility, our main problem statement boiled down to the following: <br><br><b>"With this new sense of contactless delivery and social-distancing conscious movement services in mind, how can we optimize vehicle fleet management? With a set of delivery requests for a given day, how can we make sense of the various data points to best match tasks to drivers and vehicles in an organized and optimized manner?" </b><br><br>
* Not only are we addressing current issues and changes in demand, but we're also engineering solutions to adjust to this new perception of mobility as a service.

## Approach
### Data Configuration
The model has two key functions.

<b>Function 1</b>
* <b>Input:</b> The TripRequests table, the Medical Trips table and the number of vehicles. 
* <b>Output:</b> A list that contains a python dictionary where the key is the trip id and the value is the trip object, and the eariest desired pickup time.
  * The trip object has attributes such as TripID, TripType, Number of riders, Pickup Address, Dropoff Address, scheduled timestamp (desired pickup time) etc.

<b>Function 2</b>
* <b>Input:</b> the dictionary returned by the first function, the earliest desired pickup time and the number of vehicles. 
* <b>Output:</b> A Pandas table of matched trip requests to vehicles deployed from their respective hubs.
  * Additional information like Number of Riders, Waiting Time, Distance to Pickup, Desired Pickup Time etc. are also included in the table. 
  * The intended user is the Fleet Operations Manager.

### Model
* We created a custom model for the data APIs provided by [99P Labs](https://developer.99plabs.io/) using Nearest Neighbors (which organically developed its own clusters centered around the deployed vehicles), based on key features like <b>pickup and dropoff locations and distances, trip request time, driver-vehicle feasibility</b>, and more.
* We first started with a simple model by relaxing these restrictions, limiting our training dataset, and developing around the goal of just maximizing the total number of trip requests that can be fulfilled in a given day while minimizing the average distance traveled.
* After we were able to get a minimal model running, we integrated ideal restrictions (as listed above) for a more realistic and optimized fleet management system.
* Different number of vehicles could be entered into the model and the results can be compared using the following.
  * The metrics used to measure the performance of the model are: the average distance to pickup, the drivers’ average waiting for the next nearest pickup, the number of assigned trips and the number of unassigned trips for the model. The ideal situation is to minimize the average distance to pickup, the average waiting time for the next nearest pickup and the number of unassigned trips for the model.
* The model can be used to find the minimum number of vehicles required to complete all the trips for a day (or to complete the highest number of trips for one day the company has had within the past two years).
 
## Files
<b>DBScan and POI Standardization.ipynb</b>
* Implemented DBScan, a density-based clustering algorithm to uncover new insights in optimizing routing. 
* Unlike conventional clustering algorithms such as K-Means which require extensively tweaking parameters and tuning, DBScan was an optimal choice 
* Essentially, by assigning vehicles to clusters of pickup/dropoff locations we go beyond our original algorithm of assuming a one-to-one pickup and dropoff tasks and instead incorporate many-to-one or many-to-many delivery possibilities.     
* Distance used, given more time, we would have integrated the actual road distances in our model using a routing api such as Google Maps API.
* We performed DBScan on people movement but the same code could be applied to the Medical Dataset with a few minor tweaks regarding unstandardized data naming.
* Additionally, developed code that reliably standardized the output from POI data from Overpass API from OpenStreetMaps. In the future, this data could be plotted on an interactive map, on-demand and would provide a gateway to new locations in need of deliveries. 
* Future optimization would include inducing COVID-19 cleaning, driver breaks, and other windows of time when demand is at its low as well as optimizing refueling by incorporating gas stations locations in our routing.
 
 <b>Honda_API.ipynb</b>
* Since there were many data tables pulled from the API, we decided to perform correlation analysis to get a better understanding of the data at hand. Correlation matrices were only generated for tables with relevant features, such as trip requests, safety details, information about vehicle make/model (some designed to cater towards handicap features), etc.
* Each table had a mix of numerical and categorical variables. In order to spot correlations between certain categories, categorical variables (event_type, distracted = True/False, etc.) were one-hot encoded and thus analyzed in this manner.
* Features with the highest correlations were printed out to help, highlighting the importance of certain features as compared to others.
* By providing more insight on individual data tables, future developers of the model may choose to increase the efficiency of the model using this analysis.
* This data analysis also serves to aid the Honda operations manager in understanding certain patterns or trends for rides.


<b>clustering_model.ipynb</b>
* In efforts to maximize profit, a clustering model was developed to minimize distance travelled by individual vehicles (based on pick-up and drop-off locations).
* A K-Means clustering was performed on the Medical Dataset, and the best k was chosen via the Elbow Method. Then, the position of the vehicles were plotted using their longitude and latitude locations. A map was also used to visualize where most of the pick-up and drop-off locations were.
* Temporary vehicle hubs were also chosen relative to the positions of the  vehicle pick-up locations. For future development of this model, implementing known hubs with this algorithm will help assign vehicle pick-ups and drop-offs based on where the nearest hub is located.
* After careful implementation, we decided that it would be difficult for the K-Means clustering algorithm to take into account other contraints such as time. Thus, we decided to stick with the continuing development of the custom model mentioned above. 
* Other possible improvements to this model in the future would be finding a way to include adding the necessary contraints to the K-Means clustering algorithm.

