# Carbon-Emisson-Analysis
## Upload data

### First 10 row of Table 'product_emissions'
| id            | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf                       | operations_percent_total_pcf                     | downstream_percent_total_pcf                     | 
| ------------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -----------------------------------------------: | -----------------------------------------------: | -----------------------------------------------: | 
| 10056-1-2014  | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                                            | 30.00                                            | 12.50                                            | 
| 10056-1-2015  | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                                            | 30.00                                            | 12.50                                            | 
| 10222-1-2013  | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                                            | 17.36                                            | 2.01                                             | 
| 10261-1-2017  | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                                            | 5.51                                             | 63.84                                            | 
| 10261-2-2017  | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                                            | 4.51                                             | 70.41                                            | 
| 10261-3-2017  | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 2274                 | 20.05                                            | 3.61                                             | 76.34                                            | 
| 10324-1-2016  | 15         | 16         | 19                | 2016 | KURALON  fiber                                                  | 1500      | 10000                | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 10418-1-2013  | 84         | 9          | 19                | 2013 | Portland Cement                                                 | 1000      | 1102                 | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 10661-10-2014 | 85         | 28         | 11                | 2014 | Regular Straight 505® Jeans – Steel (Water                      | 0.7665    | 15                   | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 10661-10-2015 | 85         | 28         | 6                 | 2015 | Regular Straight 505® Jeans – Steel (Water                      | 0.7665    | 15                   | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 

### First 10 row of Table 'industry_groups'
| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 
| 4  | "Mining - Iron, Aluminum, Other Metals"                                | 
| 5  | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 
| 6  | "Textiles, Apparel, Footwear and Luxury Goods"                         | 
| 7  | Automobiles & Components                                               | 
| 8  | Capital Goods                                                          | 
| 9  | Chemicals                                                              | 
| 10 | Commercial & Professional Services                                     | 

### First 10 row of Table 'companies'
| id | company_name                                   | 
| -: | ---------------------------------------------: | 
| 1  | "Autodesk, Inc."                               | 
| 2  | "Casio Computer Co., Ltd."                     | 
| 3  | "Cisco Systems, Inc."                          | 
| 4  | "CNX Coal Resources, LP"                       | 
| 5  | "Coca-Cola Enterprises, Inc."                  | 
| 6  | "Compañía Española de Petróleos, S.A.U. CEPSA" | 
| 7  | "Daikin Industries, Ltd."                      | 
| 8  | "Elitegroup computer systems co., Ltd."        | 
| 9  | "Fuji Xerox Co., Ltd."                         | 
| 10 | "Gamesa Corporación Tecnológica, S.A."         | 

### First 10 row of Table 'countries'
| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 
| 4  | Canada       | 
| 5  | Chile        | 
| 6  | China        | 
| 7  | Colombia     | 
| 8  | Finland      | 
| 9  | France       | 
| 10 | Germany      | 

### Research 
#### Problem 1: Which products contribute the most to carbon emissions?
##### SQL query
```
Select product_name  
From product_emissions
Order by carbon_footprint_pcf desc
Limit 10
```                                                                                       | 
##### Result 
| product_name                                                                                                                       | 
| ---------------------------------------------------------------------------------------------------------------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 
| Wind Turbine G132 5 Megawats                                                                                                       | 
| Wind Turbine G114 2 Megawats                                                                                                       | 
| Wind Turbine G90 2 Megawats                                                                                                        | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 
| TCDE                                                                                                                               | 
| TCDE                                                                                                                               | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 
| Electric Motor                 

#### Prblem 2: What are the industry groups of these products?
##### SQL query
```
Select 
	pe.product_name, 
	ig.industry_group
From 
	product_emissions pe
Join 
	industry_groups ig on pe.industry_group_id = ig.id  
Order by 
	carbon_footprint_pcf  desc
Limit 10
```
##### Result 
| product_name                                                                                                                       | industry_group                     | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G132 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G114 2 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G90 2 Megawats                                                                                                        | Electrical Equipment and Machinery | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | Automobiles & Components           | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | Materials                          | 
| TCDE                                                                                                                               | Materials                          | 
| TCDE                                                                                                                               | Materials                          | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | Automobiles & Components           | 
| Electric Motor                                                                                                                     | Capital Goods                      | 


#### Prblem 3: What are the industries with the highest contribution to carbon emissions ?
##### SQL query
```
Select Distinct 
	pe.industry_group_id,
	ig.industry_group,
	sum(pe.carbon_footprint_pcf) as 'total carbon emissions'
From 
	product_emissions pe
Join 
	industry_groups ig on pe.industry_group_id = ig.id
Group by 
	pe.industry_group_id
Order by 
	sum(pe.carbon_footprint_pcf) desc 
Limit 10
```
##### Result 
| industry_group_id | industry_group                                   | total carbon emissions | 
| ----------------: | -----------------------------------------------: | ---------------------: | 
| 13                | Electrical Equipment and Machinery               | 9801558                | 
| 7                 | Automobiles & Components                         | 2582264                | 
| 19                | Materials                                        | 577595                 | 
| 25                | Technology Hardware & Equipment                  | 363776                 | 
| 8                 | Capital Goods                                    | 258712                 | 
| 2                 | "Food, Beverage & Tobacco"                       | 111131                 | 
| 5                 | "Pharmaceuticals, Biotechnology & Life Sciences" | 72486                  | 
| 9                 | Chemicals                                        | 62369                  | 
| 24                | Software & Services                              | 46544                  | 
| 20                | Media                                            | 23017                  | 

#### Prblem 4: What are the company with the highest contribution to carbon emissions ?
##### SQL query
```
Select Distinct 
	pe.company_id,
	cp.company_name,
	sum(pe.carbon_footprint_pcf) as 'total carbon emissions'
From 
	product_emissions pe
Join 
	companies cp on pe.company_id = cp.id
Group by 
	pe.company_id
Order by 
	sum(pe.carbon_footprint_pcf) desc 
Limit 10
```
##### Result 
| company_id | company_name                            | total carbon emissions | 
| ---------: | --------------------------------------: | ---------------------: | 
| 10         | "Gamesa Corporación Tecnológica, S.A."  | 9778464                | 
| 61         | Daimler AG                              | 1594300                | 
| 139        | Volkswagen AG                           | 655960                 | 
| 17         | "Mitsubishi Gas Chemical Company, Inc." | 212016                 | 
| 11         | "Hino Motors, Ltd."                     | 191687                 | 
| 34         | Arcelor Mittal                          | 167007                 | 
| 141        | Weg S/A                                 | 160655                 | 
| 71         | General Motors Company                  | 137007                 | 
| 16         | "Lexmark International, Inc."           | 132012                 | 
| 7          | "Daikin Industries, Ltd."               | 105600                 | 

#### Prblem 5: What are the countries with the highest contribution to carbon emissions?
##### SQL query
```
Select Distinct 
	pe.country_id,
	co.country_name,
	sum(pe.carbon_footprint_pcf) as 'total carbon emissions'
From 
	product_emissions pe
Join 
	countries co on pe.country_id = co.id
Group by 
	pe.country_id
Order by 
	sum(pe.carbon_footprint_pcf) desc 
Limit 10
```
##### Result
| country_id | country_name | total carbon emissions | 
| ---------: | -----------: | ---------------------: | 
| 23         | Spain        | 9786130                | 
| 10         | Germany      | 2251225                | 
| 16         | Japan        | 653237                 | 
| 28         | USA          | 518381                 | 
| 22         | South Korea  | 186965                 | 
| 3          | Brazil       | 169337                 | 
| 18         | Luxembourg   | 167007                 | 
| 20         | Netherlands  | 70417                  | 
| 26         | Taiwan       | 62875                  | 
| 12         | India        | 24574                  | 

#### Prblem 6: What is the trend of carbon footprints (PCFs) over the years?
