==============================

FLEXIMART – FINAL SUBMISSION

==============================



--------------------------------

FILE 1: part3-datawarehouse/analytics\_queries.sql

--------------------------------



-- Query 1: Monthly Sales Drill-Down Analysis

SELECT

&nbsp;   d.year,

&nbsp;   d.quarter,

&nbsp;   d.month\_name,

&nbsp;   SUM(f.total\_amount) AS total\_sales,

&nbsp;   SUM(f.quantity\_sold) AS total\_quantity

FROM fact\_sales f

JOIN dim\_date d

&nbsp;   ON f.date\_key = d.date\_key

WHERE d.year = 2024==============================

FLEXIMART – FINAL SUBMISSION

==============================



--------------------------------

FILE 1: part3-datawarehouse/analytics\_queries.sql

--------------------------------



-- Query 1: Monthly Sales Drill-Down Analysis

SELECT

&nbsp;   d.year,

&nbsp;   d.quarter,

&nbsp;   d.month\_name,

&nbsp;   SUM(f.total\_amount) AS total\_sales,

&nbsp;   SUM(f.quantity\_sold) AS total\_quantity

FROM fact\_sales f

JOIN dim\_date d

&nbsp;   ON f.date\_key = d.date\_key

WHERE d.year = 2024

GROUP BY d.year, d.quarter, d.month, d.month\_name

ORDER BY d.year, d.quarter, d.month;





-- Query 2: Top 10 Products by Revenue

SELECT

&nbsp;   p.product\_name,

&nbsp;   p.category,

&nbsp;   SUM(f.quantity\_sold) AS units\_sold,

&nbsp;   SUM(f.total\_amount) AS revenue,

&nbsp;   ROUND(

&nbsp;       (SUM(f.total\_amount) /

&nbsp;       (SELECT SUM(total\_amount) FROM fact\_sales)) \* 100, 2

&nbsp;   ) AS revenue\_percentage

FROM fact\_sales f

JOIN dim\_product p

&nbsp;   ON f.product\_key = p.product\_key

GROUP BY p.product\_name, p.category

ORDER BY revenue DESC

LIMIT 10;





-- Query 3: Customer Segmentation Analysis

SELECT

&nbsp;   customer\_segment,

&nbsp;   COUNT(\*) AS customer\_count,

&nbsp;   SUM(total\_revenue) AS total\_revenue,

&nbsp;   ROUND(AVG(total\_revenue), 2) AS avg\_revenue\_per\_customer

FROM (

&nbsp;   SELECT

&nbsp;       c.customer\_key,

&nbsp;       SUM(f.total\_amount) AS total\_revenue,

&nbsp;       CASE

&nbsp;           WHEN SUM(f.total\_amount) > 50000 THEN 'High Value'

&nbsp;           WHEN SUM(f.total\_amount) BETWEEN 20000 AND 50000 THEN 'Medium Value'

&nbsp;           ELSE 'Low Value'

&nbsp;       END AS customer\_segment

&nbsp;   FROM fact\_sales f

&nbsp;   JOIN dim\_customer c

&nbsp;       ON f.customer\_key = c.customer\_key

&nbsp;   GROUP BY c.customer\_key

) t

GROUP BY customer\_segment

ORDER BY total\_revenue DESC;





--------------------------------

FILE 2: ROOT README.md

--------------------------------



\# FlexiMart Data Architecture Project



Student Name: Saral Anand  

Student ID: \[Your Student ID]  

Email: \[Your College Email]  

Course: Data for Artificial Intelligence  

Date: January 2026  



\## Project Overview



This project implements a complete data architecture for an e-commerce company (FlexiMart). It includes data ingestion from raw CSV files, data cleaning and transformation, relational and NoSQL database design, and analytical reporting using a data warehouse and OLAP queries.



The project demonstrates practical implementation of ETL pipelines, database normalization, NoSQL modeling, star schema design, and business analytics.



\## Repository Structure



fleximart-data-architecture/

│

├── data/

│   ├── customers\_raw.csv

│   ├── products\_raw.csv

│   └── sales\_raw.csv

│

├── part1-database-etl/

│   ├── etl\_pipeline.py

│   ├── schema\_documentation.md

│   ├── business\_queries.sql

│   ├── data\_quality\_report.txt

│   └── requirements.txt

│

├── part2-nosql/

│   ├── nosql\_analysis.md

│   ├── mongodb\_operations.js

│   └── products\_catalog.json

│

├── part3-datawarehouse/

│   ├── star\_schema\_design.md

│   ├── warehouse\_schema.sql

│   ├── warehouse\_data.sql

│   └── analytics\_queries.sql

│

└── README.md



\## Technologies Used



Python 3.x  

pandas, mysql-connector-python  

MySQL 8.0  

MongoDB 6.0  

SQL  



\## Setup Instructions



\### MySQL Setup



Create databases:

mysql -u root -p -e "CREATE DATABASE fleximart;"

mysql -u root -p -e "CREATE DATABASE fleximart\_dw;"



Run ETL pipeline:

python part1-database-etl/etl\_pipeline.py



Run business queries:

mysql -u root -p fleximart < part1-database-etl/business\_queries.sql



Run data warehouse scripts:

mysql -u root -p fleximart\_dw < part3-datawarehouse/warehouse\_schema.sql

mysql -u root -p fleximart\_dw < part3-datawarehouse/warehouse\_data.sql

mysql -u root -p fleximart\_dw < part3-datawarehouse/analytics\_queries.sql



\### MongoDB Setup



mongosh < part2-nosql/mongodb\_operations.js



Data was also imported and validated using MongoDB Compass.



\## Key Learnings



\- Built an end-to-end ETL pipeline using Python and MySQL  

\- Applied normalization and dimensional modeling concepts  

\- Compared relational and NoSQL databases for flexible data storage  

\- Implemented analytical reporting using OLAP queries  



\## Challenges Faced



1\. Handling inconsistent and missing data in raw CSV files, resolved through data cleaning logic in the ETL pipeline.  

2\. Managing schema and data separation in the data warehouse, resolved by maintaining separate schema and data SQL scripts.



\## Submission Notes



All scripts execute without errors.  

Data volumes and formats meet assignment requirements.  

Repository structure follows the provided guidelines.



--------------------------------

END OF FINAL SUBMISSION

--------------------------------



GROUP BY d.year, d.quarter, d.month, d.month\_name

ORDER BY d.year, d.quarter, d.month;





-- Query 2: Top 10 Products by Revenue

SELECT

&nbsp;   p.product\_name,

&nbsp;   p.category,

&nbsp;   SUM(f.quantity\_sold) AS units\_sold,

&nbsp;   SUM(f.total\_amount) AS revenue,

&nbsp;   ROUND(

&nbsp;       (SUM(f.total\_amount) /

&nbsp;       (SELECT SUM(total\_amount) FROM fact\_sales)) \* 100, 2

&nbsp;   ) AS revenue\_percentage

FROM fact\_sales f

JOIN dim\_product p

&nbsp;   ON f.product\_key = p.product\_key

GROUP BY p.product\_name, p.category

ORDER BY revenue DESC

LIMIT 10;





-- Query 3: Customer Segmentation Analysis

SELECT

&nbsp;   customer\_segment,

&nbsp;   COUNT(\*) AS customer\_count,

&nbsp;   SUM(total\_revenue) AS total\_revenue,

&nbsp;   ROUND(AVG(total\_revenue), 2) AS avg\_revenue\_per\_customer

FROM (

&nbsp;   SELECT

&nbsp;       c.customer\_key,

&nbsp;       SUM(f.total\_amount) AS total\_revenue,

&nbsp;       CASE

&nbsp;           WHEN SUM(f.total\_amount) > 50000 THEN 'High Value'

&nbsp;           WHEN SUM(f.total\_amount) BETWEEN 20000 AND 50000 THEN 'Medium Value'

&nbsp;           ELSE 'Low Value'

&nbsp;       END AS customer\_segment

&nbsp;   FROM fact\_sales f

&nbsp;   JOIN dim\_customer c

&nbsp;       ON f.customer\_key = c.customer\_key

&nbsp;   GROUP BY c.customer\_key

) t

GROUP BY customer\_segment

ORDER BY total\_revenue DESC;





--------------------------------

FILE 2: ROOT README.md

--------------------------------



\# FlexiMart Data Architecture Project



Student Name: Saral Anand  

Student ID:BITSoM\_BA\_2507562

Email: immortalss26@gmail.com

Course: Data for Artificial Intelligence  

Date: 5 January 2026  



\## Project Overview



This project implements a complete data architecture for an e-commerce company (FlexiMart). It includes data ingestion from raw CSV files, data cleaning and transformation, relational and NoSQL database design, and analytical reporting using a data warehouse and OLAP queries.



The project demonstrates practical implementation of ETL pipelines, database normalization, NoSQL modeling, star schema design, and business analytics.



\## Repository Structure



fleximart-data-architecture/

│

├── data/

│   ├── customers\_raw.csv

│   ├── products\_raw.csv

│   └── sales\_raw.csv

│

├── part1-database-etl/

│   ├── etl\_pipeline.py

│   ├── schema\_documentation.md

│   ├── business\_queries.sql

│   ├── data\_quality\_report.txt

│   └── requirements.txt

│

├── part2-nosql/

│   ├── nosql\_analysis.md

│   ├── mongodb\_operations.js

│   └── products\_catalog.json

│

├── part3-datawarehouse/

│   ├── star\_schema\_design.md

│   ├── warehouse\_schema.sql

│   ├── warehouse\_data.sql

│   └── analytics\_queries.sql

│

└── README.md



\## Technologies Used



Python 3.x  

pandas, mysql-connector-python  

MySQL 8.0  

MongoDB 6.0  

SQL  



\## Setup Instructions



\### MySQL Setup



Create databases:

mysql -u root -p -e "CREATE DATABASE fleximart;"

mysql -u root -p -e "CREATE DATABASE fleximart\_dw;"



Run ETL pipeline:

python part1-database-etl/etl\_pipeline.py



Run business queries:

mysql -u root -p fleximart < part1-database-etl/business\_queries.sql



Run data warehouse scripts:

mysql -u root -p fleximart\_dw < part3-datawarehouse/warehouse\_schema.sql

mysql -u root -p fleximart\_dw < part3-datawarehouse/warehouse\_data.sql

mysql -u root -p fleximart\_dw < part3-datawarehouse/analytics\_queries.sql



\### MongoDB Setup



mongosh < part2-nosql/mongodb\_operations.js



Data was also imported and validated using MongoDB Compass.



\## Key Learnings



\- Built an end-to-end ETL pipeline using Python and MySQL  

\- Applied normalization and dimensional modeling concepts  

\- Compared relational and NoSQL databases for flexible data storage  

\- Implemented analytical reporting using OLAP queries  



\## Challenges Faced



1\. Handling inconsistent and missing data in raw CSV files, resolved through data cleaning logic in the ETL pipeline.  

2\. Managing schema and data separation in the data warehouse, resolved by maintaining separate schema and data SQL scripts.



\## Submission Notes



All scripts execute without errors.  

Data volumes and formats meet assignment requirements.  

Repository structure follows the provided guidelines.



--------------------------------

END OF FINAL SUBMISSION

--------------------------------



