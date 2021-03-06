# ev-net-impact
Data collection, engineering and visualisation project using MySQL, Pandas, and Tableau Online

**Tableau Online Viz:**
[The real climate impact of electric vehicles](https://public.tableau.com/app/profile/lachy.berry/viz/Therealclimateimpactofelectricvehicles/EV_impact)

## About this project
The adoption of electric vehicles is touted as a key stepping stone in the global transition to net zero. While true, the carbon efficiency of EVs will always be tied to electricity production. Reliance on fossil fuels for electricity simply shifts emissions from petrol pumps to charging stations and from exhaust pipes to power plants.

The aim of this project is to identify how much impact electric vehicles actually have on carbon emissions around the world. Are they that much cleaner than petrol-powered alternatives?

Answering this question will require understanding how each country generates electricity, how much power electric vehicles need to run, and how much fuel conventional vehicles guzzle.

## Repository structure
`data` stores all datasets used in this project. The `source` subfolder contains all data downloaded, replicated and scraped from online sources without alteration. `tables` contains SQL tables created as part of the data schema for this project from cleansed source data. `views` contains the views (virtual tables) generated from schema tables to simplify querying later on.

`sql_queries` contains the results corresponding to the MySQL queries used for this project. Results are uploaded to Tableau Online and used to create visualisations in the final dashboard.

`notebooks` contains the Jupyter notebooks written in the course of this project.
