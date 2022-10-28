A simple Vue app that allows a user to search for a location, and uses two of OpenWeatherMap's APIs to return current weather data.
First, the location query is sent to Geocoding API to fetch latitude and longitude based on the name of the city. Second, the lat and lon values are used to request weather data from Current Weather Data API.

The background is changed to reflect if the weather is warm or cold.

![Warm Weather](./preview-img/ktm_weather.png?raw=true "Warm Weather Preview")
![Cold Weather](./preview-img/nuuk_weather.png?raw=true "Cold Weather Preview")


# vue-weather

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
