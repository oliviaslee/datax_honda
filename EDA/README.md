# EDA - Exploratory Data Analysis

Contains the following files
* <b>DBScan and POI Standardization.ipynb</b>
  * DBScan is a density-based clustering algorithm to uncover new insights in optimizing routing. 
  * Unlike conventional clustering algorithms, such as K-Means which require extensively tweaking parameters and tuning, DBScan was an optimal choice.
  * Essentially, by assigning vehicles to clusters of pickup/dropoff locations we can incorporate many-to-one or many-to-many pickup and dropoff delivery possibilities.
  * Distance used, given more time, we would have integrated the actual road distances in our model using a routing api such as Google Maps API.
  * We performed DBScan on people movement but the same code could be applied to the Medical Dataset with a few minor tweaks regarding unstandardized data naming.
  * Additionally, developed code that reliably standardized the output from POI data from Overpass API from OpenStreetMaps. In the future, this data could be plotted on an interactive map, on-demand, and would provide a gateway to new locations in need of deliveries. 
  * Future optimization would include inducing COVID-19 cleaning, driver breaks, and other windows of time when demand is at its low as well as optimizing refueling by incorporating gas station locations in our routing.
* <b>clustering_model.ipynb</b>
  * In efforts to maximize profit, a clustering model was developed to minimize distance traveled by individual vehicles (based on pick-up and drop-off locations).
  * A K-Means clustering was performed on the Medical Dataset, and the best k was chosen via the Elbow Method. Then, the position of the vehicles were plotted using their longitude and latitude locations. A map was also used to visualize where most of the pick-up and drop-off locations were.
  * Temporary vehicle hubs were also chosen relative to the positions of the  vehicle pick-up locations. For future development of this model, implementing known hubs with this algorithm will help assign vehicle pick-ups and drop-offs based on where the nearest hub is located.
  * After careful implementation, we decided that it would be difficult for the K-Means clustering algorithm to take into account other contraints such as time. Thus, we decided to stick with the continuing development of the custom model. 
  * Other possible improvements to this model in the future would be finding a way to include adding the necessary contraints to the K-Means clustering algorithm.

* <b>Honda_API.ipynb</b>
  * Since there were many data tables pulled from the API, we decided to perform correlation analysis to get a better understanding of the data at hand. Correlation matrices were only generated for tables with relevant features, such as trip requests, safety details, information about vehicle make/model (some designed to cater towards handicap features), etc.
  * Each table had a mix of numerical and categorical variables. In order to spot correlations between certain categories, categorical variables (event_type, distracted = True/False, etc.) were one-hot encoded and thus analyzed in this manner.
  * Features with the highest correlations were printed out to help, highlighting the importance of certain features as compared to others.
  * This data analysis also serves to aid the Honda operations manager in understanding certain patterns or trends for rides.

* <b>Honda_visuals.ipynb</b>
* In order to obtain general ideas of data from different tables, we also created visualizations in Python including scatter plots and bar charts.
* The visualizations assist us to better see and understand the trends, outliers, and patterns in data from each table.
