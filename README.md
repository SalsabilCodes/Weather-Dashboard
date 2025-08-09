# Power BI Weather Dashboard with WeatherAPI

This project shows how to build a **real-time weather dashboard** in Power BI using live data from WeatherAPI. The dashboard displays current weather conditions along with Air Quality Index (AQI) indicators for a comprehensive environmental overview.

---

## Project Status: Completed

---

## Project Overview

The dashboard integrates WeatherAPI’s JSON data into Power BI, enabling users to monitor temperature, humidity, wind speed, and air quality metrics across multiple cities. It includes data transformation steps, interactive visuals, and reusable DAX measures to classify AQI levels with color coding and health suggestions.

---

## Data Source

- WeatherAPI.com — provides live, historical, and forecast weather data via REST API in JSON format.

---

## Methods Used

- Power BI Web connector for API integration  
- Power Query Editor to parse and transform JSON data  
- DAX for AQI classification and dynamic measures  
- Interactive visuals: Cards, Gauges, Maps, Slicers  

---

## Technologies

- Power BI Desktop  
- WeatherAPI RESTful service  
- DAX (Data Analysis Expressions)  

---

## Project Details

### 1. Obtain WeatherAPI Key
- Register on WeatherAPI.com and get your API key for authentication.

### 2. Construct API URL
- Example URL for current weather:  
  `https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=CITY_NAME`

### 3. Connect Power BI to WeatherAPI
- Use **Get Data > Web** in Power BI Desktop to connect to the API URL.

### 4. Transform Data
- Expand nested records (`current`, `condition`, `air_quality`) in Power Query.  
- Rename columns and adjust data types for clarity.

### 5. Build Dashboard
- Add cards (temperature, humidity), gauges (wind speed), charts (daily trends), and slicers (city selector).

### 6. Styling & Interactivity
- Insert weather icons and map visuals for city locations.  
- Enable dynamic filtering with slicers.

### 7. Add AQI Indicators with Reusable DAX Measures
- Create generic DAX measures for AQI Color, Suggestion, and Status using pollutant columns such as `pm2_5`, `co`, `no2`.  
- Example for AQI Color:

```DAX
AQI Color TEMPLATE =
VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
RETURN
SWITCH(
    TRUE(),
    AQI <= 50, "#43d946",
    AQI <= 100, "#fff570",
    AQI <= 150, "#ff9800",
    AQI <= 200, "#d99343",
    AQI <= 300, "#ff5b0f",
    "#d95243"
)

