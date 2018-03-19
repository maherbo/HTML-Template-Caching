# HTML-Template-Caching
**UPDATE**:

This branch updates the original version by replacing the template loading via an IFRAME call with an AJAX call instead.  The advantage being that it is much, much faster, as there are no DOM builds with each IFRAME loading (which could be detrimental when you have IFRAMEs within IFRAMEs).

The IFRAME is still the «template» element, but it has no 'src' attribute.  The source file is stored in the 'data-src' attribute instead.  The - now empty - IFRAME is only necessary to fire up the 'onload' event.  Then, the template content is requested with an Ajax call, it is copied within a `<template>` element such that the document fragment is constructed, and the IFRAME template is replaced by the document fragment as before.

***
**ORIGINAL README**:

A demo on how to use IFRAMEs to cache automatically HTML templates, while fetching only dynamic data from the server.

This demo uses a very simple javascript function - setTemplate() - such that a server will only serve HTML templates or dynamic data, with separate requests.

The web page is a template by itself (main.html in our case).  The HTTP header for cache should be set such that it must revalidate every time to see if the website's logic has changed (identified by a 'website' version number perhaps).

The web page contains IFRAMEs which links to HTML templates that contains HTML document fragments (the page header or footer for example, which are often the same on every page).  These documents must be sent with a HTTP header for cache that states that the browser cached version will never go stale. The IFRAME 'src' attribute should contain a 'website' version number, which only need to be modified when changes are made server-side on the model or the view.

Other IFRAMEs can be used to fetch dynamic data.  These documents must be sent with a HTTP header for cache that states that the browser must not used a cached version and always request a fresh version.

After each IFRAME is loaded, the function setTemplate() replaces the IFRAME with the content of the file of its 'src' attribute.

Template and data IFRAMEs can be nested.

The demo also contains a style element and a function setEvents() to demonstrate how CSS and event listeners can be added to elements found in templates.

Once a page has been loaded, on subsequent requests of the same page, only the files with dynamic data are requested by the browser, which reduces the work load for the server and maybe the loading time as well for the user (unfortunately, IFRAME are elements that relatively take a long time to load).
