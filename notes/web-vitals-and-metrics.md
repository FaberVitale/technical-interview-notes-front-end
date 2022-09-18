# Web vitals aand metrics

## Metrics

### TTFB - Time to first byte

[TTFB](https://web.dev/ttfb/) is a metric that measures the time between the request for a resource and when the first byte of a response begins to arrive.
In other words how long it takes before we get the very first byte of a response from the server.

TTFB is the sum of the following request phases:

- Redirect time.
- Service worker startup time (if applicable).
- DNS lookup.
- Connection and TLS negotiation,
- server rendering, if any, up until the point at which the first byte of the response has arrived.

A good TTFB should be <= **0.8s**.

### FCP - First contentful paint

The [First Contentful Paint](https://web.dev/fcp/) (FCP) metric measures the time from when the page starts loading
to when any part of the page's content is rendered on the screen.

A good TTFB should be <= **1.8s**.


### LCP - Largest contentful paint

The [Largest Contentful Paint](https://web.dev/lcp/) (LCP) metric reports the render time of the **largest image or text block visible within the viewport**,
relative to when the page first started loading.

A good LCP should be <= **2.5s**.

### FID - First input delay

[FID](https://web.dev/fid/) measures the time from when a user first interacts with a page (i.e. when they click a link, tap on a button, or use a custom, JavaScript-powered control)
to the time when the browser is actually able to begin processing event handlers in response to that interaction.


### TTI - Time to interactive

[TTI](https://web.dev/tti/) how long it takes before the pages responds to the user interactions or 
more formally  measures the time from when the page starts loading to when its main sub-resources have loaded and it is capable of reliably 
responding to user input quickly.

### TBT - Total blocking time

[TBT](https://web.dev/tbt/), The Total Blocking Time metric measures the total amount of time between First Contentful Paint (FCP) and Time to Interactive (TTI) 
where the main thread was blocked for long enough to prevent input responsiveness.

### CLS - Cumulative layout shifts

[CLS](https://web.dev/cls/) - metric for measuring visual stability because it helps quantify 
how often users experience unexpected layout shifts.
