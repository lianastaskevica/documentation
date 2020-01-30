# Introduction to ScnadiPWA Tech Stack 

## How Magento 2 (M2) frontend (FE) works

The first time you open a page, browser caches all its **static** assets: scripts (JS), styles (CSS) and uses markdown (HTML) returned from the server to display the content of the page. The next time you visit the same website (e.g., going from product listing page (PLP) to product description page (PDP)) the browser fetches (loads) only HTML and reuses **browser** cached assets to display content. This means that to render the page (draw the content) it requires to request the HTML from a server. 

The HTML content is cached on the server. This means that for same page (e.g., PDP) the server will generate the HTML only once. Generating HTML on the server is called SSR (Server-side rendering). While generating, the server might use multiple entities - in database defined information sources (product information, user information, category, etc.). M2 is smart, it can **automatically** invalidate (purge, flush) specific HTML page caches on demand - when the entity information was changed (e.g., the product name was changed => related category and product page caches must be flushed). This mechanism is called "Full Page Cache". 

### What is the problem of such solution? 

Despite changing only one information entity (e.g., product name), the server will flush and after regenerate all HTML pages where this entity was used. This will make server load unchanged entities all over again even though they have not been changed. This makes M2 very "resource-heavy", it does a lot of unnecessary requests for unchanged entities. 

### How to make M2 not load unnecessary entities all over again? 

You must request the information about this entity separately. This cannot be done using solely HTML generated on the server because after it is cached the information cannot be separated. HTML is just a presentation of the entity information. We cannot find the exact place in the generated HTML where one or another entity was changed and invalidate exactly its part of markdown. This means that we cannot achieve effective caching by only implementing SSR even using the "Full Page Cache" mechanism. 

In order not to load the whole HTML all over again we must communicate with the server with the separate entities. Those entities can be presented in different formats, e.g. XML, JSON. To communicate by sharing the information (not presentation like HTML), the server must have any kind of API (Application Programming Interface). The API can be implemented in different ways, e.g. REST API (JSON), SOAP API (XML), GraphQL (JSON). 

The method of communication with the server with API is called AJAX (Asynchronous Javascript and XML). With the AJAX methodology the information is retrieved from the server, then passed to the algorithm on client (in browser), which generates the HTML. There could be multiple separate AJAX requests, e.g. product, category, user, etc. Each request can be separately cached on the server. This approach when done for all the data on the page is called Client-Side Rendering (CSR). 

### Can we implement CSR in M2?

Yes. Out of the box, Magento 2.3.x comes with partial GraphQL support + full REST API support. However, the default Magento theme is still mostly SSR. In places like checkout and cart, AJAX requests are used. They optimize and enhance the user experience on those pages. 

To implement full CSR, we need to completely rework the way how M2 approaches rendering. We must get rid of [layout / template system](). We need to implement a solution that will be capable of working in the browser (on client), make requests to M2 APIs, and render the information in human-readable format (in HTML). 


## How does ScnadiPWA implement CSR?

ScandiPWA does not support Magento layout / template system. Therefore, we need a substitution to it but in the client's browser. ScandiPWA uses React as a base for its FE because it is the most popular library for modern user interface (UI) development. React is a library which allows for a more effective page rendering. Instead of changing the whole page, React compares the expected representation of the page with the current one and applies the changes only to the exact part that was changed. 

As an API implementation ScandiPWA uses GraphQL. Firstly, GraphQL was initially chosen to be used by Magento themselves. Secondly, it is a development-friendly tool. Let me explain why. In its essence, GraphQL is a language that allows you to communicate with the server throughout only one endpoint, by pointing on such fields that you want the server to provide an information about. 

By rewriting (by implementing features present in) the M2 FE using the new technology stack like React and QraphQL as well as using the AJAX methodology, we can implement a CSR on the website. 


## Which benefits does PWA bring? 

PWA stands for Progressive Web Applications. PWA allows you to have one source code for all the platforms like web-browsers, Android and iOS applications, and PCs. This makes targeting new audience cheaper. Additionally, PWA solution brings you the ability of the offline browsing and the possibility to install the applicationg to your homepage directly from the browser. 
