# AEM - Magento Integration using Commerce Integration Framework FAQ

This document answers 17 questions about the Magento integration with AEM.

### 1. Is GraphQL only used for Magento or will this be available for querying content authored on AEMs JCR?

Adobe has adopted Magento’s GraphQL APIs as its official commerce API for all commerce related data. Hence, AEM uses GraphQL to exchange commerce data with Magento and later this year with any commerce engine via I/O Runtime. However, AEM intends to use GraphQL for querying in the future.

### 2. How does Adobe I/O come into play? Does AEM talk to Magento directly?

The AEM commerce connector connects to Magento GraphQL. Hence, AEM can directly connect to Magento without an I/O Runtime layer. If there is need to integrate additional third party solutions, the I/O Runtime platform can be used to host the mapping layer to connect the Magento GraphQL APIs to any third party solutions APIs.
The I/O Runtime platform can also be used to extend or customize commerce services. For this use-cases you would call the I/O Runtime endpoint that will then host a customized implementation of the respective service. Integration and extension use-cases can be combined.

### 3. Can Product assets (images) be stored and referenced from AEM via Magento admin? How can assets from Dynamic Media be consumed?

There isn't currently an AEM Assets – Magento integration. As a workaround, you can store product assets (images) in AEM Assets but you will have to manually store the asset URLs in Magento. Dynamic Media is now part of AEM Assets and will work the same way.

### 4. Does it matter where Magento is deployed? (On-prem or in the cloud)

It does not matter where Magento is deployed. The integration and the new AEM Venia store front will work regardless of the deployment model. However, if it is deployed based on the approved E2E reference architecture, E2E tests will be run against performance KPIs that were gathered that represent an enterprise customer’s profile. So, this will provide you with additional information that you can use as a benchmark.

### 5. How are catalog pages or product pages created in AEM? How do they persist in AEM?

This new integration does not need the classic CIF on-prem workflow to import product and create product pages in AEM. Catalog pages and product pages are created and cached dynamically in AEM based on generic catalog and product page templates. No Product or Catalog data is imported and stored in AEM.

### 6. Do you also cache pricing and other data via Dispatcher. Does that raise a frequent cache invalidation challenge?

Dynamic data such as price or inventory is not cached on the Dispatcher. Dynamic data is fetched client-side with web components directly via GraphQL APIs. Only static data (such as product or category data) is cached on the Dispatcher. If product data changes, there will be a need for cache invalidation.

### 7. Why are you not using We.Retail?

The Venia theme (developed by Magento) is used which is mobile first and aligned with Magento’s PWA. The Venia theme represents the latest in-terms of CSS styling and AEM core components.

### 8. When you update product data in Magento, is that a real-time push to AEM? Or is it a batch process?

A connector (AEM-CIF connector) was developed which enables data to flow from Magento to AEM on-demand. Hence, this is not a real-time push or a batch process when there is an update in Magento.

### 9. Is there any recommendation on unified search across AEM content with Commerce?

A product search reference implementation is provided but no unified search with content. This feature is usually very customer specific and better solved on a project-specific level.

### 10. How can product data be used in MSM or translations?

Product data is usually already translated in PIM or in Magento. The AEM – Magento Integration supports the connection to multiple Magento stores & store views. In an MSM setup typically one AEM site is linked to one Magento store view.

### 11. How does CIF work with other commerce platforms?

Integration with third party solutions such as other commerce solutions will be enabled later this year via the I/O Runtime platform. GraphQL support will be enabled on the I/O Runtime platform so that you can build a mapping layer (hosted on I/O Runtime) to map the GraphQL APIs to the third party solution’s APIs to build the integration.

### 12. Is there a way to enhance the product data with commercial text? Where do you do this? In AEM or in Magento?

This functionality is planned in early 2020 but can be developed on a project-level. There are multiple ways to achieve this and it will depend on the use case. One way would be to work with custom attributes. Allow AEM authors to mutate these fields in AEM’s product editor and synchronize the data back to the PIM. Another option would be leveraging AEM Experience Fragments which gets injected into the product pages.

### 13. Does the integration between AEM-Magento change when Adobe I/O Runtime platform is used?

Customers will not need to re-do the integration once GraphQL on I/O Runtime is available.
Customers who want to extend commerce services can use the same integration and write action sequences hosted on the I/O Runtime platform to inject business logic and enrich the commerce services.

### 14. With no products stored in AEM, how do you envision authors mapping images to a specific product?

You can store product assets (images) in AEM Assets but you will have to manually store the asset URLs in Magento. Authors will have access to a tagging feature later in 2019 so that they can tag assets with product or catalog to enable product specific asset search.

### 15. Since AEM creates product and catalog pages dynamically based on a generic template in AEM, what would I see if I were to open CRXDE Lite and check under content? Would I see an entire product tree based on the products in Magento? If not, how would an author enhance those pages?

There are no JCR catalog or product pages anymore. See question 12.

### 16. Will SPA store front work with AEM SPA editor?

AEM can be used as an authoring tool for any kind of store front. Currently, hybrid rendering is used for the new store front. In the future, AEM will be used for authoring with SPA and PWA.

### 17. How does PIM play into this framework?

PIM data gets exposed to AEM and clients via GraphQL requests.
