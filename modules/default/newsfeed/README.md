# Module: News Feed
The `newsfeed ` module is one of the default modules of the SmartMirror.
This module displays news headlines based on an RSS feed. Scrolling through news headlines happens time-based (````updateInterval````), but can also be controlled by sending news feed specific notifications to the module.

## Screenshot
- News Feed Screenshot using the NYT
![NYT News Feed Screenshot](newsfeed_screenshot.png)

## Using the module

### Configuration
To use this module, add it to the modules array in the `config/config.js` file:
````javascript
modules: [
	{
		module: "newsfeed",
		position: "bottom_bar",	// This can be any of the regions. Best results in center regions.
		config: {
			// The config property is optional.
			// If no config is set, an example calendar is shown.
			// See 'Configuration options' for more information.

			feeds: [
				{
					title: "New York Times",
					url: "http://www.nytimes.com/services/xml/rss/nyt/HomePage.xml",
				},
				{
					title: "BBC",
					url: "http://feeds.bbci.co.uk/news/video_and_audio/news_front_page/rss.xml?edition=uk",
				},
			]
		}
	}
]
````

### Notifications
#### Interacting with the module
MagicMirror's [notification mechanism](https://github.com/ANANGH/SMART-MIRROR/tree/master/modules#thissendnotificationnotification-payload) allows to send notifications to the `newsfeed` module. The following notifications are supported:

| Notification Identifier | Description
| ----------------------- | -----------
| `ARTICLE_NEXT`          | Shows the next news title (hiding the summary or previously fully displayed article)
| `ARTICLE_PREVIOUS`      | Shows the previous news title (hiding the summary or previously fully displayed article)
| `ARTICLE_MORE_DETAILS`  | When received the _first time_, shows the corresponding description of the currently displayed news title. <br> The module expects that the module's configuration option `showDescription` is set to `false` (default value). <br><br> When received a _second consecutive time_, shows the full news article in an IFRAME. <br> This requires that the news page can be embedded in an IFRAME, e.g. doesn't have the HTTP response header [X-Frame-Options](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options) set to e.g. `DENY`.<br><br>When received the _next consecutive times_, reloads the page and scrolls down by `scrollLength` pixels to paginate through the article.
| `ARTICLE_LESS_DETAILS`  | Hides the summary or full news article and only displays the news title of the currently viewed news item.
| `ARTICLE_TOGGLE_FULL`   | Toogles article in fullscreen.

Note the payload of the sent notification event is ignored.

#### Example
The following example shows how the next news article title can be displayed on the MagicMirror.
````javascript
this.sendNotification('ARTICLE_NEXT');
````

#### `newsfeed` specific notification emitting modules
The third party [MMM-Gestures](https://github.com/thobach/MMM-Gestures) module supports above notifications when moving your hand up, down, left or right in front of a gesture sensor attached to the MagicMirror. See module's readme for more details.

The `feeds` property contains an array with multiple objects. These objects have the following properties:

| Option     | Description
| ---------- | -----------
| `title`    | The name of the feed source to be displayed above the news items. <br><br> This property is optional.
| `url`      | The url of the feed used for the headlines. <br><br> **Example:** `'http://www.nytimes.com/services/xml/rss/nyt/HomePage.xml'`
| `encoding` | The encoding of the news feed. <br><br> This property is optional. <br> **Possible values:**`'UTF-8'`, `'ISO-8859-1'`, etc ... <br> **Default value:** `'UTF-8'`
