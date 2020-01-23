# Introduction to ScnadiPWA Tech Stack 

## How Magento 2 (M2) frontend (FE) works

The first time you open a page, browser caches all its **static** assets: scripts (JS), styles (CSS) and uses markdown (HTML) returned from server to display the content of the page. The next time you visit the same website (e.g., going from product listing page (PLP) to product description page (PDP)) the browser fetches (loads) only HTML and reuses **browser** cached assets to display content. This means that in order to render the page (draw the content) it requires to request the HTML from server. 

The HTML content is cached on the server. This means that for same page (e.g., PDP) the server will generate the HTML only once. Generating HTML on server is called SSR (Server-side rendering). While generating, the server might use multiple entities - in database defined information sources (product information, user information, category, etc.). M2 is smart, it can **automatically** invalidate (purge, flush) specific HTML page caches on demand - when the entity information was changed (e.g., product name was changed => related category and product page caches must be flushed). This mechanism is called "Full Page Cache". 

What is the problem of such solution? 

Despite changing only one information entity (e.g., product name), the server will flush and after regenerate all HTML pages where this entity was used. This will make server load unchanged entities all over again even though they have not been changed. This makes M2 very "resource-heavy", it does a lot of unnecessary requests for unchanged entities. 

How to make M2 not load unnecessary entities all over again? 

You must request the information about this entity separately. This cannot be done using only HTML generated on server because after it is cached the information cannot be separated. HTML is just a presentation of the entity information. We cannot find the exact place in the generated HTML where one or another entity was changed and invalidate exactly its part of markdown. This means that we cannot achieve effective caching by only implementing SSR even using the "Full Page Cache" mechanism. 

<!-- To be continued... -->

Any sorts of AJAX requests (REST API, GraphQL) solves this issue by sharding (separating) entities from each other. This way M2 only invalidates and regenerates the responses related to changed entity (not loading the unchanged ones). This is why requesting information on a page is more effective than 

> **Problem**: Each time a new page is loaded Magento loads all neccessary scripts and assets (resources) for it. Also, the animation between pages is impossible. This is because Magento is by definition server side rendered (**SSR**). 

The ScnadiPWA is client-side rendered. What does it mean? 

1. We do not load page each time you transition between them. This means that all assets and scripts are loaded only once during the first page visit. 

> **Problem**: If the page static assets (CSS, JS) are loaded only once, how can we implement the mechanism of invalidating them? E.g., if the JS logic has been changed, how can we update the assets on the page? 

Magento has a built-in mechanism for that - static content versioning. This allows browsers to 