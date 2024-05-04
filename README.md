[![DOI](https://zenodo.org/badge/748623024.svg)](https://zenodo.org/doi/10.5281/zenodo.10625192)

<figure>
    <img src="https://github.com/mouddentarik/Earthquake01/assets/107276479/b6ce2e7f-41c3-46f3-9f93-1e3a54bcebe4)" width="300">
    <img src="https://github.com/mouddentarik/Earthquake01/assets/107276479/d97d8e6c-6abf-4324-8e22-c92fa745522d)" width=300>
    <figcaption> 
      The left figure shows: the spatial pattern of earthquakes around the world from 1970-01-03 up to now, according to https://www.arcgis.com/apps/mapviewer.
    The right figure shows: the positions' palents and comets from https://theskylive.com/
    </figcaption>
</figure>


# Implementation

The implementation of creating a final dataset is essential for testing the validity of the relationship between the planet's ‘position and earthquake events. We use Python, which offers powerful libraries to clean, merge, and transform the data.

# Steps Involved
<b>Launch the earthQuakes01.ipynb</b>: the important cells

<ul>
  <li>Earthquakes1.eventType.unique()---> ('Earthquake', 'Nuclear Explosion', 'Quarry Blast', 'Other Event',
    'Explosion', 'Mine Collapse', 'Rock Burst', 'Sonic Boom',
    'Mining Explosion', 'Landslide', 'Collapse', 'Volcanic Eruption')</li>
  <li>Earthquakes2=Earthquakes1.query("eventType == 'Earthquake'")--->isolate only Earthquakes events</li>
  <li> python regex example: to get the planets'position and date from text files </li>

  
```
import re
import datetime

# Create an empty DataFrame with column names
DataFrame_MarsEarth = pd.DataFrame(columns=['Date', 'Mars_Earth'])

file = open("Mars_Earth.txt", "r")
i=0
while True:
    content=file.readline()
    if not content:
        break
#     print(content)
    r1 = re.findall(r"\d{4}/\d{2}/\d{2}",content)
    r2=re.findall(r"\,.*?\],",content)
    r3=re.findall(r"\,.*?\]",r2[0][1:])
    #################################################
    format = '%Y/%m/%d'
    # convert from string format to datetime format
    Dt = datetime.datetime.strptime(r1[0], format)

    Dis=float(r3[0][1:-1])

    DataFrame_MarsEarth.loc[i] = [Dt.date(),Dis]
    
    i=i+1  

file.close()
```
</ul>

<b>Launch the earthQuakes02.ipynb</b>: the important cells
<ul>
  <li>merged_df1=pd.merge(merged_df, DataFrame_MarsEarth, on="Date", how="inner")--->combining two dataset</li>
</ul>



# Future Steps

include comet features into the dataset
