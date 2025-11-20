Market Intelligence: 

Business Requirement:  

A government buyer typically selects products based on the best offer price available on the GeM 
platform for a given set of specifications. However, this process does not necessarily ensure the best 
market price for the product, as the prices listed on GeM are not validated against broader market 
trends or performance. 
To address this, market intelligence data for specific categories should be obtained and made available 
to buyers. This would enable them to compare GeM-listed prices with market rates and leverage the 
GeM platform more effectively to achieve price parity. Additionally, this data would assist in cases 
where GeM prices exceed market rates, helping buyers discover the most competitive prices. 
<img width="2019" height="1002" alt="image" src="https://github.com/user-attachments/assets/ac4db3e3-dae4-4e47-8fa6-58a7848b0e7d" />

Proposed solution: 

To enhance market intelligence, data from various e-marketplaces can be scraped using open-source 
Python libraries such as BeautifulSoup and Scrapy. These tools allow for efficient extraction of product 
listings, prices, and other relevant details from online platforms. By regularly scraping and updating 
market data, buyers can be empowered to make informed decisions by comparing GeM prices with real
time market trends. This automated approach will help identify price discrepancies and ensure better 
pricing accuracy within GeM. 

Solution Consumption:

Currently, this solution is integrated into the Product Display Page (PDP) of the GeM portal, providing 
buyers with actionable recommendations directly where they view product detail.

<img width="1181" height="686" alt="image" src="https://github.com/user-attachments/assets/14f55326-a979-4ae0-a2d5-5c83a1467ffd" />
<img width="1242" height="658" alt="image" src="https://github.com/user-attachments/assets/728cf2a8-5371-403b-b4b9-0c71824d3ae2" />

Following are the stakeholders and processes where this solution can have impact: 
• Buyer: The buyers will be able to access the competitive market values of similar products in 
other e-Marketplaces. This will help them to identify any product with better value in 
marketplace and whether the discovered prices are competitive or not in bids. 
• Sellers: The sellers get the intelligence to mark the price of their product to be reflective of the 
market (indirect) 
• GEM SPV: Will create competition among sellers and hence make the platform competitive 
among other e- Marketplaces with comparable listed prices. 

Data: 
To build this solution, required data consists of: 
• Input: Product Id and Category Id 
• Data is extracted from Google shopping, Google search, Amazon, Flipkart, Bing Search using 
scrapers (Python code). 

<img width="1293" height="1310" alt="image" src="https://github.com/user-attachments/assets/88c76299-c9d6-499b-ba9c-9830c788f5d4" />


Model Methodology:  

This methodology outlines the complete process of optimizing the search for relevant products across e
marketplaces using specific keywords, scraping data, and preprocessing it to extract meaningful insights 
for buyers and sellers on the GeM platform. The aim is to help buyers find competitive prices and 
identify non-conforming products.

<img width="1289" height="685" alt="image" src="https://github.com/user-attachments/assets/0c57ea60-cfa6-44ef-9131-f0c0e06a9d0a" />
<img width="1332" height="741" alt="image" src="https://github.com/user-attachments/assets/75aad622-5ed7-43ec-941e-0fd0a02ef1a9" />

Steps In Model: 

1. Creating Optimized Keywords for Product Search: 
• Goal: To create a precise and effective search string for product discovery on e-marketplaces 
like Amazon, Flipkart, and others. 
• Approach: Based on GeM data, important attributes such as make, model, and critical product 
specifications are extracted.
• Keyword Generation: After multiple rounds of experimentation, it was determined that a 
combination of the product’s make, model, and a few key specifications (such as capacity, 
features, or technical specifications) forms the most optimized keyword for product discovery 
on search engines and e-marketplaces. 
• Example: For a product like an air purifier, the keyword might look like: “Dyson air purifier 
model X, 300 sq ft, HEPA filter”.

2. Using the Keyword for Search on E-Marketplaces: 
• Once the optimized search string is created, it is used to query various e-marketplaces (such as 
Flipkart, Amazon, or Snapdeal) via web scraping tools. The Python libraries used for this process 
include: 
• BeautifulSoup: For HTML parsing and extracting information from web pages. 
• Scrapy: For large-scale data extraction from multiple pages in a structured manner. 
3. Scraping the Top 15 Relevant Products: 
• Goal: To limit the scope of scraping to the top 15 relevant products for each keyword search on 
e-marketplaces. 
• Reasoning: Based on extensive experimentation, the first 15 products on search results 
generally offer a good balance between relevance and diversity in pricing and features, which is 
critical for analysis. 
• Process: The solution scrapes product information like product title, price, brand, model, and 
specifications for the top 15 results, ensuring relevant comparison data from e-marketplaces. 
4. Pre-processing the Scraped Data: 
• Goal: To clean the raw scraped data and ensure it is ready for meaningful analysis. 
• Removing Noise: Some scraped data may contain irrelevant or misclassified products, duplicate 
listings, or incomplete information. Such data is filtered out through pre-processing steps. 
• Standardizing Product Information: Product data from different sources may have slight 
variations in format or terminology. These are standardized to ensure comparability. 
• Handling Missing Data: For any missing fields such as price or brand, imputation techniques are 
applied where possible, or the incomplete entries are discarded. 
5. Brand/Make Extraction: 
• Goal: To identify branded products within a category and focus on scraping data only for those 
products. Unbranded products are often not available or have inconsistent listings across e
marketplaces, making them unsuitable for comparison. 
6. Keyword Formation: 
• The identified brands are used in the search string to ensure that relevant and branded products 
are scraped. 
• Example: After extracting the brand Dyson for an air purifier product on GeM, the search string 
could be “Dyson air purifier model X” to find matching products on e-marketplaces.
7. Handling Non-Branded Products: 
• Goal: To focus on branded products where comparable data exists across multiple e
marketplaces. Products that are unbranded often do not have consistent listings and may lead 
to gaps in data. 
• Process: During scraping, the solution filters out non-branded or generic products, as their 
market data cannot be reliably compared across platforms. 
8. Using NLP (Fuzzy Wuzzy) to Find Similar Products: 
• Objective: Use Fuzzy Wuzzy, a powerful Natural Language Processing (NLP) technique, to 
identify and match similar products across different e-marketplaces, even when product names 
or descriptions differ slightly. 
• Fuzzy String Matching: When the scraped product names or descriptions from different e
marketplaces vary slightly due to inconsistencies in naming conventions or typographical 
differences, Fuzzy Wuzzy is used to find similar products based on their text similarity scores. 
• Implementation: The algorithm assigns a similarity score (from 0 to 100) based on the overlap of 
strings, allowing the system to compare and match products even when the names are not 
exactly the same. 
• Example: If GeM lists a product as "Dyson Air Purifier Model X", and an e-marketplace lists it as 
"Dyson Air Purifier - X Series", Fuzzy Wuzzy will calculate a high similarity score and match these 
products, enabling accurate price comparison. 
• Benefits: This technique helps improve product matching accuracy, especially in cases where 
product titles are slightly inconsistent across platforms. It ensures that all relevant products are 
included in the analysis, providing a more comprehensive view of market competitiveness. 
9. Data Consolidation and Price Analysis: 
• Once the clean and standardized data is collected, it is consolidated into a structured format (for 
further analysis. 
• Price Comparison: The consolidated data is analyzed to identify price differences between GeM
listed products and their counterparts on e-marketplaces. This helps to spot instances where the 
GeM price is higher than the market, allowing buyers to make informed decisions.

Business Value: 

1. Control High MRP & High Offer Prices Defined by Sellers: The solution directly addresses the issue of 
inflated Maximum Retail Prices (MRP) and high offer prices set by sellers on the GeM platform. By 
leveraging market intelligence data scraped from various e-marketplaces, the platform can compare 
sellers' listed prices with the broader market landscape. This will discourage sellers from setting 
unreasonably high MRPs and offer prices, knowing their pricing can now be benchmarked against 
market norms. Consequently, this promotes transparency and ensures fair pricing, which can drive 
more competitive and value-driven offers on the platform, benefiting both buyers and the platform 
itself.

2. Empower Buyers to Know the Right Price: The solution empowers government buyers with real-time 
access to market intelligence. With a clear comparison of product prices across multiple e
marketplaces, buyers can confidently assess whether the prices offered on GeM are competitive or 
inflated. This transparency in pricing helps buyers make more informed purchasing decisions, 
avoiding overpayment for products and optimizing procurement budgets. Empowered with data
driven insights, buyers can negotiate better deals and drive the selection of products that offer the 
best value for money.

4. Identify Non-Conforming Product Offerings Compared to the Market: By continuously monitoring 
market trends and prices from various e-marketplaces, the solution helps in identifying non
conforming or outlier product offerings on GeM. Sellers who offer products at prices significantly 
above market rates or who list products with mismatched specifications can be flagged. This 
identification process ensures that the platform maintains a high standard of product conformity 
and quality, reducing the risk of procurement inefficiencies caused by overpriced or subpar 
products. Ultimately, this will lead to a more trustworthy and competitive marketplace, ensuring 
that buyers are purchasing products that meet market standards in both price and quality.

Integration & API: Developed and integrated RESTful APIs using FlaskAPI 

Input: Solution requires GeM category name and product ID for which data has to be extracted. 

<img width="1277" height="811" alt="image" src="https://github.com/user-attachments/assets/4bc8c356-ed8b-4461-8bb8-41ec7f9efef2" />

Outcome: The data stored in database in below format, which includes external marketplace, date when data extracted, 
title of extracted product and its respective price. 

<img width="1230" height="180" alt="image" src="https://github.com/user-attachments/assets/360a58ab-0d74-45a0-a405-421959121f41" />


<img width="1339" height="461" alt="image" src="https://github.com/user-attachments/assets/0e542ce1-9aa2-49f0-9e28-f051360a80df" />


