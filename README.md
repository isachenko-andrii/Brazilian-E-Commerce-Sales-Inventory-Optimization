![Project-logo](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/project-logo.png)
  
  <div align="center">  
    
## Brazilian E-Commerce Sales & Inventory Optimization<br>(ABC/XYZ Analysis)  
  
</div>
    
## Project description  
  
This project provides a data-driven approach to optimizing inventory and sales strategies for the Brazilian Olist e-commerce platform.  
By implementing a combined ABC/XYZ Analysis, we classify product categories based on their revenue contribution and demand stability.  
This helps businesses minimize "dead stock," avoid stockouts for "star" products, and optimize working capital.  

## Business Problem  
  
Managing over 70+ product categories requires a prioritized approach.  
The project answers three critical questions:  
  
• **Which products generate the most profit but are at risk of stockouts?**  
  
• **Which categories have erratic demand and should be managed "on-demand"?**  
  
• **Where can we reduce inventory to free up frozen capital?**  
  
## Data used  
  
The analysis uses open-source data from the Olist Store, the largest department store in Brazilian marketplaces.  
    • Source: [Kaggle (Brazilian E-Commerce Public Dataset by Olist)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
    • Sample size: 100,000+ orders from 2016 to 2018.  
    • Data composition: Relational structure including tables for orders, product items, product category translation, and timestamps.  

**Types of basic data:**  
  
<table>
  <thead>
    <tr>
      <th align="left">Column</th>
      <th align="left">Data type</th>
      <th align="left">Role in analysis</th>
      <th align="left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>order_id</b></td>
      <td><code>Text</code></td>
      <td>Identifier</td>
      <td>Unique order number. Used to count the number of transactions.</td>
    </tr>
    <tr>
      <td><b>product_id</b></td>
      <td><code>Text</code></td>
      <td>Identifier</td>
      <td>A unique product code for linking between relational tables.</td>
    </tr>
    <tr>
      <td><b>price</b></td>
      <td><code>Number</code></td>
      <td>Metrics (Revenue)</td>
      <td>Cost of goods. The basic indicator for calculating shares in <b>ABC analysis</b>.</td>
    </tr>
    <tr>
      <td><b>freight_value</b></td>
      <td><code>Number</code></td>
      <td>Metrics (Costs)</td>
      <td>Logistics (delivery) costs for each individual order item.</td>
    </tr>
    <tr>
      <td><b>Category_EN</b></td>
      <td><code>Text</code></td>
      <td>Dimension</td>
      <td>Category name in English. Basic aggregation level for <b>XYZ analysis</b>.</td>
    </tr>
    <tr>
      <td><b>Order_Date</b></td>
      <td><code>Datetime</code></td>
      <td>Time series</td>
      <td>Purchase date. Based on this, the demand stability (CV) is calculated by months.</td>
    </tr>
  </tbody>
</table>
    
## Technology Stack  
  
**Tool:** Microsoft Excel / Google Sheets  
**Advanced Formulas:**  
* **IFS & IFERROR** for multi-level risk classification  
* **STDEV.P / AVERAGE** for Coefficient of Variation ($CV$) calculation.  
* **XLOOKUP** for relational data merging across multiple datasets.
* **Pivot tables** for data aggregation
* **Visualization:** Dashboard with KPI and charts.  
  
**Recommended software:** Microsoft Excel 2021, Microsoft 365, or Google Sheets for full formula compatibility (XLOOKUP, IFS).  
  
## Methodology & Formula Logic
 
The project stands out for its robust handling of edge cases in demand forecasting:  
    
  **ABC Analysis (Revenue Contribution)**  
    
  **A-Class (80% Revenue):** High-priority drivers.  
  **B-Class (15% Revenue):** Stable contributors.  
  **C-Class (5% Revenue):** High-volume but low-value "long tail."   
     
  **XYZ Analysis (Demand Stability)**  
    
  We used the **Coefficient of Variation (CV)** to measure risk.  
  **Special Logic:** To ensure accuracy, we implemented a custom formula to handle single-sale  
  **anomalies ($CV=0$):**  
  =IFERROR(IFS(CV=0; "Z"; CV>0.8; "Z"; CV>0.4; "Y"; TRUE; "X"); "Z")  
    
  **X (CV ≤ 0.4):** Highly stable demand.  
  **Y (0.4 < CV ≤ 0.8):** Moderate volatility (seasonality/promotions).  
  **Z (CV > 0.8 or single sales):** Erratic/Unpredictable demand.  
  
## Key Insights & Results  
  
• **Revenue Concentration:** Group A represents only ~15% of categories but generates ~80% of total revenue ($6.97M).  
• **The "Star" Segment (AY):** Categories like health_beauty and computers_accessories are the backbone of the business—high revenue with manageable volatility.  
• **Risk Zone (AZ):** housewares and perfumery generate massive revenue but suffer from erratic spikes. They require a "Safety Stock" buffer of 25%+.  
• **The "Dead Stock" (CZ):** Identified categories with low revenue and zero predictability. Delisting these could free up approximately 15% of warehouse capacity.  
• **Seasonality:** Peak demand detected from May to July and a "Black Friday" spike in November.  
  
## Visualizations  

The project includes an interactive dashboard for strategic decision-making: 

**Revenue Concentration (Pareto)**  
  
![Pareto Chart](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Cover.png)  
      
**ABC/XYZ Strategic Matrix**    

![Pareto Chart](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/ABC-XYZ-analysis-matrix.png)  
        
**Category Dynamics & Seasonality**    
  
![Sales Dynamics](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Seasonality-of-leaders.png) 
    
## Project structure  
  
**Brazilian-E-Commerce-Sales-Inventory-Optimization**/ — project directory  
├── data/ — Project data  
│      ├── raw/ — Original Olist CSV files (orders, items, products)  
│      └── processed/ — Excel/Sheets file with master table  
├── docs/ — Methodology explanations and project.xlsx  
├── results/ — Screenshots of the Dashboard and final insights  
├── report/ — Report of project  
├── LICENSE — MIT License  
├── project-logo.png — Project cover  
└── README.md — Project documentation  
      
## How to Use  

To explore this analysis:  
1. To open the project file, follow the link:  
  
Version of the project using IFS & IFERROR and XLOOKUP  
For Microsoft Excel 2021, Microsoft 365, or Google Sheets for full formula compatibility  
https://docs.google.com/spreadsheets/d/1bSjTMzd_2ykpMQc9449ffet8W8dJv1Y3C8BU4SFKg9M/edit?usp=sharing  
  
For older versions (INDEX + MATCH used)  
https://docs.google.com/spreadsheets/d/1iRc6Vj5kr9cEDyhsMmvyFtzySWG2HWmPqqLPvuMe1vY/edit?usp=sharing  
  
**The project follows the international date standard ISO 8601 (YYYY-MM-DD), which is critical for the correct processing of data in input formulas.**  
  
2. Access the Dataset  
If you wish to see the raw data, download it from Kaggle:  
[Kaggle: Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
  
  or download CSV files from:  
File location: https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/tree/main/data/raw  
  
**olist_order_items_dataset.csv** - Main table with prices and ID  
**olist_products_dataset.csv** - Directory of products and categories    
**product_category_name_translation.csv** - Vocabulary: Portuguese -> English    
**olist_orders_dataset.csv** - Order dates      
  
## Contact  
    
**Name:** [Andrii Isachenko](https://isachenko-andrii.github.io)  
**LinkedIn:** [Andrii Isachenko](https://www.linkedin.com/in/isachenko-andrii/)  
**E-mail:** isao.datastudio@gmail.com  
  
## Acknowledgments  
  
Thanks to [Olist](https://www.olist.com/) for providing this rich dataset for the data community.  
Special thanks to the [Kaggle](https://www.kaggle.com/) platform for hosting the data.  
Project Status: Completed. Planned future update: Adding RFM (Recency, Frequency, Monetary) analysis for customer segmentation.  
  
**Project Status:** Completed.  
  
**License:** MIT License.  

