# Caching

Legislation.gov.uk receives an extremely large volume of traffic every day. To improve performance and serve content quickly and efficiently, we _cache_ the content we serve on legislation.gov.uk using a [content delivery network](https://en.wikipedia.org/wiki/Content_delivery_network). A cache is a temporary store of frequently accessed data that can speed up repeated requests for the same data.

When a user requests a resource from legislation.gov.uk, our servers have to retrieve the resource from the database and transform it into the format requested by the user. This retrieval and transformation process is often slow and may consume significant server resources. 

When our API returns a response to the request, we save a copy of the response in the cache. The next time a user requests the same resource, we can serve the copy from the cache if it is fresh enough. As the cache already contains the requested content in the desired format, it can serve it much more quickly and efficiently than the API served the original request.

On the website, a Time to Live (TTL) mechanism has been implemented which determines how long the content can be cached before a check needs to be made for an updated version.

<!--TODO fill in details on TTL etc.-->

Newly published legislation does not exist in the cache and therefore is always up to date, as well as all related summary pages on the website such as http://www.legislation.gov.uk/new, http://www.legislation.gov.uk/new/ukpga, http://www.legislation.gov.uk/ukpga, etc. where the cache is purged. <!--TI 15/9/22: Not sure whether is this indeed the case? Also, which is the current caching strategy for publishing changes to existing legislation? Is the cache purged every time there is an update? -->