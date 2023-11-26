# python-api-challenge

# The requirements for "Part 1: WeatherPy" are the following:

    1. Create Plots to Showcase the Relationship Between Weather Variables and Latitude (30 points)
    
        - Use the OpenWeatherMap API to retrieve weather data from the cities list generated in the started code (10 points)
            - First I set the base url to be used in this activity
            
                # Set the API base URL
                url = "http://api.openweathermap.org/data/2.5/weather?appid="+weather_api_key+"&units=metric&q="
                
            - Then we had to create our endpoint URL to make the request for each city in our loop
            
                # Create endpoint URL with each city
                city_url = requests.get(url + city)
                
            - Within the try statement we had to convert the request to json()
            
                # Parse the JSON and retrieve data
                city_weather = city_url.json()
                
            - Then we had to pull out our desired values from the API. I pulled an example of one city in a previous cell so I could find how to pull the necessary information
            
                # Parse out latitude, longitude, max temp, humidity, cloudiness, wind speed, country, and date
                city_lat = city_weather["coord"]["lat"]
                city_lng = city_weather["coord"]["lon"]
                city_max_temp = city_weather["main"]["temp_max"]
                city_humidity = city_weather["main"]["humidity"]
                city_clouds = city_weather["clouds"]["all"]
                city_wind = city_weather["wind"]["speed"]
                city_country = city_weather["sys"]["country"]
                city_date = city_weather["dt"]
                
            - The rest of the code for this was already provided other than us creating a DataFrame from our results we could use in our plots later
                
            - **Code for this was taken from activities performed in class. Specifically, Weather_Stats_Solution**

        - Create a scatter plot to showcase the relationship between Latitude vs. Temperature (5 points)
            - Used plt.scatter to create the plot based on the information that was needed in this part of the assignment
            
                    # Build scatter plot for latitude vs. temperature
                    plt.scatter(city_data_df["Lat"],city_data_df["Max Temp"], marker="o", edgecolor="black")

                    # Incorporate the other graph properties
                    plt.title("City Max Latitude vs. Temperature (2023-11-25)")
                    plt.ylabel("Max Temperature (C)")
                    plt.xlabel("Latitude")
                    plt.grid(True)

                    # Save the figure
                    plt.savefig("../output_data/Fig1.png")

                    # Show plot
                    plt.show()
                    
             - **Code for this was taken from activities we performed in class. With the exception of the edgecolor, which I got from ChatGPT**

        - Create a scatter plot to showcase the relationship between Latitude vs. Humidity (5 points)
            - Used plt.scatter to create the plot based on the information that was needed in this part of the assignment
            
                    # Build the scatter plots for latitude vs. humidity
                    plt.scatter(city_data_df["Lat"],city_data_df["Humidity"], marker="o", edgecolor="black")

                    # Incorporate the other graph properties
                    plt.title("City Latitude vs. Humidity (2023-11-25)")
                    plt.ylabel("Humidity (%)")
                    plt.xlabel("Latitude")
                    plt.grid(True)

                    # Save the figure
                    plt.savefig("output_data/Fig2.png")

                    # Show plot
                    plt.show()
                    
             - **Code for this was taken from activities we performed in class. With the exception of the edgecolor, which I got from ChatGPT**

        - Create a scatter plot to showcase the relationship between Latitude vs. Cloudiness (5 points)
            - Used plt.scatter to create the plot based on the information that was needed in this part of the assignment
            
                    # Build the scatter plots for latitude vs. cloudiness
                    plt.scatter(city_data_df["Lat"],city_data_df["Cloudiness"], marker="o", edgecolor="black")

                    # Incorporate the other graph properties
                    plt.title("City Latitude vs. Cloudiness (2023-11-25)")
                    plt.ylabel("Cloudiness (%)")
                    plt.xlabel("Latitude")
                    plt.grid(True)

                    # Save the figure
                    plt.savefig("output_data/Fig3.png")

                    # Show plot
                    plt.show()
                    
             - **Code for this was taken from activities we performed in class. With the exception of the edgecolor, which I got from ChatGPT**

        - Create a scatter plot to showcase the relationship between Latitude vs. Wind Speed (5 points)
            - Used plt.scatter to create the plot based on the information that was needed in this part of the assignment
            
                    # Build the scatter plots for latitude vs. wind speed
                    plt.scatter(city_data_df["Lat"],city_data_df["Wind Speed"], marker="o", edgecolor="black")

                    # Incorporate the other graph properties
                    plt.title("City Latitude vs. Wind Speed (2023-11-25)")
                    plt.ylabel("Wind Speed (%)")
                    plt.xlabel("Latitude")
                    plt.grid(True)

                    # Save the figure
                    plt.savefig("output_data/Fig4.png")

                    # Show plot
                    plt.show()
                    
            - **Code for this was taken from activities we performed in class. With the exception of the edgecolor, which I got from ChatGPT**

    2. Compute Linear Regression for Each Relationship (40 points)
    
        - Linear regression scatter plot for Northern Hemisphere: Temperature (C) vs. Latitude (5 points)
            - I did not create a variable for linear regression like indicated in the starter code. But the assignment didn't specify that we had to do it that way, which is why I went with this route.
            - First created my DataFrames for the northern and southern hemispheres to reference in my plots. 
            
                    # Create a DataFrame with the Northern Hemisphere data (Latitude >= 0)
                    northern_hemi_df = city_data_df.loc[city_data_df["Lat"] >= 0,:]
                    
                    # Create a DataFrame with the Southern Hemisphere data (Latitude < 0)
                    southern_hemi_df = city_data_df.loc[city_data_df["Lat"] < 0,:]
                    
            - Then I created my plot with the linear regression for the desired parameters. 
            
                    # Linear regression on Northern Hemisphere
                    x_values = northern_hemi_df["Lat"]
                    y_values = northern_hemi_df["Max Temp"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(1,-25),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Max Temp')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
             - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**

        - Linear regression scatter plot for Southern Hemisphere: Temperature (C) vs. Latitude (5 points)
            - I created my plot with the linear regression for the desired parameters. This is all stuff we've learned in previous classes. And we really just had to add the equations and make some adjustments based on the desired effect.
            
                    # Linear regression on Southern Hemisphere
                    x_values = southern_hemi_df["Lat"]
                    y_values = southern_hemi_df["Max Temp"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(-35,8),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Max Temp')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
            - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**

        - Linear regression scatter plot for Northern Hemisphere: Humidity (%) vs. Latitude (5 points)
            - I created my plot with the linear regression for the desired parameters. This is all stuff we've learned in previous classes. And we really just had to add the equations and make some adjustments based on the desired effect.
            
                    # Northern Hemisphere
                    x_values = northern_hemi_df["Lat"]
                    y_values = northern_hemi_df["Humidity"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(45,20),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Humidity')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
             - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**

        - Linear regression scatter plot for Southern Hemisphere: Humidity (%) vs. Latitude (5 points)
            - I created my plot with the linear regression for the desired parameters. This is all stuff we've learned in previous classes. And we really just had to add the equations and make some adjustments based on the desired effect.
            
                    # Southern Hemisphere
                    x_values = southern_hemi_df["Lat"]
                    y_values = southern_hemi_df["Humidity"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(-25,20),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Humidity')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
             - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**

        - Linear regression scatter plot for Northern Hemisphere: Cloudiness (%) vs. Latitude (5 points)
            - I created my plot with the linear regression for the desired parameters. This is all stuff we've learned in previous classes. And we really just had to add the equations and make some adjustments based on the desired effect.
            
                    # Northern Hemisphere
                    x_values = northern_hemi_df["Lat"]
                    y_values = northern_hemi_df["Cloudiness"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(48,50),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Cloudiness')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
            - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**

        - Linear regression scatter plot for Southern Hemisphere: Cloudiness (%) vs. Latitude (5 points)
            - I created my plot with the linear regression for the desired parameters. This is all stuff we've learned in previous classes. And we really just had to add the equations and make some adjustments based on the desired effect.
            
                    # Southern Hemisphere
                    x_values = southern_hemi_df["Lat"]
                    y_values = southern_hemi_df["Cloudiness"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(-55,80),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Cloudiness')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
            - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**

        - Linear regression scatter plot for Northern Hemisphere: Wind Speed (m/s) vs. Latitude (5 points)
            - I created my plot with the linear regression for the desired parameters. This is all stuff we've learned in previous classes. And we really just had to add the equations and make some adjustments based on the desired effect.
            
                    # Northern Hemisphere
                    x_values = northern_hemi_df["Lat"]
                    y_values = northern_hemi_df["Wind Speed"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(5,17),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Wind Speed')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
            - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**

        - Linear regression scatter plot for Southern Hemisphere: Wind Speed (m/s) vs. Latitude (5 points)
            - I created my plot with the linear regression for the desired parameters. This is all stuff we've learned in previous classes. And we really just had to add the equations and make some adjustments based on the desired effect.
            
                    # Southern Hemisphere
                    x_values = southern_hemi_df["Lat"]
                    y_values = southern_hemi_df["Wind Speed"]
                    (slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
                    regress_values = x_values * slope + intercept
                    line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
                    # Plot scatter plot
                    plt.scatter(x_values,y_values)
                    # Plot regression line
                    plt.plot(x_values,regress_values,"r-")
                    plt.annotate(line_eq,(-35,17),fontsize=15,color="red")
                    # Label plot
                    plt.xlabel('Latitude')
                    plt.ylabel('Wind Speed')
                    # Print r square value
                    print(f"The r-value is: {rvalue}")
                    # Show plot
                    plt.show()
                    
            - **Code was taken from activities we had performed in class. Specifically, the banking_deserts_solution**
            
       - **The last part of this section was the explain what was happening in the linear regression with the northern and southern hemispheres for each set of the parameters. I answered this in the the code file so it should be located there to review.**

# The requirements for "Part 2: VacationPy" are the following (30 points)

        3. Create a map that displays a point for every city in the city_data_df DataFrame (5 points)
            - We first read in our csv we had created with our city data earlier
            - Then we used hvplot.points() to plot a map our data. We based it off the Latitude and Longitude of each city, set the size = to the Humidity column of our DataFrame, and set the color=to city to match the picture provided. We also added geo and tiles to specify the map and the format we wanted
            
                    # Configure the map plot
                    map_plot_1 = city_data_df.hvplot.points(
                        "Lng",
                        "Lat",
                        geo = True,
                        tiles = "OSM",
                        size = "Humidity",
                        color = "City"
                    )

                    # Display the map plot_1
                    map_plot_1
                    
             - **Code for this was provided in the activities we performed in class. Specifically, the geoviews_demo_solution**

        4. Narrow down the city_data_df DataFrame to find your ideal weather condition (5 points)
            - I then used the loc method to only pull the cities I wanted based on my ideal weather conditions. 
            - I also used methods we had learned in class to drop rows with null values.
            
                    # Narrow down cities that fit criteria and drop any results with null values
                    ideal_city_df = city_data_df.loc[(city_data_df["Max Temp"] > 19) & (city_data_df["Max Temp"] < 28) & 
                                                    (city_data_df["Wind Speed"] > 2) & (city_data_df["Wind Speed"] < 10) & 
                                                     (city_data_df["Humidity"] > 30) & (city_data_df["Humidity"] < 60), :]

                    # Drop any rows with null values
                    ideal_city_df = ideal_city_df.dropna(how='any')

                    # Display sample data
                    ideal_city_df
                    
             - I then created my new DataFrame and added a column for the Hotel
             
                     # Use the Pandas copy function to create DataFrame called hotel_df to store the city, country, coordinates, and humidity
                    hotel_df = ideal_city_df[["City", "Country", "Lat", "Lng", "Humidity"]]

                    # Add an empty column, "Hotel Name," to the DataFrame so you can store the hotel found using the Geoapify API
                    hotel_df["Hotel Name"] = ""

                    # Display sample data
                    hotel_df
                    
             - **Code for this was taken from activities we performed in class. ChatGPT also helped me resolve the syntax errors I was receiving when trying to do my loc. I wasn't using the proper syntax to separate my different criteria.**

        5. For each city in the hotel_df DataFrame, use the Geoapify API to find the first hotel located within 10,000 metres of your coordinates (10 points)
            - We first had to set our parameters before the loop to specify what we wanted to look at. 
            - Set the radius = to 10000, set a limit (probably didn't need it since we were pulling the first one), set my categories for hotel that I found on the API documentation, and then set the params
            
                    # Set parameters to search for a hotel
                    radius = 10000
                    limit = 20
                    categories = "accommodation.hotel"
                    params = {
                        "categories":categories,
                        "limit":limit,
                        "apiKey": geoapify_key
                    }
                    
             - Then we had to pull the latitude and longitude from the DataFrame within the for loop and then add it to our params
                    # get latitude, longitude from the DataFrame
                    lat = hotel_df.loc[index, "Lat"]
                    lon = hotel_df.loc[index, "Lng"]

                    # Add filter and bias parameters with the current city's latitude and longitude to the params dictionary
                    params["filter"] = f"circle:{lon},{lat},{radius}"
                    params["bias"] = f"proximity:{lon},{lat}"
                    
             - Then we had to make the request using our base url and the params, and convert the results to json()
             
                    # Set base URL
                    base_url = "https://api.geoapify.com/v2/places"


                    # Make and API request using the params dictionaty
                    name_address = requests.get(base_url, params=params)

                    # Convert the API response to JSON format
                    name_address = name_address.json()
                    
             - The rest of the code was provided for us and we just had to run the cell
             - **Code for this was taken from activities we performed in class. Specifically, the restaurants solution really helped me.

        6. Add the hotel name and the country as additional information in the hover message for each city in the map. (10 points)
            - Finally, I added the desired hover points using hover_cols[]. ChatGPT helped me with this method. 
            
                # Configure the map plot
                map_plot_2 = hotel_df.hvplot.points(
                    "Lng",
                    "Lat",
                    geo = True,
                    tiles = "OSM",
                    size = "Humidity",
                    frame_width = 700,
                    frame_height = 500,
                    color = "City", 
                    hover_cols=["Country", "Hotel Name"]
                )

                # Display the map plot_1
                map_plot_2
                
            - **Code for this was taken from ChatGPT, which helped my find the hover_cols=[] solution.