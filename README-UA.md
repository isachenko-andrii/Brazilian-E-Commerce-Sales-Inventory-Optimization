![Project-logo](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/project-logo.png)
#### [EN](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/blob/main/README.md) | [UA](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/blob/main/README-UA.md) Цей матеріал також доступний англійською мовою.
---  
  
  <div align="center">  
    
## Brazilian E-Commerce Sales & Inventory Optimization<br>(ABC/XYZ Analysis)  
  
</div>
    
## Опис проекту  
  
Цей проєкт пропонує підхід, заснований на даних, до оптимізації стратегій запасів та продажів для бразильської платформи електронної комерції Olist. Впроваджуючи комбінований ABC/XYZ-аналіз, ми класифікуємо категорії продуктів на основі їхнього внеску в дохід та стабільності попиту. Це допомагає компаніям мінімізувати «мертві запаси», уникати дефіциту «зіркових» продуктів та оптимізувати оборотний капітал.  

## Бізнес-проблема  
  
Управління понад 70 категоріями продуктів вимагає пріоритетного підходу. Проєкт відповідає на три критичні питання:  
  
• **Які товари приносять найбільший прибуток, але ризикують призвести до дефіциту?**  
  
• **Які категорії мають нестабільний попит і повинні керуватися «на вимогу»?**  
  
• **Де ми можемо зменшити запаси, щоб звільнити заморожений капітал?**  
  
## Використані дані  
  
В аналізі використовуються відкриті дані з Olist Store, найбільшого універмагу на бразильських торгових майданчиках.  
    • Джерело: [Kaggle (Brazilian E-Commerce Public Dataset by Olist)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
    • Розмір вибірки: Понад 100 000 замовлень з 2016 по 2018 рік.  
    • Композиція даних: реляційна структура, включаючи таблиці замовлень, товарних позицій, категорій товарів та часових позначок.  

**Типи даних:**  
  
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
    
## Технологічний стек  
  
**Інструменти:** Microsoft Excel / Google Sheets  
**Використані формули:**  
* **IFS & IFERROR** для багаторівневої класифікації ризиків.  
* **STDEV.P / AVERAGE** для розрахунку коефіцієнта варіації (CV).  
* **XLOOKUP** для об'єднання реляційних даних між кількома наборами даних.
* **Pivot tables** для агрегації даних.
* **Visualization:** інформаційна панель з ключовими показниками ефективності (KPI) та діаграмами.  
  
**Рекомендоване програмне забезпечення:** Microsoft Excel 2021, Microsoft 365, або Google Sheets для повної сумісності формул (XLOOKUP, IFS).  
  
## Методологія та логіка формул
 
Проєкт вирізняється надійною обробкою граничних випадків у прогнозуванні попиту:  
    
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
  
## Ключові висновки та результати  
  
• **Revenue Concentration:** Group A represents only ~15% of categories but generates ~80% of total revenue ($6.97M).  
• **The "Star" Segment (AY):** Categories like health_beauty and computers_accessories are the backbone of the business—high revenue with manageable volatility.  
• **Risk Zone (AZ):** housewares and perfumery generate massive revenue but suffer from erratic spikes. They require a "Safety Stock" buffer of 25%+.  
• **The "Dead Stock" (CZ):** Identified categories with low revenue and zero predictability. Delisting these could free up approximately 15% of warehouse capacity.  
• **Seasonality:** Peak demand detected from May to July and a "Black Friday" spike in November.  
  
## Візуалізації  

Проєкт включає інтерактивний дашборд для прийняття стратегічних рішень: 

**Olis Sales Strategic Dashboard**  
  
![Pareto Chart](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Cover.png)  
      
**ABC/XYZ Strategic Matrix**    

![Pareto Chart](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/ABC-XYZ-analysis-matrix.png)  
        
**Category Dynamics & Seasonality**    
  
![Sales Dynamics](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Seasonality-of-leaders.png) 

**Revenue Concentration (Pareto)**  
  
![Pareto](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Pareto-analysis.png)  
    
## Структура проекту  
  
**Brazilian-E-Commerce-Sales-Inventory-Optimization**/ — Каталог проекту   
├── data/ — Дані проєкту  
│      ├── raw/ — Оригінальні CSV-файли Olist (замовлення, товари, продукти)  
│      └── processed/ — Excel/Sheets файли з головною таблицею  
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
Розташування файлу: https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/tree/main/data/raw  
  
**olist_order_items_dataset.csv** - Main table with prices and ID  
**olist_products_dataset.csv** - Directory of products and categories    
**product_category_name_translation.csv** - Vocabulary: Portuguese -> English    
**olist_orders_dataset.csv** - Order dates      
  
## Контакти  
    
**Ім'я:** [Andrii Isachenko](https://isachenko-andrii.github.io)  
**LinkedIn:** [Andrii Isachenko](https://www.linkedin.com/in/isachenko-andrii/)  
**E-mail:** isao.datastudio@gmail.com  
  
## Подяки  
  
Дякую [Olist](https://www.olist.com/) за надання цього багатого набору даних.  
Особлива подяка платформі [Kaggle](https://www.kaggle.com/) за надання даних.  
  
**Статус проекту:** Завершено.  
  
***Ліцензія:** MIT License.  

