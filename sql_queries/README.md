### ev-net-impact/sql_queries

This folder contains the results of SQL queries used to visualise data for the ev-net-impact project.

Each query corresponds to a Tableau Online visualisation and is described below.

Note: some queries are based on pre-generated views. See the project code for the full script used.

### Query 1
`SELECT t1.region, geo_type, year, total_emissions
FROM total_emissions t1
INNER JOIN geo_types t2 ON t1.region = t2.region
WHERE geo_type != 'Other';`

* Retrieves emissions by production source data by year and region. Additional columns added to calculate total and identify countries and continents.
* Visual: treemap showing proportion of world emissions from electricity generation produced by each country or continent.

![image](https://user-images.githubusercontent.com/95948405/153863631-118ef6f7-b759-4c6b-9d24-bb9785d3caaf.png)

### Query 2
`SELECT t1.region, geo_type, t1.year,
    coal_twh / total_twh AS coal_pct,
    gas_twh / total_twh AS gasl_pct,
    nuclear_twh / total_twh AS nuclear_pct,
    hydro_twh / total_twh AS hydro_pct,
    other_renewables_twh / total_twh AS other_renewables_pct,
    solar_twh / total_twh AS solar_pct,
    oil_twh / total_twh AS oil_pct,
    wind_twh / total_twh AS wind_pct,
    (nuclear_twh + hydro_twh + other_renewables_twh + solar_twh + wind_twh) / total_twh AS renewables_pct   
FROM electricity_production t1
INNER JOIN geo_types t2 ON t1.region = t2.region
INNER JOIN total_twh t3 ON t1.region = t3.region AND t1.year = t3.year
WHERE geo_type != 'Other';`

* Displays electricity production by source as a percentage of total production by year and country or continent.
* Visual: 100% bar chart colour-coded by electricity source, showing change from 1985 to 2020 for top producing countries/continents.

![image](https://user-images.githubusercontent.com/95948405/153857976-c776f07a-612d-4b6a-bbe6-443447b31e30.png)

### Query 3
`SELECT region, year, CO2e_grams_per_km_electric
FROM ev_co2_per_km;`

* Displays emissions per km of the average electric vehicle in each country based on national grid carbon intensity.
* Visual: world map using colour to indicate CO2e per km in grams.

![image](https://user-images.githubusercontent.com/95948405/153861144-fbd0c549-f9b8-4a78-a217-b9ee0f8c10ac.png)

### Query 4
`SELECT region, year, CO2e_grams_per_km_petrol
FROM petrol_co2_per_km;`

* Displays emissions per km of the average petrol vehicle in each country based on GFEI fuel efficiency and EIA energy conversion data.
* Visual: bar chart displaying CO2e per km in grams of petrol vehicles in select countries.

![image](https://user-images.githubusercontent.com/95948405/153863062-9403cb11-b560-4c34-b3f9-2dde45fe2b8c.png)

### Query 5
`SELECT t1.region, t1.year, CO2e_grams_per_km_electric, CO2e_grams_per_km_petrol,
    (CO2e_grams_per_km_petrol - CO2e_grams_per_km_electric) AS absolute_diff,
    ((CO2e_grams_per_km_electric / CO2e_grams_per_km_petrol) - 1) AS percentage_diff
FROM ev_co2_per_km t1
INNER JOIN petrol_co2_per_km t2 ON t1.region = t2.region AND t1.year = t2.year;`

* Calculates the difference in average emissions per km between electric and petrol vehicles in absolute and percentage terms.
* Visual: heatmap + stacked barchart displaying difference in emissions per km in select countries.

![image](https://user-images.githubusercontent.com/95948405/153863433-77174836-e663-413b-8652-0450da5038a7.png)

### Query 6
`SELECT t1.segment, 
    AVG(lge_per_100km * (SELECT factor FROM emissions_factors WHERE source = 'petrol') / 100) AS CO2e_grams_per_km_petrol,
    AVG(wh_per_km * total_emissions / total_twh / 1000) AS CO2e_grams_per_km_electric
FROM ev_efficiency t1
INNER JOIN vehicle_segments t2 ON t1.segment = t2.segment
INNER JOIN fuel_economy t3 ON t2.product = t3.product
INNER JOIN total_emissions t4 ON t3.year = t4.year AND t3.region = t4.region
INNER JOIN total_twh t5 ON t4.year = t5.year AND t4.region = t5.region
WHERE t3.year = 2019 AND t1.segment IN ('spv', 'sedan', 'hatchback', 'suv')
GROUP BY t1.segment;`

* Retrieves the average emissions per km for electric and petrol vehicles in different market segments (hatchbacks, sedans, SUVs, vans).
* Visual: stacked bar chart showing CO2e per km for petrol vs electric vehicles within each segment.

![image](https://user-images.githubusercontent.com/95948405/153863272-c34757b2-c70f-4235-bc47-78e285b166fb.png)

### Query 7
`SELECT t1.region, t1.year,
    (total_sales - ev_sales)
    * (CO2e_grams_per_km_petrol - CO2e_grams_per_km_electric)
    / 1000000 AS CO2_tonnes_saved_per_km
FROM annual_vehicle_sales t1
INNER JOIN annual_ev_sales t2 ON t1.year = t2.year AND t1.region = t2.region
INNER JOIN petrol_co2_per_km t3 ON t1.year = t3.year AND t1.region = t3.region
INNER JOIN ev_co2_per_km t4 ON t1.year = t4.year AND t1.region = t4.region
WHERE t1.year = 2019
ORDER BY 3 desc;`

* Calculates the annual reduction in emissions of CO2e if all non-electric vehicle sales had, in fact, been electric. Based on vehicle sales data from IEA.
* Visual: treemap showing relative amount of preventable emissions from new vehicle sales in each country.

![image](https://user-images.githubusercontent.com/95948405/153863517-fce452d4-11da-4c49-8058-cfa763736fea.png)

### Query 8
`SELECT t1.region, t1.year,
    (nuclear_twh + hydro_twh + other_renewables_twh + solar_twh + wind_twh) / total_twh AS renewables_pct,
    total_twh,
    CO2e_grams_per_km_electric
FROM electricity_production t1
INNER JOIN geo_types t2 ON t1.region = t2.region
INNER JOIN total_twh t3 ON t1.region = t3.region AND t1.year = t3.year
INNER JOIN ev_co2_per_km t4 ON t1.region = t4.region AND t1.year = t4.year
WHERE t2.geo_type != 'Other';`

* Retrieves total electricity production, the proportion of production made up by renewable sources, and the emissions per km of the average electric vehicle in select countries.
* Visual: scatterplot demonstrating linear relationship between ev emissions and the carbon intensity of national grids. Dot size represents the scale of domestic production.

![image](https://user-images.githubusercontent.com/95948405/153864166-f168aa45-ef11-4027-aef6-c6c10fe57356.png)
