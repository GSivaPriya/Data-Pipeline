# Sales data Pipeline
### Objective:
Creating a sales datapipline for a Retail company
To prepare a pipeline that fetches data from a csv file names Sales data.csv, a json file from JSONPlaceholder API - /users for users data, and Weather data from OpenWeatherMap API.
The goal is to create a database table with all the data merged to create visualizations and to gain insights from the data.

### Dependencies:
You will require:
1. pandas
2. matplotlib
3. requests
4. python-dotenv
5. sqlite3
6. os

Pandas is used for creating and manipulating dataframes
Matplotlib is used for visualising the data
Requests is used for sending requests to the API and fetch the data
python-dotenv is used to securely store the confidential variables (API keys)
Sqlite3 for creating a database and a Sales_Table to store the final data created

# Setting up Code Environment
1. Create a python 3.10 virtual environment.
2. Create Environment variables to store your credentials:
    Weather API key with variable name WEATHER_API_KEY
3. Install all the dependencies by running the command : pip install -r requirements.txt

# Code execution
Run the file "sales_data_pipeline.ipynb" using python sales_data_pipeline.ipynb

# Alternate method
## Running the Docker container

To run the Docker container, first pull the image from Docker Hub:

```sh
docker pull sivapriyag/sales_data_pipeline:latest
```
Then run the following command

docker run -p 8888:8888 sivapriyag/sales_data_pipeline:latest

 
# Description of the Data Pipeline
### Phase 1:
The pipeline starts with importing necessary dependencies: os, pandas, matplotlib, requests and sqlite3. Then th sales data is fetched from the csv file to the dataframe 'sales_data'. It contained 1000 rows. The data is checked for null values and duplicates. Upon checking it was found that the order_id of the sales_data is duplicated. As order_ids cannot be duplicates, the duplicated values are removed and we remain with 945 total entries which are stored in a new dataframe :'sales_data_unique'.

### Phase 2:
Next, data regarding the users is fetched from "https://jsonplaceholder.typicode.com/users" using requests library. By utilizing the function get_user_data() (which returns the normalised dataframe), the data from the url is obtained in json format which is further transformed to a dataframe named 'user_data'. The necessary columns such as id, name, username, email, city, latitude and longitude are kept and rest of the data are removed which gives us the final user_data dataframe.

### Phase 3:
Then, Weather data for each user entry is fetched by utilizing the OpenWeatherMap API by providing latitude and longitude data to the API. Weather information such as main_weather, feels_like, humidity etc are fetched from the API. A new dataframe 'weather_data' is created using the latitude, longitude and the other weather information. The work is done by 2 functions: get_weather_info(lat,lng) and create_weather_info(dataframe)

The get_weather_info() takes in the latitude and longitude values, hits the API and fetches all the information regarding weather in metric units in json format and returns the same.
The create_weather_info() takes in the user_data which contains the latitude and longitude features, iterates over each row to access the coordinates, uses the get_weather_info() funtion to fetch the weather data, extracts the required features from the json (main weather, humidity etc), and finally converts the data into a dataframe resulting in 'weather_data'. This dataframe is returned by the create_weather_info() function.

Column names are renamed for maintaining simplicity.


### Phase 4:
As the aim is to create a new table with all the information combined, a new dataframe 'merged_df' is created by merging user data with weather data on latitude and longitude, and this data is further merged with sales_table based on customer ids. The merged_df containes 18 columns. 

Changes to the datatype: The date of order was changed to datetime type.

Utilizing the merged_df, Visualizations are created to know:
1. Total sales per customer.
2. Average order quantity per product.
3. Top selling products.
4. Sales trend over time.
5. Average sales based on the weather condition.
6. Top customers
By the help of matplotlib.

### Phase 5
Sqlite3 is used to create a database called : sales_data_pipeline.db and a new table with name Sales_Table is created, in which the the merged_df data is entered. As Sqlite3 does not have the datatype 'Date', the order_date is converted into string type and a new column 'order_date_str' is created.

The database schema:
order_id INT, customer_id INT, product_id INT, quantity INT, price REAL, name TEXT, username TEXT, email TEXT, lat REAL, lng REAL, main_weather TEXT, description TEXT, temperature REAL, feels_like REAL, humidity INT, pressure REAL, order_date_str TEXT,  PRIMARY KEY (order_id)

The order_id is selected as the Primary Key.