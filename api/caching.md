# Caching

Legislation.gov.uk receives an extremely large volume of traffic every day. To improve performance and serve content quickly and efficiently, we [cache](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching) the content we serve on legislation.gov.uk. A cache is a temporary store of frequently accessed data that can speed up repeated requests for the same data. We serve requests to legislation.gov.uk through a [content delivery network](https://en.wikipedia.org/wiki/Content_delivery_network), which is a set of servers around the world that each maintain their own local cache, so they can serve responses quickly to users nearby.

When a user requests a resource from legislation.gov.uk that is not already in the cache, our servers have to retrieve the resource from the database and transform it into the format requested by the user. This retrieval and transformation process is often slow and may consume significant server resources. 

When our API returns a response to the request, our content delivery network saves a copy of the response in the regional cache nearest to the user that made the request. The next time a user in the same region requests the same resource, we can serve the copy from the cache if it is fresh enough. As the cache already contains the requested content in the desired format, the content delivery network can serve the content much more quickly and efficiently than the API served the original request.

## Cache freshness and Time to Live (TTL)

On the website, a Time to Live (TTL) mechanism has been implemented which determines how long our content delivery network caches content before a check needs to be made for an updated version.

Currently we cache all pages on legislation.gov.uk for 1 hour, except the new legislation feeds under `/new/`, which we cache for 5 minutes. Newly published legislation does not exist in the cache until it is first requested.