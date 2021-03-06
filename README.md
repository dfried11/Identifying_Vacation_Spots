# Analysis of Weather using APIs


## General Overview

Using WeatherPy.ipynb, extracts data from Open Weather Map API and creates a CSV file of weather information for several hundred cities throughout the world. Analyzes the influence of latitude on weather using regression; visualizes results with Matplotlib. Using VacationPy.ipynb, creates a heatmap that visualizes differences in humidity between cities; overlayes the map with hotels from locations experiencing great weather.


### WeatherPy.ipynb

Weather data was extracted from [openweathermap.org](https://api.openweathermap.org). Data from each API request were converted to a json object. Below are the general project steps.

1. Generated a list of cities: Looped through a list of over 600 latitude-longitude pairs to find the nearest city using Citipy.
2. Extracted weather information for each city using a series of successive API calls; saved weather data for each city in lists.
3. Created a Pandas dataframe from the lists and exported the dataframe to a CSV file ("cities.csv").
4. Used regression to analyze the influence of latitude on weather. Created visualizations with Matplotlib.

          def regression(x, y, x_label, y_label, hemisphere):
              title = f'{hemisphere} Hemisphere:\nRegressing {y_label} on {x_label}'
              (slope, intercept, rvalue, pvalue, stderr) = linregress(x, y)
              regress_values = x * slope + intercept
              line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
              plt.scatter(x, y)
              plt.plot(x,regress_values,"r-")
              plt.xlabel(x_label)
              plt.ylabel(y_label)
              plt.title(title)
              title = title.replace(':\n', '_').replace(' ', '_')
              plt.savefig(f'output_data/{title}.png')
              plt.show()
              print(line_eq)
              print()
              print(f"r = {pearsonr(x, y)[0]:.2f}, p = {pearsonr(x, y)[1]:.4f}, r_squared = {rvalue**2:.2f}")
              print()
      
![Example of Regression Output](/WeatherPy/output_data/Northern_Hemisphere_Regressing_Max_Temperature_(F)_on_Latitude.png)

![Example of Regression Interpretation](/WeatherPy/output_data/Interpretation_NH_Temp_Latitude.PNG)


### VacationPy.ipynb

Created a heatmap with [Google Maps Platform](https://maps.googleapis.com) and the CSV file generated from WeatherPy.ipynb ("cities.csv"). The heatmap visualizes differences in humidity between cities. Identifies cities experiencing great weather; for each of these cities, finds the nearest hotel within a 5,000 meter radius and adds the hotel name to the heatmap.

![Hotel Map](/VacationPy/output_data/hotel_map.png)


