![Project-logo](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/project-logo.png)
#### [EN](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/blob/main/README.md) | [UA](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/blob/main/README-UA.md) Цей матеріал також доступний англійською мовою.
---  
  
  <div align="center">  
    
## Оптимізація продажів та складу Brazilian E-Commerce<br>(ABC/XYZ Analysis)  
  
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
      <th align="left">Колонка</th>
      <th align="left">Тип даних</th>
      <th align="left">Роль в аналізі</th>
      <th align="left">Опис</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>order_id</b></td>
      <td><code>Text</code></td>
      <td>Ідентифікатор</td>
      <td>Унікальний номер замовлення. Використовується для підрахунку кількості транзакцій.</td>
    </tr>
    <tr>
      <td><b>product_id</b></td>
      <td><code>Text</code></td>
      <td>Ідентифікатор</td>
      <td>Унікальний код продукту для зв'язування між реляційними таблицями.</td>
    </tr>
    <tr>
      <td><b>price</b></td>
      <td><code>Number</code></td>
      <td>Метрика (Дохід)</td>
      <td>Вартість товарів. Основний показник для розрахунку часток в ABC-аналізі</b>.</td>
    </tr>
    <tr>
      <td><b>freight_value</b></td>
      <td><code>Number</code></td>
      <td>Метрика (Витрати)</td>
      <td>Логістичні (доставкові) витрати для кожного окремого товару замовлення.</td>
    </tr>
    <tr>
      <td><b>Category_EN</b></td>
      <td><code>Text</code></td>
      <td>Вимір</td>
      <td>Назва категорії англійською мовою. Базовий рівень агрегації для XYZ-аналізу</b>.</td>
    </tr>
    <tr>
      <td><b>Order_Date</b></td>
      <td><code>Datetime</code></td>
      <td>Часові ряди</td>
      <td>Дата покупки. На основі цього розраховується стабільність попиту (CV) по місяцях.</td>
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
    
  **A-Class (80% Revenue):** Товари з високим пріоритетом.  
  **B-Class (15% Revenue):** Стабільні учасники.  
  **C-Class (5% Revenue):** High-volume but low-value "long tail."   
     
**XYZ-аналіз (стабільність попиту)**  
  
Ми використовували **коефіцієнт варіації (CV)** для вимірювання ризику.  
**Спеціальна логіка:** Для забезпечення точності ми впровадили власну формулу для обробки одиничних продажів.  
**аномалій ($CV=0$):**  
=IFERROR(IFS(CV=0; "Z"; CV>0.8; "Z"; CV>0.4; "Y"; TRUE; "X"); "Z")  
  
**X (CV ≤ 0.4):** Дуже стабільний попит.  
**Y (0.4 < CV ≤ 0.8):** Помірна волатильність (сезонність/акції).  
**Z (CV > 0.8 або одиничні продажі):** Нестабільний/непередбачуваний попит.  
    
## Ключові висновки та результати  
  
• **Концентрація доходів:** Група A представляє лише ~15% категорій, але генерує ~80% загального доходу (6,97 млн ​​доларів США).  
• **Сегмент «Зірка» (AY):** Такі категорії, як здоров'я та краса, а також комп'ютерні аксесуари, є основою бізнесу — високий дохід з керованою волатильністю.  
• **Зона ризику (AZ):** Товари для дому та парфумерія генерують величезний дохід, але страждають від нестабільних стрибків. Вони потребують буфера «страхового запасу» на рівні 25%+.  
• **«Мертвий запас» (CZ):** Визначені категорії з низьким доходом та нульовою передбачуваністю. Виключення їх зі списку може звільнити приблизно 15% складських потужностей.  
• **Сезонність:** Піковий попит спостерігається з травня по липень, а сплеск «Чорної п'ятниці» — у листопаді.  
  
## Візуалізації  
  
Проєкт включає інтерактивний дашборд для прийняття стратегічних рішень: 
  
**Стратегічна панель керування продажами Olis**  
  
![Pareto Chart](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Cover.png)  
      
**Стратегічна матриця ABC/XYZ**    

![Pareto Chart](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/ABC-XYZ-analysis-matrix.png)  
        
**Динаміка категорій та сезонність**    
  
![Sales Dynamics](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Seasonality-of-leaders.png) 

**Концентрація доходу (Парето)**  
  
![Pareto](https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/raw/main/results/Pareto-analysis.png)  
    
## Структура проекту  
  
**Brazilian-E-Commerce-Sales-Inventory-Optimization**/ — Каталог проекту   
├── data/ — Дані проєкту  
│      ├── raw/ — Оригінальні CSV-файли Olist (замовлення, товари, продукти)  
│      └── processed/ — Excel/Sheets файли з головною таблицею  
├── docs/ — Пояснення методології та посилання на project.xlsx  
├── results/ — Знімки екрана панелі інструментів та остаточні висновки  
├── report/ — Звіт про проект  
├── LICENSE — MIT License  
├── project-logo.png — Обкладинка проекту    
└── README.md — Проектна документація  
      
## Як використовувати  
  
Щоб ознайомитися з цим аналізом:  
  
1. Щоб відкрити файл проєкту, перейдіть за посиланням:  
  
Версія проєкту з використанням IFS & IFERROR та XLOOKUP  
Для Microsoft Excel 2021, Microsoft 365 або Google Sheets для повної сумісності з формулами  
https://docs.google.com/spreadsheets/d/1bSjTMzd_2ykpMQc9449ffet8W8dJv1Y3C8BU4SFKg9M/edit?usp=sharing  
  
Для старіших версій (використовується INDEX + MATCH)  
https://docs.google.com/spreadsheets/d/1iRc6Vj5kr9cEDyhsMmvyFtzySWG2HWmPqqLPvuMe1vY/edit?usp=sharing  
  
**Проєкт відповідає міжнародному стандарту дати ISO 8601 (РРРР-ММ-ДД), який є критично важливим для правильної обробки даних у вхідних формулах.**   
  
2. Отримайте доступ до Набір даних  
Якщо ви хочете переглянути необроблені дані, завантажте їх з Kaggle:  
[Kaggle: Бразильський публічний набір даних електронної комерції](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
  
або завантажте файли CSV з:  
Розташування файлу: https://github.com/isachenko-andrii/Brazilian-E-Commerce-Sales-Inventory-Optimization/tree/main/data/raw  
  
**olist_order_items_dataset.csv** - Головна таблиця з цінами та ідентифікатором  
**olist_products_dataset.csv** - Каталог товарів та категорій  
**product_category_name_translation.csv** - Словник: Португальська -> Англійська  
**olist_orders_dataset.csv** - Дати замовлення   
    
## Контакти  
    
**Автор:** [Andrii Isachenko](https://isachenko-andrii.github.io)  
**Посада:** Junior Data Analyst  
**LinkedIn:** [Andrii Isachenko](https://www.linkedin.com/in/isachenko-andrii/)  
**E-mail:** andrii.isachenko@gmail.com  
  
## Подяки  
  
Дякую [Olist](https://www.olist.com/) за надання цього багатого набору даних.  
Особлива подяка платформі [Kaggle](https://www.kaggle.com/) за надання даних.  
  
**Статус проекту:** Завершено.  
  
**Ліцензія:** MIT License.  

