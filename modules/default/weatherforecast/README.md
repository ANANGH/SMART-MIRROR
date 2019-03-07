# Module: Weather Forecast
The `weatherforecast` module is one of the default modules of the SmartMirror.
This module displays the weather forecast for the coming week, including an an icon to display the current conditions, the minimum temperature and the maximum temperature.

## Screenshots

- 5 day forecast
![Screenshot of 5 day forecast](forecast_screenshot.png)

## Using the module

To use this module, add it to the modules array in the `config/config.js` file:
````javascript
modules: [
	{
		module: "weatherforecast",
		position: "top_right",	// This can be any of the regions.
									// Best results in left or right regions.
		config: {
			// See 'Configuration options' for more information.
			location: "Amsterdam,Netherlands",
			locationID: "", //Location ID from http://openweathermap.org/help/city_list.txt
			appid: "abcde12345abcde12345abcde12345ab" //openweathermap.org API key.
		}
	}
]
````
