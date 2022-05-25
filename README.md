# corona-analysis

ARIMA forecasting and dashboarding with publicly available corona data. Includes Kubernetes deployment scripts for the trained model, REST API and dashboard.

## Environment
Assuming `conda` is available in your shell you can run the following from the root of this repository to create and activate an anaconda environment called `corona-analysis`, and to run the `jupyter notebook` server:
```sh
conda create --file environment.yml
conda activate corona-analysis
jupyter notebook
```

## Data Sources
* [COVID-19 Data Repository by the Center for Systems Science and Engineering (CSSE) at Johns Hopkins University](https://github.com/CSSEGISandData/COVID-19#covid-19-data-repository-by-the-center-for-systems-science-and-engineering-csse-at-johns-hopkins-university)
* [RKI Corona Bundesländer](https://npgeo-corona-npgeo-de.hub.arcgis.com/datasets/ef4b445a53c1406892257fe63129a8ea_0/data)
* "Frozen" datasets from JHU have been added to this repo as well to get started quickly

## Deployment
```sh
cd deployment/docker-images/dashboard
docker build -t devdojo/corona-dashboard .

cd deployment/docker-images/model
docker build -t devdojo/corona-model .

cd deployment
kubectl apply -f dashboard.yaml
```

## Key Take-Aways
* Working with different (freely available) data sources to get insights
* Use different ways to perform exploratory data analysis
  * Pandas styles to highlight certain aspects in data frames
  * Jupyter widgets to add interactive elements for e.g., data selection
  * Ploty to create interactive charts
  * Folium to create interactive maps
  * Voilá for easy dashboarding
  * Using the jupyter "scratchpad" extension to try code snippets in a new cell without convoluting the global namespace
* Deployment of dashboards in Kubernetes
  * Decouple model and dashboard with deployments and services
  * Create a REST API in front of a model with fastAPI
  * Use Voilá to deploy a jupyter notebook as dashboard
* Explore and understand stationarity which is an important aspect when working with timeseries
