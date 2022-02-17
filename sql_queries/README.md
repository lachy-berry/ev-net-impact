# ev-net-impact/sql_queries/

This folder contains the results of SQL queries used to visualise data for the ev-net-impact project.

Each query corresponds to a Tableau Online visualisation and is described below.

### Query 1
* Retrieves emissions by production source data by year and region. Additional columns added to calculate total and identify countries and continents.
* Visual: treemap showing proportion of world emissions from electricity generation produced by each country or continent.

![image](https://user-images.githubusercontent.com/95948405/153863631-118ef6f7-b759-4c6b-9d24-bb9785d3caaf.png)

### Query 2
* Displays electricity production by source as a percentage of total production by year and country or continent.
* Visual: 100% bar chart colour-coded by electricity source, showing change from 1985 to 2020 for top producing countries/continents.

![image](https://user-images.githubusercontent.com/95948405/153857976-c776f07a-612d-4b6a-bbe6-443447b31e30.png)

### Query 3
* Displays emissions per km of the average electric vehicle in each country based on national grid carbon intensity.
* Visual: world map using colour to indicate CO2e per km in grams.

![image](https://user-images.githubusercontent.com/95948405/153861144-fbd0c549-f9b8-4a78-a217-b9ee0f8c10ac.png)

### Query 4
* Displays emissions per km of the average petrol vehicle in each country based on GFEI fuel efficiency and EIA energy conversion data.
* Visual: bar chart displaying CO2e per km in grams of petrol vehicles in select countries.

![image](https://user-images.githubusercontent.com/95948405/153863062-9403cb11-b560-4c34-b3f9-2dde45fe2b8c.png)

### Query 5
* Calculates the difference in average emissions per km between electric and petrol vehicles in absolute and percentage terms.
* Visual: heatmap + stacked barchart displaying difference in emissions per km in select countries.

![image](https://user-images.githubusercontent.com/95948405/153863433-77174836-e663-413b-8652-0450da5038a7.png)

### Query 6
* Retrieves the average emissions per km for electric and petrol vehicles in different market segments (hatchbacks, sedans, SUVs, vans).
* Visual: stacked bar chart showing CO2e per km for petrol vs electric vehicles within each segment.

![image](https://user-images.githubusercontent.com/95948405/153863272-c34757b2-c70f-4235-bc47-78e285b166fb.png)

### Query 7
* Calculates the annual reduction in emissions of CO2e if all non-electric vehicle sales had, in fact, been electric. Based on vehicle sales data from IEA.
* Visual: treemap showing relative amount of preventable emissions from new vehicle sales in each country.

![image](https://user-images.githubusercontent.com/95948405/153863517-fce452d4-11da-4c49-8058-cfa763736fea.png)

### Query 8
* Retrieves total electricity production, the proportion of production made up by renewable sources, and the emissions per km of the average electric vehicle in select countries.
* Visual: scatterplot demonstrating linear relationship between ev emissions and the carbon intensity of national grids. Dot size represents the scale of domestic production.

![image](https://user-images.githubusercontent.com/95948405/153864166-f168aa45-ef11-4027-aef6-c6c10fe57356.png)
