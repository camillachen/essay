# Geo 458 Essay
## Xiao Ye Chen


## Introduction
The digital-geography project is titled " Seattle On Street Parking: Rates Vary by Time of Day." The goal of the project is to let people who plan to park in Seattle know the price by the time of the day. The major functions are showing areas with specific area's parking cost. Clicking on the area will show the cost of the parking area and when certain start time begin and end for parking. Another function the option of clicking on the time of the day buttom on top, that displays

1. Morning Rates
2. Midday Rates
3. Evening Rates


 Clicking on each rate would change the map content because certain area's price of parking will change depending on the time of the day.

There is a legend that shows the color of cost of parking. The target audience are people who plan to park in Seattle. Just being a Seattle driver isn't specific enough, because if they are Uber or someone who drives out of Seattle for work, they wouldn't need to park in Seattle area. It has to be specifcally someone who wants to park in Seattle that isn't their home or apartment parking area.  The author is the Seattle City GIS workers from the Seattle Department of Transportation.


The client server is ArcGIS online, powered ESRI online. The data is from is from the Seattle Department of Transportation. I think the client is gisrevprxy.seattle.gov.


The major libaries in use and their functions.
Does this project support responsive design?

The Data that is flowed between the client and the server is the map of Seattle, and the colored polygons with the cost and start and end time detail of the parking event. It also has information of sending back the areas that are marked with colored polygons to show the different costs of parking.
The project supports responsive design. The webpage does get bigger or smaller as the user interacts with the zoom, but it does not disrupt or makes the page unreadable. It looks fine in all zooms and readable.
Here are all the Javascript Arcgis libraries they use.

These are the javascript libraries that helps control what the map does and what it looks like.
<pre><code>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/nls/jsapi_en-us.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/dojox/gfx/svg.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/dojox/gfx/svg.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/dojox/gfx/svgext.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/dijit/Search.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/tasks/locator.js"></script>
<script type="text/javascript" charset="utf-8" src="/apps/MapSeries/resources/common/nls/webmap.js?v=1.18.0.js"></script>
<script type="text/javascript" charset="utf-8" src="/apps/MapSeries/resources/common/nls/media.js?v=1.18.0.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/arcgis/Portal.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/dijit/Legend.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/dijit/OverviewMap.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/dijit/BasemapGallery.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/styles/basic.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/tasks/AddressCandidate.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/layers/VectorTileLayer.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/layers/ArcGISImageServiceLayer.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/virtualearth/VETiledLayer.js"></script>
<script type="text/javascript" charset="utf-8" src="./resources/tpl/viewer/nls/template.js?v=1.18.0"></script>
<script type="text/javascript" charset="utf-8" src="/apps/MapSeries/resources/common/nls/core.js?v=1.18.0.js"></script>
<script type="text/javascript" charset="utf-8" src="/apps/MapSeries/app/custom-scripts.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/layers/VectorTileLayerImpl.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/layers/nls/VectorTileLayerImpl_en-us.js"></script>
<script type="text/javascript" charset="utf-8" src="https://js.arcgis.com/3.32/esri/layers/LabelLayer.js"></script>
</code></pre>

Here are some of the javascript libraries that helps displays what the webpage looks like.
<pre><code>
<script src="app/main-app.js?v=1.18.0"></script>
<script src="app/viewer-min.js?v=1.18.0"></script>
<script src="app/config.js?v=1.18.0"></script>
<script src="https://js.arcgis.com/3.32/init.js"></script>
</code></pre>

Here are the functions.
<pre><code>function loadJS(url, isExternal)
{
	if( isExternal )
		url = document.location.protocol == 'file:' ? 'http:' + url : url;
	else
		url += '?v=' + app.version + (!app.isProduction ? '&_=' + new Date().getTime() : '');

	var ref = window.document.getElementsByTagName('script')[0];
	var script = window.document.createElement('script');
	script.src = url;
	script.async = false;
	ref.parentNode.insertBefore(script, ref);
}

function loadCSS(url, isExternal)
{
	if( isExternal )
		url = document.location.protocol == 'file:' ? 'http:' + url : url;
	else
		url += '?v=' + app.version + (!app.isProduction ? '&_=' + new Date().getTime() : '');

	var el = document.createElement("link");
	el.setAttribute("rel", "stylesheet");
	el.setAttribute("type", "text/css");
	el.setAttribute("href", url);
	document.getElementsByTagName("head")[0].appendChild(el);
}

function getUrlVar(name)
{
	var vars = [], hash;
	if( window.location.href.indexOf('?') == -1 ) return null;

	var hashes = window.location.href.slice(window.location.href.indexOf('?') + 1).split('&');
	for(var i = 0; i < hashes.length; i++){
		hash = hashes[i].split('=');
		hash[0] = hash[0].split('#')[0];
		vars.push(hash[0]);
		vars[hash[0]] = (hash[1] == undefined) ? true : hash[1];
	}
	return vars[name];
}

function defineDojoConfig()
{
	var path1 = location.pathname.replace(/\/[^/]+$/, '/');

	window.dojoConfig = {
		parseOnLoad: true,
		isDebug: false,
		useDeferredInstrumentation: true,
		async: !app.isProduction,
		has: { "esri-webgl-max-contexts": -1 },
		//cacheBust: ! app.isProduction,
		packages: [
			{
				name: 'app',
				location: path1 + 'app'
			},{
				name: 'storymaps',
				location: path1 + 'app/storymaps'
			},
			{
				name: 'lib-app',
				location: path1 + 'lib-app'
			},
			{
				name: 'lib-build',
				location: path1 + 'lib-build'
			},
			{
				name: 'commonResources',
				location: path1 + (app.isProduction ? 'resources/common' : 'app/storymaps/common/_resources/')
			}
		],
		aliases: [
			['text', 'lib-build/text'],
			['underscore', 'lib-build/lodash']
		]
	};

	if (location.search.match(/locale=([\w\-]+)/)) {
		window.dojoConfig.locale = RegExp.$1;
	}
}

app.isProduction = true;

defineDojoConfig();

app.isInBuilder = getUrlVar('edit') || getUrlVar('fromScratch') || getUrlVar('fromscratch');
app.indexCfg = configOptions;

loadCSS(app.pathJSAPI + "esri/css/esri.css", true);
loadCSS(app.pathJSAPI + "dijit/themes/claro/claro.css", true);

if( app.isProduction ) {
	if ( app.isInBuilder )
		loadCSS("app/builder-min.css");
	else
		loadCSS("app/viewer-min.css");
}

loadJS(app.pathJSAPI + 'init.js', true);
loadJS('app/config.js');

CKEDITOR_BASEPATH = app.isProduction ? 'resources/lib/ckeditor/' : 'lib-app/ckeditor/';

if( app.isProduction ) {
	_ = {};

	if ( app.isInBuilder )
		loadJS('app/builder-min.js');
	else
		loadJS('app/viewer-min.js');
}

loadJS('app/main-app.js');

// Enable Google Analytics on storymaps.esri.com
if (window.location.href.toLowerCase().indexOf("storymaps.esri.com") >= 0) {
	var _gaq = _gaq || [];
	_gaq.push(['_setAccount', 'UA-26529417-1']);
	_gaq.push(['_trackPageview']);

	(function() {
		var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
		ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
		var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
	})();
}
</code></pre>


I can't find the geojson source, so I cannot display it.

The tilelayers are shown in the image below.
![tileLayers](tilelayer.jpg).
You can see there are 4 javascript tilelayers to show. One that shows the rcGISImageServiceLayer, one that shows LableLayer javascript, and the last two shows the VectorTile layer javascript.

<mark>The overall UI/UX and Web Mapping the design this webpage has is very use friendly overall and is the design is basic. </mark>The webpage is easy to navigate overall, with the information disaplyed as is. The basemap is easy to read and the dullness color of it mapes the colored areas stand out, sort of guiding the user to see those areas are interactive.  It uses legend as stated earlier. I do think the map would be more user friendly if that made the pointer change to one that shows the colored polygons are clickable so the user know for sure you can click on that area to interact with.

Here is the information displayed on the Legend for the colored areas for the morning rates:

| Morning:       | 8am - 11am ($/hr) |
| ----------- | ----------- |
| Purple      | $0.50      |
| Light Purple   | $1.00       |
| Blue      | $1.50      |
| Light Blue     | $2.00      |
| Green      | $2.50      |
| Light Green      | $3.00      |
| Yellow      | $3.50      |
| Orange      | $4.00      |
| Pink      | $4.50      |
| Red      | $5.00      |


The website heavily relies on javascript libraris and is powered by ESRI. I think this map is very useful and easy for anyone to navigate for those wanting to know about the parking cost in certain areas in Seattle. I think it would be more useful if this map was more well known so people could decide where they would park based on the area. Some of the parking area cost go as high as $5.00 per hour, and that could affect where someone would choose to go. If they plan to eat at a restaurant for two hours, but it would cost $10.00 just to park, they would decide on another place to eat. I think it is important for people who are cautious about their money spending.

<mark>Word Count icluding the markdown information and codes: 	1596 </mark>
