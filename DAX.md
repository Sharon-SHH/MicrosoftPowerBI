# DAX

**Calendar** (Date)

**Regions** (Sales Territory Key, Region, Country, Continent, Territory Manager, Email Address)

**Product Category** (Product Category Key, Product Category)

**Product Subcategory** (Product Subcategory Key, Sub Category, Product Category Key)

**Sales** (Transaction_Date, Stock_Date, Invoice_ID, Age_Group_Key, Customer_Gender_Key, Region_Key, Product_Category_Key, Sub_Category_Key, Product_Key, Quantity_Sold)

### Based on Sales

```sql
# Total Revenue
Total Revenue = 
SUMX(
    'Maven Cycles Sales',
    'Maven Cycles Sales'[Quantity_Sold] *
    RELATED(
        'Maven Cycles Products'[Unit Price]
    )
)
# Total Cost
Total Cost = 
SUMX(
    'Maven Cycles Sales',
    'Maven Cycles Sales'[Quantity_Sold] *
    RELATED(
        'Maven Cycles Products'[Unit Cost]
    )
)
# Total Order
Total Orders = 
DISTINCTCOUNT(
    'Maven Cycles Sales'[Invoice_ID]
)
# Quantity Sold
Quantity Sold = 
SUM(
    'Maven Cycles Sales'[Quantity_Sold]
)
# Quantity Sold (Stock Date)
Quantity Sold (Stock Date) = 
CALCULATE(
    [Quantity Sold],
    USERELATIONSHIP(
        'Maven Cycles Sales'[Stock_ Date],
        'Maven Cycles Calendar'[Date]
    )
)
# Profit Margin 
Profit Margin = 
DIVIDE(
    [Total Revenue] - [Total Cost],
    [Total Revenue],
    "N/A"
)

# profit
Profit = [Total Revenue] - [Total Cost]
# All Profit
ALL Profit = 
CALCULATE(
  [Profit],
  ALL(
   'Maven Cycles Sales'
  )
)
# % of profit
% of Profit = 
DIVIDE(
    [Profit],
    [ALL Profit]
)

```



