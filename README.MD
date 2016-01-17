About
-----
Unofficial iGoogle widget for Google Reader that works with Google Apps. Originally created around October 2008.

Background
----------
For the past few weeks, my RSS reader (Bloglines) has not been behaving. I started exploring Google Reader to see if it would fit my needs. One immediate issue I ran into is iGoogle support. I got used to this Bloglines notifier gadget for iGoogle that tells me when I have new items. BUT, the official Google Reader gadget seems not work under Google Apps (which I use) and the new canvas version fails in Firefox.

After a look at the Gadget API, I whipped up a very small hack for this problem. It is an iGoogle gadget which embeds the mobile version of Google Reader (which fits perfectly inside iGoogle). It is a very simple gadget with Content Type = url and is basically just a glorified iFrame. As long as you are logged into Google Reader, it should work. I tested it under Firefox 3 and Opera 9.5 under Ubuntu 8.

My initial goal was to make a notifier just like the Bloglines one, that simply shows how many unread items there are and a link to Google Reader. Unfortunatly, there is not official API, but there is an unofficial one which has been documented here [https://code.google.com/p/pyrfeed/wiki/GoogleReaderAPI]. There is an API call called "unread-count" which returns the exact data I needed in either XML and JSON. However, in order to obtain it, you must be logged into Google Reader.

Here is where I ran into cross domain security issues with Javascript. In order to get the XML output of that API call, my code needs to share the same domain as Google itself. There is no service that Google offers that can do that probably for the security reasons. Flash via crossdomain.xml isn't helpful either. Using a proxy wouldn't help since I do not have access to the cookies for Google Reader. And to top it off, the content on iGoogle is not served from a Google.com subomain.

So the next obvious step would be JSON. HOWEVER, the unofficial reader API does not offer ability to have a callback function for the JSON format. The raw JSON format is useless since the browser does not offer access to it via innerHTML, and it by itself is not parsed.

The next alternative after that would be to use the Gadget API Fetch functions to request the XML or JSON directly. HOWEVER, we run into the same cookie problem as before - they are served via a server side proxy which is not on the same domain. To get around that problem one could use the Account Authentication API which does return the correct tokens. BUT, the Gadget API's fetch functions do not support cookies which is the only way to use the security tokens once they have been obtained.

As a last alternative, I was planning on using the Fetch functions to do the account authentication and then a server side proxy via something like AppEngine or my own server, that can be passed the SID and then pass it on as a cookie. However, that would involve more time than necessary so I leave that exercise to the reader.

The end result is a hack that simply embeds the mobile version of Google Reader in iGoogle. It might not be very innovative but hey, it works.

Status
------
This project is no longer under active development.

Copyright
---------
Copyright (c) 2008-2015 Shaftek Enterprises.

Copyright (c) 2016- Impossible Dreams Network.

License
-------
Licensed under the Apache 2.0 License, see LICENSE
