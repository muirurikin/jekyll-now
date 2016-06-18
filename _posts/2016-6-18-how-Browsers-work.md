---
layout: post
title: How Browsers Work
---

#how-Browsers-Work
A browser has a UI (user interface) that most commonly includes an address bar, back/forward button, and reload button. Sometimes developers refer to this as the “chrome” (little “c”, not Chrome by Google) of a browser. When you navigate to a URL in the address bar you are making a “request” for the content at that URL.

That URL you typed into the address bar maps to an IP address. This is called a DNS lookup. DNS stands for “Domain Name System” and it maps numeric computer addresses to human readable names. All computers have an IP addres

Once the browser has the IP address it sends an HTTP request to the web server at that address. HTTP stands for “Hypertext Transfer Protocol” and is used to facilitate requests from your client (the browser) and responses from the server. In our case the response is HTML from the web server at www.google.com.

As this HTML response is being sent to your browser, the browser’s rendering engine is displaying the requested content on your screen. To accomplish this the rendering engine “parses” the HTML and creates a DOM tree.The browser then parses style data (CSS or inline styles) and together with the HTML it constructs a render tree. The render tree displays rectangles (that represent divs, paragraphs, headlines, etc.) with a few visual attributes such as color and size dimensions. These rectangles are displayed in order on the page. Next, the browser lays out the contents in the position they will appear in the browser. The last step is “painting” where the elements are drawn on the screen.
