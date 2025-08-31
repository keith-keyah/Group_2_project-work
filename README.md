# group2_project

# ANALYSIS OF CROP YIELD IN KARAMOJA REGION

<img width="1100" height="953" alt="image" src="https://github.com/user-attachments/assets/b8220496-2988-4d13-9903-21416461c147" />


# Business Understanding

An NGO seeks to provide technical support as well as farm inputs to the farmers experiencing extremely low yield in the Karamoja region of Uganda.

# Problem Statement

The NGO lacks visibility into the overall state of the region and often needs to rely on some very local sources of information to prioritize their activities. Dalberg Data Insights (DDI) has been requested to develop a new food security monitoring tool to support the decision making of the NGO

# Objectives

- Identify regions with lowest total yield
- Identify regions with lowest sorghum yield per HA
- Identify regions with lowest maize yield per HA
- Correlation between population size and yield
- Correlation between crop area and yield

# Success Criteria

Understanding the areas that have the lowest yields in order for the NGO to prioritize in terms of resource distribution.

# Data Understanding

*First we import the necessary libraries then we load the datasets*

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```
```python
district_crop_yield = pd.read_csv('/content/Uganda_Karamoja_District_Crop_Yield_Population.csv')
district_crop_yield.head()
```
```python
subcounty_crop_yield = pd.read_csv('/content/Uganda_Karamoja_Subcounty_Crop_Yield_Population.csv')
subcounty_crop_yield.head()
```

#

*We then check the structure of the datasets and summary of descriptive statistics*

#

- We go forward to Show correlation of the `numerical columns` only and presenting it in a `heat map`

```python
district_crop_yield.select_dtypes(include='number').corr()

sns.heatmap(district_crop_yield.select_dtypes(include='number').corr(), annot=True)
plt.rcParams['figure.figsize']=(20,10)
plt.show()
```
*Correlation Heatmap at district level*
<img width="589" height="594" alt="image" src="https://github.com/user-attachments/assets/96b66a4f-9669-471b-bca4-076bd2b593ab" />

#

*Correlation Heatmap at subcounty level*
<img width="1526" height="819" alt="image" src="https://github.com/user-attachments/assets/cfcaba15-5221-4d2a-8737-7ebdf5442e22" />

# DATA CLEANING

- We check for null or missing values in the datasets

```python
district_crop_yield.isna().sum()
```
```python
subcounty_crop_yield.isna().sum()
```

*`NO` null values found in both datasets*

#

- creating new fields to show total production per district and sub-county

```python
district_crop_yield['Total_Yield'] = district_crop_yield['M_Prod_Tot'] + district_crop_yield['S_Prod_Tot']
district_crop_yield.head()
```
*The same can be done for the subcounty level*

#

- Next we remove all duplicates in both datasets if any

```python
district_crop_yield.shape
```
```python
district_yield_cleaned = district_crop_yield.drop_duplicates()
district_yield_cleaned.shape
```
*The same is done for the subcouty level*

The datasets do not have duplicated values

## EDA- Exploratory Data Analysis

- Checking for regions with `lowest yield` at district level and using a bar graph to visualize

```python
district_yield_cleaned = district_yield_cleaned.sort_values(by='Total_Yield')
print(district_yield_cleaned.head(4)['NAME'])
```

<img width="1644" height="877" alt="image" src="https://github.com/user-attachments/assets/664becd2-e748-419c-bc95-1a1c69255eb8" />

#

- We used a bar graph to visualize subcounty's yield from the least to highest

<img width="1666" height="1024" alt="image" src="https://github.com/user-attachments/assets/26c2f59e-eca5-4ea0-9453-ea54d5c4e3b3" />

#

- Finding the sorghurm yield in district and subcounty level using a bar graph

*sorghurm yield per HA Districtwise*
<img width="1639" height="877" alt="image" src="https://github.com/user-attachments/assets/ff93db15-b6f5-4fd7-a691-e0307693dd81" />

#

*Sorghurm yield per HA Subcountywise*
<img width="1639" height="1024" alt="image" src="https://github.com/user-attachments/assets/c7602da1-440c-4d11-8f49-61431a52ba2b" />

- Finding the `Maize yield` in district and subcounty level and visualizing it using a bar graph

<img width="1648" height="877" alt="image" src="https://github.com/user-attachments/assets/8b2176b8-9119-46f9-8695-de8412d8bb1e" />

#
<img width="1666" height="1024" alt="image" src="https://github.com/user-attachments/assets/de5a5831-f128-465d-ba43-91d74256f9d8" />

#

- Finding the `correlation` between `population` and `total production` by using a scatter plot

<img width="1644" height="877" alt="image" src="https://github.com/user-attachments/assets/398a86f9-94dc-477e-9304-7d9e53e0943c" />

#

<img width="1622" height="910" alt="image" src="https://github.com/user-attachments/assets/512bed95-f8ad-4051-8286-01197781cc9b" />

#

- Finding `Correlation` between `crop area` and `total production` using a scatter plot

<img width="1644" height="877" alt="image" src="https://github.com/user-attachments/assets/98b68f98-5329-46e4-8819-5641386d0662" />
#

<img width="1622" height="904" alt="image" src="https://github.com/user-attachments/assets/e6ab0c3a-85a0-4596-b457-452a84d2b236" />

# Key Findings

`4 Districts with lowest total yield:`

- MOROTO
- ABIM
- AMUDAT
- NAPAK

`10 Sub-Counties with lowest total yield:`

- SOUTHERN DIVISION
- NORTHERN DIVISION
- AMUDAT TOWN COUNCIL
- NAKAPIRIPIRIT TOWN COUNCIL
- KAABONG TOWN COUNCIL
- KATIKEKILE
- LODIKO
- KAABONG EAST
- NGOLERIET
- TAPAC

`4 Districts with lowest sorghum yield per HA:`

- MOROTO
- NAPAK
- AMUDAT
- KAABONG

`10 Sub-Counties with lowest sorghum yield per HA:`

- LOPEEI
- RUPA
- SOUTHERN DIVISION
- LOKOPO
- LOTOME
- MATANY
- NORTHERN DIVISION
- NADUNGET
- NGOLERIET
- AMUDAT TOWN COUNCIL
  
`4 Districts with lowest maize yield per HA:`

- MOROTO
- NAPAK
- KAABONG
- ABIM

`10 Sub-Counties with lowest maize yield per HA:`

- SOUTHERN DIVISION
- TAPAC
- NORTHERN DIVISION
- MATANY
- LOTOME
- NGOLERIET
- KATIKEKILE
- NADUNGET
- KALAPATA
- KAABONG EAST

`Correlation between population size and total yield`

- There is a weak but positive correlation between population size and total yield.

`Correlation between crop area and total yield`
- There is a strong and positive correlation between crop area and total yield.

## CONCLUSION

1. Regions with Lowest Total Yield
The analysis highlights the following districts and sub-counties with the lowest total yield.

- Districts: Moroto, Abim, Amudat, and Napak.

- Sub-Counties: Southern Division, Northern Division, Amudat Town Council, Nakapiripirit Town Council, Kaabong Town Council, Katikekile, Lodiko, Kaabong East, Ngoleriet, and Tapac.

2. Regions with Lowest Maize Yield per HA
The analysis identifies the following districts and sub-counties that are struggling specifically with sorghum production.

- Districts: Moroto, Napak, Amudat, and Kaabong.

- Sub-Counties: Lopeei, Rupa, Southern Division, Lokopo, Lotome, Matany, Northern Division, Nadunget, Ngoleriet, and Amudat Town Council.

3. Regions with Lowest Maize Yield per HA The findings point to the districts and sub-counties with the lowest maize yields per hectare as follows:
- Districts: Moroto, Napak, Kaabong, and Abim.

- Sub-Counties: Southern Division, Tapac, Northern Division, Matany, Lotome, Ngoleriet, Katikekile, Nadunget, Kalapata, and Kaabong East.

4. There is a weak but positive correlation between population size and total yield, suggesting that as the population increases, total yield tends to increase as well.

5. The more area a region has allocated for crops, the higher the chance of a bigger yield.


## RECOMMENDATIONS

1. If the organization has limited resources, focus should be made on the most affected areas first before proceeding to the other areas in the region.
2. As the region also suffers from pests and disease outbreak, it would be important to explore the effect of these on crop production in the different regions as well.
3. It is important to also analyze the impact of farming practices used across the different regions crop yields.
4. Population is a huge factor in farming. It is worth exploring how population density and not just the absolute numbers, affects productivity.
