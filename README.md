# StudyRefs

def select_marker_color(row):
    if row['lived'] == 'yes':
        return 'pink'
    elif row['lived'] == 'no' and row['visited'] == 'yes':
        return 'purple'
    return 'blue'
cities['colors'] = cities.apply(select_marker_color, axis=1)


https://www.youtube.com/watch?v=FdqDgoG-SFM
https://github.com/jtemporal/folium-101/blob/main/folium-101.ipynb

https://panel.holoviz.org/gallery/external/Folium.html

#Folium
https://www.kaggle.com/code/daveianhickey/how-to-folium-for-maps-heatmaps-time-data/notebook

map_hooray = folium.Map(location=[51.5074, 0.1278],
                    zoom_start = 11) # Uses lat then lon. The bigger the zoom number, the closer in you get

from folium import plugins
# Adds tool to the top right
from folium.plugins import MeasureControl
map_hooray.add_child(MeasureControl())


from folium import plugins
map_hooray = folium.Map(location=[51.5074, 0.1278],
                    zoom_start = 13) 
# Ensure you're handing it floats
df_acc['Latitude'] = df_acc['Latitude'].astype(float)
df_acc['Longitude'] = df_acc['Longitude'].astype(float)
# Filter the DF for rows, then columns, then remove NaNs
heat_df = df_acc[df_acc['Speed_limit']=='40'] # Reducing data size so it runs faster
heat_df = df_acc[df_acc['Year']=='2007'] # Reducing data size so it runs faster
heat_df = heat_df[['Latitude', 'Longitude']]
# Create weight column, using date
heat_df['Weight'] = df_acc['Date'].str[3:5]
heat_df['Weight'] = heat_df['Weight'].astype(float)
heat_df = heat_df.dropna(axis=0, subset=['Latitude','Longitude', 'Weight'])
# List comprehension to make out list of lists
heat_data = [[[row['Latitude'],row['Longitude']] for index, row in heat_df[heat_df['Weight'] == i].iterrows()] for i in range(0,13)]
# Plot it on the map
hm = plugins.HeatMapWithTime(heat_data,auto_play=True,max_opacity=0.8)
hm.add_to(map_hooray)
# Display the map
map_hooray




