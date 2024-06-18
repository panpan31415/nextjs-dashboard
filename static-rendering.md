# what is static rendering?

data fetching and rendering happens on the server at build time (when you deploy) or during revalidation.
The result can then be distributed and cached in a Content Delivery Network (CDN).

Whenever a user visits your application, the cached result is served. There are a couple of benefits of static rendering:

- Faster Websites - Prerendered content can be cached and globally distributed. This ensures that users around the world can access your website's content more quickly and reliably.

- Reduced Server Load - Because the content is cached, your server does not have to dynamically generate content for each user request.

- SEO - Prerendered content is easier for search engine crawlers to index, as the content is already available when the page loads. This can lead to improved search engine rankings.

Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data which is regularly updated.


## what is revalidation? 
revalidation is the process of purging the Data Cache and re-fetching the latest data. This is useful when your data changes and you want to ensure you show the latest infomration.

chached data can be revalidated in two ways. 
### time based revalidation
    automaticlly revaidalte data after a certain amount of time
    has passed.
### on demand revalidation
    Manually revalidate data based on an event(e.g. form submission). On-demand revalidation can use tag-based or path based approach to revalidate groups of data at once.
### what is CDN
A CDN (Content Delivery Network) is a group of servers spread out over many locations. These servers store duplicate copies of data so that servers can fulfill data requests based on which servers are closest to the respective end-users. CDNs make for fast service less affected by high traffic.
