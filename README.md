![Project-logo](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/project-logo.png)
## Project title: Brazilian E-Commerce Sales & Inventory Optimization (ABC/XYZ Analysis)  
<center>Brazilian E-Commerce Sales & Inventory Optimization</center> 
<h2 style="text-align: center;">(ABC/XYZ Analysis)</h2> 
  
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
    
## Technology Stack  
  
**Tool:** Microsoft Excel / Google Sheets  
**Advanced Formulas:**  
* **IFS & IFERROR** for multi-level risk classification  
* **STDEV / AVERAGE** for Coefficient of Variation ($CV$) calculation.  
* **XLOOKUP** for relational data merging across multiple datasets.
* **Pivot tables** for data aggregation
* **Visualization:** Dashboard with KPI and charts.  
  
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
1. Download the archive with the project file  
[project.zip](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/blob/main/docs/project.zip)  
         
File location: https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/blob/main/docs/ 
      
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
    
**Name:** Andrii Isachenko  
**LinkedIn:** [Andrii Isachenko](https://www.linkedin.com/in/isachenko-andrii/)  
**E-mail:** isao.datastudio@gmail.com  
  
## Acknowledgments  
  
Thanks to [Olist](https://www.olist.com/) for providing this rich dataset for the data community.  
Special thanks to the [Kaggle](https://www.kaggle.com/) platform for hosting the data.  
Project Status: Completed. Planned future update: Adding RFM (Recency, Frequency, Monetary) analysis for customer segmentation.  
  
**License:** MIT License.

