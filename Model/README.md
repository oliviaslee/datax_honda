# Model
* We created a custom model for the data APIs provided by [99P Labs](https://developer.99plabs.io/) using Nearest Neighbors (which organically developed its own clusters centered around the deployed vehicles), based on key features like <b>pickup and dropoff locations and distances, trip request time, driver-vehicle feasibility</b>, and more.
* We first started with a simple model by relaxing these restrictions, limiting our training dataset, and developing around the goal of just maximizing the total number of trip requests that can be fulfilled in a given day while minimizing the average distance traveled.
* After we were able to get a minimal model running, we integrated ideal restrictions (as listed above) for a more realistic and optimized fleet management system.
* Different number of vehicles could be entered into the model and the results can be compared using the following.
  * The metrics used to measure the performance of the model are: the average distance to pickup, the drivers’ average waiting for the next nearest pickup, the number of assigned trips and the number of unassigned trips for the model. The ideal situation is to minimize the average distance to pickup, the average waiting time for the next nearest pickup and the number of unassigned trips for the model.
* The model can be used to find the minimum number of vehicles required to complete all the trips for a day (or to complete the highest number of trips for one day the company has had within the past two years).

### Contains the following files:
* Model files
  * Micro-transit query.ipynb
  * Public Simple Model.ipynb
* Data files can be found in [this google drive]()
  * Due to the sensitive and internal nature of the data set, we've stored the data files within a Berkeley google drive where a berkeley.edu email is needed to access the files. For additional information, please contact any of the project members or mentors.
