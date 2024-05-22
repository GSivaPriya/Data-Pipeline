# Sales data Pipeline
### Objective:
To prepare a pipeline that fetches data from a csv file names Sales data.csv, a json file from JSONPlaceholder API - /users for users data, and Weather data from OpenWeatherMap API.
The goal is to create a database table with all the data merged to create visualizations and to gain insights from the data.

### Dependencies:
You will require:
1. pandas
2. matplotlib
3. requests
4. python-dotenv
5. sqlite3

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

 
