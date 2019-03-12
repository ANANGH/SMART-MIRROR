# Module: Calendar
The `calendar` module is one of the default modules of the SmartMirror.
This module displays events from a public .ical calendar. It can combine multiple calendars.

## Using the module

To use this module, add it to the modules array in the `config/config.js` file:
````javascript
modules: [
	{
		module: "calendar",
		position: "top_left",	// This can be any of the regions. Best results in left or right regions.
		config: {
			// The config property is optional.
			// If no config is set, an example calendar is shown.
			// See 'Configuration options' for more information.
		}
	}
]
````

### Calendar configuration

The `calendars` property contains an array of the configured calendars.
The `colored` property gives the option for an individual color for each calendar.
The `coloredSymbolOnly` property will apply color to the symbol only, not the whole line. This is only applicable when `colored` is also enabled.

#### Default value:
````javascript
config: {
	colored: false,
	coloredSymbolOnly: false,
	calendars: [
		{
			url: 'http://www.calendarlabs.com/templates/ical/US-Holidays.ics',
			symbol: 'calendar',
			auth: {
			    user: 'username',
			    pass: 'superstrongpassword',
			    method: 'basic'
			}
		},
	],
}
````

#### Calendar configuration options:
| Option                | Description
| --------------------- | -----------
| `url`	                | The url of the calendar .ical. This property is required. <br><br> **Possible values:** Any public accessble .ical calendar.
| `symbol`              | The symbol to show in front of an event. This property is optional. <br><br> **Possible values:** See [Font Awesome](http://fontawesome.io/icons/) website. To have multiple symbols you can define them in an array e.g. `["calendar", "plane"]`
| `color`              | The font color of an event from this calendar. This property should be set if the config is set to colored: true. <br><br> **Possible values:** HEX, RGB or RGBA values (#efefef, rgb(242,242,242), rgba(242,242,242,0.5)).
| `repeatingCountTitle`	| The count title for yearly repating events in this calendar.  <br><br> **Example:** `'Birthday'`
| `maximumEntries`      | The maximum number of events shown.  Overrides global setting. **Possible values:** `0` - `100`
| `maximumNumberOfDays` | The maximum number of days in the future.  Overrides global setting
| `auth`                | The object containing options for authentication against the calendar.
| `symbolClass`         | Add a class to the cell of symbol.
| `titleClass`          | Add a class to the title's cell.
| `timeClass`           | Add a class to the time's cell.


#### Calendar authentication options:
| Option                | Description
| --------------------- | -----------
| `user`                | The username for HTTP authentication.
| `pass`                | The password for HTTP authentication. (If you use Bearer authentication, this should be your BearerToken.)
| `method`              | Which authentication method should be used. HTTP Basic, Digest and Bearer authentication methods are supported. Basic authentication is used by default if this option is omitted. **Possible values:** `digest`, `basic`, `bearer` **Default value:** `basic`
