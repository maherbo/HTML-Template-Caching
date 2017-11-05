# HTML-Template-Caching
A demo on how to use IFRAMEs to cache automatically HTML templates, while fetching only dynamic data from the server.

This demo uses a very simple javascript function - setTemplate() - such that a server will only serve HTML templates or dynamic data, with separate requests.

The web page is a template by itself (main.html in our case).  The HTTP header for cache should be set such it must revalidate every time to see if the website's logic has changed (identified by a 'website' version number perhaps).

The web page contains IFRAMEs which links to HTML templates that contains HTML document fragments (the page header or footer for example, which are often the same on every page).  These documents must be sent with a HTTP header for cache that states that the browser cached version will never go stale. The IFRAME 'src' attribute should contain a 'website' version number, which only need to be modified when changes are made server-side on the model or the view.

Other IFRAMEs can be used to fetch dynamic data.  These documents must be sent with a HTTP header for cache that states that the browser must not used a cached version and always request a fresh version.

After each IFRAME is loaded, the function setTemplate() replaces the IFRAME with the content of the file of its 'src' attribute.

Template and data IFRAMEs can be nested.

The demo also contains a style element and a function setEvents() to demonstrate how CSS and event listeners can be added to elements found in templates.

Once a page has been loaded, on subsequent requests of the same page, only the files with dynamic data are requested by the browser, which reduces the work load for the server and maybe the loading time as well for the user (unfortunately, IFRAME are elements that relatively take a long time to load).
