Wappalyzer
==========

[Wappalyzer](http://wappalyzer.com/) is a 
[browser extension](http://wappalyzer.com/download) that uncovers the 
technologies used on websites.  It detects
[content management systems](http://wappalyzer.com/categories/cms),
[web shops](http://wappalyzer.com/categories/web-shops),
[web servers](http://wappalyzer.com/categories/web-servers), 
[JavaScript frameworks](http://wappalyzer.com/categories/javascript-frameworks),
[analytics tools](http://wappalyzer.com/categories/analytics) and
[many more](http://wappalyzer.com/applications).


Contributing
------------

**Adding a new application**

* Edit `share/apps.json`
* Add a 16x16 PNG image to `share/images/icons` matching the application name.
* Provide the URL to the application's website when submitting a pull request.

Example:

```javascript
"Application Name": { 
	cats:    [ "1" ], 
	headers: { "X-Powered-By": "Application Name" },
	url:     ".+\\.application-name\\.com",
	html:    "<link[^>]application-name\\.css", 
	meta:    { "generator": "Application Name" },
	script:  "application-name\\.js",
	env:     "ApplicationName",
	implies: [ "PHP" ]
	}
```


Drivers
-------

Wappalyzer is multi-platform. The main code lives in the `share/` directory and
platform specific code in `drivers/`. The sections below describe how to set up
a development environment for the various existing drivers.

To keep files synchronised between drivers, run the `links.sh` script (UNIX-like 
system only, Windows user will have to manually copy the files across.)


**Mozilla Firefox**

* Place a file called `wappalyzer@crunchlabz.com` in the extensions directory in
  your [profile folder](http://kb.mozillazine.org/Profile_folder_-_Firefox) 
	(`~/.mozilla/firefox/xxxxx.default/extensions/` on Linux) containing the full
	path to `drivers/firefox`.
* Restart Firefox
* Navigate to `about:config` and set `extensions.wappalyzer.debug` to `true`.
* Ctrl+Shift+J brings up a console for debugging.


**Google Chrome**

The Chrome version needs some love, if anyone wants to pick it up. It's
currently not as feature-rich as the Firefox add-on (although partially due to 
API limitations.)

* Navigate to `about:extensions`
* Check "Developer mode"
* Click "Load unpacked extension..."
* Select `drivers/chrome/`


**Bookmarklet**

Beta version available for testing at [wappalyzer.com/bookmarklet](http://wappalyzer.com/bookmarklet).


**HTML**

The HTML driver serves purely as an example. It's a good starting point if you
want to port Wappalyzer to a new platform.

* Navigate to `drivers/html/`


**PHP**

The PHP driver requires the [V8js](http://php.net/manual/en/book.v8js.php) class. Installing V8js 
using [PECL](http://pecl.php.net/) on Debian Linux or Ubuntu should be very straight forward:

* `# aptitude install php5-dev php-pear libv8-dev`
* `# pecl install channel://pecl.php.net/v8js-0.1.3`
* `# echo "extension=v8js.so" > /etc/php5/conf.d/v8js.ini`

Runnning Wappalyzer from the command line:

`$ php drivers/php/index.php wappalyzer.com`

Running Wappalyzer inside a PHP script:

```php
require('WappalyzerException.php');
require('Wappalyzer.php');

$wappalyzer = new Wappalyzer($url);

$detectedApps = $wappalyzer->analyze();
```


**Mozilla Jetpack**

Work in progress, experimental. See https://wiki.mozilla.org/Jetpack.


Screenshot
----------

Wappalyzer on Firefox:

![Screenshot](http://wappalyzer.com/sites/default/themes/wappalyzer/images/installed.png)
