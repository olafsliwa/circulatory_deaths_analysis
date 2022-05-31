# Deaths causes by cardiovascular diseases  - data analysis project

## Main purpose of the analysis
Pace of life is getting faster and faster. We have been observing this phenomenon for the last few years. Our everyday life changes drastically including the way we eat, work, rest and study. Increasing pressure, work in a hurry and bad eating habits lead to serious health problems. One of the results is huge number of deaths caused by cardiovascular diseases every year. Lack of physical activity, easy access to unhealthy, processed food and increasing stress are one of the variables that increase the likelihood of health problems. The main purpose of this analysis is to show how different factors affect the circulatory diseases mortality rate in different European countries. Thanks to the data which is publicly available on the Eurostat website, it is possible to compare number of deaths caused by cardiovascular diseases in different group of people with their BMI, alcohol consumption and eating habits.

## Steps taken
**•	Preparing data – uploading into MS Excel and transformation in PowerQuery**  
First step consist in uploading five tables with data which will be used in further analysis.
Using Power Query, data has been transformed through such actions as:
1. Removing columns that will be useless in the next stages
2. Filtering data. Keeping only information related to the subject of the analysis such us: age group (people from 15 years old), time period (2014 year only), geographic regions (excluding groups of countries such as EU28 which stands from: European Union 28 countries) and paying attention to correctness of the data (eliminating data marked as: break in time series, characterized as low reliability and information achieved in a process which differs from the ones established in the study).
3. Adding custom column ‘age_group’ which allows to classify groups of people from different tables in same method (using same buckets). In some cases, there is a need to use ‘group by’ functionality and sum created age groups, but in others buckets has been already created on the Eurostat website.
4. Process of data transformation looks quite similar in all of the tables. However, bmi, fruits consumption and alcohol consumption datasets requires further taking actions in order to convert columns with numerical values (showing proportion of people with specific attributes) into percentage format.

**•	Creating list of countries, which occur in each data set**  
Next step focus on creating table consisting of distinct country names, which occur in each table and show information for all available groups. In achieving the above result, all datasets were merged on common ‘geo’ column.

**•	Creating ‘bridge’ tables**  
Crucial subject related to the readability of the data visualization is to explain shortcuts which appear in all data tables, but can not be obvious for a person who is not familiar with the information used. It is easily achievable and can be done in two different ways. First method requires creation of a custom column in each data table which explain problematic abbreviations. On the other hand, second solution involves making ‘bridge’ table for each column containing information about distinct properties such as age group, country of origin, gender etc..

**•	Creating table containing information about population and number of deaths**  
Formation of the table that holds data about the number of inhabitants and number of deaths for particular parts of the population will be useful in the further stages of the analysis and visualization. Data was merged based on common columns: age_group, geo, and sex.

**•	Obtaining final version of remaining tables**  
Final versions of a data tables were obtained simply by merging transformed versions of uploaded tables with the ‘bridge’ table containing countries which will be analyzed.

**•	Uploading data into PowerBi**  
The obtained results were uploaded to PowerBi and the additional actions were taken. A calculation column ‘mortality rate’ has been added, which shows proportion of deaths caused by cardiovascular diseases to total number of people in a group, in which number of deaths was noticed. The described calculation is shown below:  
  ```diff
-Mortality Rate = DATA_population_deaths4[number_of_deaths]/DATA_population_deaths4[inhabitants]
```

**•	Data model and final visualization**  
Results of the whole analysis are visible in the photos below. We can see data model created for the purposes of analysis and the final data visualization.
![SCCC](https://user-images.githubusercontent.com/98387772/171108811-9b78ae88-25c7-42ce-9fe0-f77a447396a3.png)
![SC](https://user-images.githubusercontent.com/98387772/171108204-e7f066c2-3461-4979-a62a-822245711162.png)  
![SC2](https://user-images.githubusercontent.com/98387772/171108209-d138005c-46e6-42cc-b538-7def29d348ec.png)  


## Limitations
Data used to create visualization are available as percentages of the specific part of the population only. This form of data presentation without the number of people in each group prevent analysis of the aggregated data. Percentages alone cannot be summed and divided by the number of elements taking into the consideration due to highly possible risk that groups are not equally numerous.
This problem can be solved by creating calculated column in PoweBi as a result of multiplication percentage of people in a cluster and its population taken from the population table. However, the results of such an action may not be 100% valid and are not necessary for the purposes of the analysis.

## Development directions
There is always room for improvements, which allow to find more compelling conclusions. One of them is to apply the instructions about creating calculated column which was mentioned above. In order to achieving deeper analysis, interesting solutions would be to expand analyzed data set with the information on other diseases.

## Data source
Datasets uses in the analysis which has been described above, come from Eurostat, which is one the biggest institution gathering statistical data in the European Union. Information can be found by clicking on the links below:
- Population on 1 January by age and sex (https://ec.europa.eu/eurostat/databrowser/view/DEMO_PJAN/default/table?lang=en&category=demo.demo_pop),
- Cause of death – deaths by country of residence and occurrence (https://ec.europa.eu/eurostat/databrowser/view/HLTH_CD_ARO/default/table?lang=en&category=hlth.hlth_cdeath.hlth_cd_gmor),
- Body mass index (BMI) by sex, age and degree of urbanization (https://ec.europa.eu/eurostat/databrowser/view/HLTH_EHIS_BM1U/default/table?lang=en&category=hlth.hlth_det.hlth_bmi),
- Daily consumption of fruit and vegetables by sex, age and degree of urbanization (https://ec.europa.eu/eurostat/databrowser/view/HLTH_EHIS_FV3U/default/table?lang=en&category=hlth.hlth_det.hlth_cfv),
- Frequency of alcohol consumption by sex, age and degree of urbanization (https://ec.europa.eu/eurostat/databrowser/view/HLTH_EHIS_AL1U/default/table?lang=en&category=hlth.hlth_det.hlth_alc).
