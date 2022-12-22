import json
import numpy as np
import pandas as pd
import plotly.express as px


import plotly.io as pio
pio.renderers.default = 'browser'


import geopandas as gpd
import matplotlib.pyplot as plt
import pathlib


f = pathlib.Path () / 'rain_polyo.json'
assert f.exists ()
gdf = gpd.read_file(f)
gdf.head()


gdf.plot()



df = pd.read_csv("calcifiy_dat.csv")


df.head(50)


fig = px.choropleth(
    df,
    locations=df['ID'],
    geojson=gdf,
    color="COUNT_DD",
    hover_name='Count_LD_50K',
    hover_data=['Count_rain','DD','GRIDCODE','COUNT_DD','Count_LD_50K','Count_rain','Rainfall_mm'],
    title='Rain info',    
)
fig.update_geos(fitbounds="locations", visible=False)



fig.show()
