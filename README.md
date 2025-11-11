# Customer-sales-insights-dashboard
Power BI dashboard for customer sales &amp; insights
### 📊 Overview  
An interactive **Power BI dashboard** that analyzes **customer sales, regional performance, and product categories** to uncover actionable business insights.  
The report visualizes **sales trends**, **active customer behavior**, and **discount-performance relationships**, helping decision-makers track KPIs easily.

---

### 🧰 Tools & Technologies  
- **Power BI Desktop** (May 2024 or later recommended)  
- **Data Source:** Excel / CSV (Customer, Sales, Product, and Date tables)  
- **DAX Calculations** for KPIs and visuals  
- **GitHub** for portfolio sharing  

---

### 📁 Repository Structure  
```
📦 customer-sales-insights-dashboard
 ┣ 📂 assets
 ┃ ┗ 📜 customer-sales-insights.png       → Dashboard screenshot
 ┣ 📂 data                               → Optional: sample data files (if shareable)
 ┣ 📜 Customer-Sales-Insights.pbix        → Power BI report file
 ┗ 📜 README.md                           → Project documentation
```

---

### 🧩 Data Model Overview  

#### **Tables**
- **Sales** — Sales transactions (SalesID, CustomerID, ProductID, SalesAmount, Discount, Quantity, Region, SalesDate, Tax, TotalAmount)
- **Customers** — Customer details (CustomerID, FullName, IsActive, CustomerType, Country, Region)
- **Products** — Product details (ProductID, Category, Price, SupplierName, StockQty)
- **DateTable** — Calendar table with Year, Month, Quarter, etc.

#### **Relationships**
- `Sales[CustomerID]` → `Customers[CustomerID]`  
- `Sales[ProductID]` → `Products[ProductID]`  
- `Sales[SalesDate]` → `DateTable[Date]`  

---

### 💡 Key Metrics (DAX Measures)

```DAX

Customer Count;=
CustomerCount = COUNT(Customers[CustomerID])

Active Customers :=
Active Customer = CALCULATE(
    DISTINCTCOUNT(Customers[CustomerID]),
    FILTER(
        ALL(Customers),
        Customers[IsActive] = TRUE()
            && Customers[CustomerID] IN VALUES(Sales[CustomerID])
    )
)

Active Non-Sale Customers :=
Non Sales Active Customer = CALCULATE(
    DISTINCTCOUNT(Customers[CustomerID]),
    FILTER(
        ALL(Customers),
        Customers[IsActive] = TRUE()
            && NOT(Customers[CustomerID] IN VALUES(Sales[CustomerID])
    )
))

DateTable :=
DateTable = 
ADDCOLUMNS (
    CALENDAR (MIN(Sales[SalesDate]), MAX(Sales[SalesDate])),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "MMM"),
    "Month Year", FORMAT([Date], "MMM YYYY"),
    "Quarter", "Q" & FORMAT([Date], "Q"),
    "Day", DAY([Date]
))

AverageProductRating :=
AverageProductRating = AVERAGE(Products[Rating])

```
---

### 📈 Key Insights  
✔️ **Top 5 Customers** drive major sales volume  
✔️ **Electronics category** leads total revenue share  
✔️ **West and Central regions** show strong sales consistency  
✔️ **Online and Wholesale channels** outperform Retail  
✔️ **Active customer ratio**: ~51% of total base  
✔️ **Discount-performance analysis** shows minimal correlation — suggesting optimized discount strategy potential  

---

### 🗺 Dashboard Preview  

<img width="769" height="397" alt="dashboard 2" src="https://github.com/user-attachments/assets/b8cf1b3a-85d3-4b97-9ddf-fa142ee5d9fc" />

---

### 🔍 How to View the Dashboard  
1. Download the `.pbix` file from this repository.  
2. Open it in **Power BI Desktop**.  
3. Refresh data (if connected to Excel/CSV) via **Home → Refresh**.  
4. Use slicers (Category, Region, Year) to interact and explore insights.

---

### 🚀 Future Enhancements  
- Add **forecasting & trend analysis**  
- Introduce **RFM segmentation** for customer loyalty insights  
- Connect to **SQL Server / API** for real-time refresh  
- Deploy to **Power BI Service** with auto-refresh  

---

### ✨ About the Creator  
👩‍💻 **Anshika Agarwal**  
Data Analyst skilled in Power BI, Python, SQL, and Excel — passionate about turning data into meaningful stories.  

