# SPA application challenges

By design Magento front-end can not be separated from the Magneto back-end. This is because it is rendered on the server side, so you need a complete Magento instance to render the HTML for the browser (client).

This aspect means that running in the high-loaded environment can be challenging. The resources needed to render the page are huge. To leverage the load, it is common to have multiple Magento instances serving the single purpose of rendering the HTML pages to the client.

The SPA is capable of rendering the page on its own. It only requires the data coming from server. This means, it enough to have just the static files (scripts and styles) (**and not the whole Magento!**) to render the HTML.

The multiple smaller servers (not Magento) serving the static files of the front-end only are caller headless servers.

### What does the headless mean?

However, for SEO purpuses we cannot return just the static files (scripts and styles) of the application. 

**Why?** Because crawlers are not browsing the SPA. They are reading the generated HTML and opening the found links in "new windows". This means our history manipulation is not relevant and is not working for crawlers. Each page is requested directly from the server. 

Therefore, we need to make sure the responses form the server (status codes) are correct. For example, if a page is not found, we should respond with 404, which is impossible to achieve without a server. The server returning just those static files and making sure the response codes are correct is is called the headless server (aka headless frond-end sever).

As stated above, the crawlers require the complete page HTML to parse the information inside. By design, SPA is not providing this HTML immediately. It needs to initialize scripts before content becomes available to the client. This means that crawlers are not able to parse any CSR page out-of-the-box. 

### How to make crawlers parse the CSR pages? 




 ## What is the difference between PWA-Studio and ScandiPWA?

PWA-Studio is made by Magento core team. They positions themselves as headless store-front for Magento. 
 