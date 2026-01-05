# NoSQL Database Analysis – FlexiMart

## Section A: Limitations of Relational Databases (RDBMS)

Relational databases like MySQL work well for structured and fixed-schema data, but they face limitations when handling highly diverse product information. In an e-commerce platform like FlexiMart, different products require different attributes. For example, laptops need specifications such as RAM, processor, and storage, while shoes require size, color, and material. Representing such variability in an RDBMS often results in many nullable columns or multiple tables, which increases complexity.

Frequent schema changes are another challenge. Adding new product types usually requires altering table structures, which can be time-consuming and risky in production systems. This reduces flexibility and slows down development. Additionally, storing nested data such as customer reviews is inefficient in relational databases because reviews must be stored in separate tables and accessed using joins, increasing query complexity and reducing performance.

## Section B: Benefits of MongoDB for Product Catalog

MongoDB addresses these problems using a flexible, document-based data model. Each product can store only the attributes relevant to it, making MongoDB suitable for handling diverse product categories within the same collection.

MongoDB also allows embedded documents, which makes it possible to store customer reviews directly inside product documents. This improves read performance and simplifies data retrieval because product details and reviews can be fetched in a single query. Furthermore, MongoDB supports horizontal scalability through sharding , allowing data to be distributed across multiple servers. This makes it suitable for large-scale e-commerce platforms with growing product catalogs.

## Section C: Trade-offs of Using MongoDB

Despite its flexibility, MongoDB has certain disadvantages. It does not enforce strong relational constraints such as foreign keys, which can lead to data inconsistency if not handled properly at the application level. Additionally, MongoDB is less suitable for complex transactional systems that require strict ACID compliance across multiple entities. In such scenarios, relational databases like MySQL provide better reliability.
