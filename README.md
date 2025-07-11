# **📁 Retail Analytics Dashboard on Zepto Dataset using PostgreSQL, Excel, and Power BI**
## **📝 Project Description:**
#### 🃏The project focuses on analyzing a structured dataset from **Zepto**, a hyperlocal grocery delivery platform.
It involves performing **data cleaning, transformation, and visualization** to uncover insights across categories, pricing, 
discount strategies, and product performance.     
    
#### The process integrates SQL for **data exploration**, **Excel for data modeling**, and **Power BI** for **interactive dashboards**
to help understand business-critical **KPIs** like revenue distribution, stock status, discount optimization, and product-wise performance.

## **📄 Dataset Overview (Zepto Dataset)**
The dataset contains detailed information on products listed on Zepto, with the following key columns:

**🚏 Column_Name   |** ***🗺 Description***   
**💧 Category |**	  Product category (e.g., Beverages, Dairy, Fruits, etc.)    
**💧 name |**	    Product name    
**💧 mrp |**	        Maximum Retail Price    
**💧 discountPercent |**	    Discount applied on the product (in %)    
**💧 availableQuantity |**   	Number of units in stock    
**💧 discountedSellingPrice |**   	Actual selling price after discount   
**💧 weightInGms |**	            Weight of the product in grams    
**💧 outOfStock |**        	Boolean flag for stock status    
**💧 quantity |**	       Units sold or listed    

## **✅ Additional calculated fields used in analysis:**

**💧 Discount Amount**

**💧 Total Revenue**

**💧 Price per Gram**

**💧 MRP Category (High, Medium, Low)**

# **🧑‍💻 POSTGRESQL Query Process (Data Exploration & KPI Extraction)**
***PostgreSQL*** was used to query the dataset stored in a relational format. Here are sample tasks:

## **✅ Sample Queries:**

### **🟢 Beginner Level (1–5)**
#### **1 . View all product records ?**
SELECT *    
FROM Zepto;

#### **2. List all distinct product categories ?**
SELECT DISTINCT category     
FROM Zepto;

#### **3. Count total number of products ?**
SELECT COUNT(*) AS total_products      
FROM Zepto;

#### **4. Find total available quantity in stock ?**
SELECT SUM(available_quantity) AS total_stock      
FROM Zepto;

#### **5. Show products that are out of stock ?**
SELECT name
, category     
FROM Zepto   
WHERE out_of_stock = 'TRUE';


### **🟡 Intermediate Level (6–10)**
#### **6. Calculate total revenue (selling price × quantity) ?**
SELECT SUM(discounted_Selling_Price * quantity) AS total_revenue       
FROM Zepto        
WHERE out_of_stock = 'FALSE';

#### **7. Show top 5 highest MRP products ?**
SELECT DISTINCT Name
, MRP          
FROM Zepto        
ORDER BY MRP DESC       
LIMIT 5;

#### **8. Get average discount percentage per category ?**
SELECT category         
, ROUND(AVG(Discount_Percent),3) AS AVG_Discount         
FROM Zepto         
GROUP BY category;

#### **9. Show products with more than 30% discount ?**
SELECT Name
, discount_Percent    
FROM Zepto    
WHERE discount_Percent > 30;

#### **10. Count number of out-of-stock items per category ?**
SELECT category    
, COUNT(*) AS out_of_stock_count    
FROM Zepto   
WHERE out_of_stock = 'TRUE'    
GROUP BY category    
ORDER BY out_of_stock_count DESC;

### **🔵 Advanced Level (11–15)**
#### **11. Max in Weight_In_Gms per Category ?** 
SELECT category    
, Name   
, Weight_In_Gms   
FROM Zepto    
WHERE Weight_In_Gms = (SELECT MAX(Weight_In_Gms) FROM Zepto)

#### **12. List categories with more than 3 products ?**
SELECT category    
, COUNT(*) AS product_count   
FROM Zepto   
GROUP BY category    
HAVING COUNT(*) > 3      
ORDER BY product_count DESC;

#### **13. Rank products by discount percentage (highest first) ?**
SELECT Name    
, discount_Percent   
,
       RANK() OVER (ORDER BY discount_Percent DESC) AS rank_by_discount                      
FROM Zepto;

#### **14. Find the product(s) with the maximum available quantity ?**
SELECT Name   
, Available_quantity   
, Quantity    
FROM Zepto   
WHERE Available_quantity = (SELECT MAX(available_quantity) FROM Zepto)         
ORDER BY Quantity DESC;

#### **15. Group products into “High”, “Medium”, “Low” MRP buckets ?**
SELECT Name    
, MRP    
,
  CASE        
    WHEN MRP >= 4000 THEN 'High'      
    WHEN MRP BETWEEN 2000 AND 3999 THEN 'Medium'       
    ELSE 'Low'        
  END AS mrp_category        
FROM Zepto;

# **📊 Excel Process (PivotTables & Static Dashboard)**
## **✅ Excel Steps :**

### **1️⃣ Data Cleaning:**

**🀄️ Verified column data types**

**🀄️ Removed blanks, duplicates**

### **⏩ Created helper columns:**

**Discount Amount = mrp - discounted_Selling_Price**

**Total Revenue = discounted_Selling_Price * quantity**

**Price per Gram = discounted_Selling_Price / weight_In_Gms**

**MRP Category = IF(MRP>=4000, "High", IF(MRP>=2000, "Medium", "Low"))**

### **2️⃣ PivotTable Metrics:**

**Revenue by Category**

**Top Selling Products by Quantity**

**Quantity by Product**

**Out of Stock Count by Category**

**Category Wise Product count and Quantity**

**Revenue by MRP Category (High, Medium, Low)**

### **3️⃣ Charts & Visuals:**

**Stacked Bar Chart**

**Pie Chart**

**Stacked Column Chart**

## **💹 Excel Dashboard**
![Image](https://github.com/user-attachments/assets/a21c15a9-3a77-4983-a4a9-90f0881f57fc)

## **📢 Insights :**

#### ⏩ Premium categories (**Cooking Essentials, Munchies**) contribute the most to revenue.

#### ⏩ High number of **out-of-stock** items observed in fast-moving categories.

#### ⏩ 95%+ revenue generated from **High-MRP** products.

# **📈 Power BI Dashboard Process (Interactive & Dynamic Reporting)**
## **✅ Power BI Workflow :**

### **🪸  Data Modeling :**

Applied data types, formatting.

**Created DAX measures for:**

💧 Total Revenue

💧 Avg Discount %

💧 Out of Stock Count

💧Top Price per Gram

### **⛓️‍💥 Visuals Created :**

**🪭Bar Chart :** Total Revenue by Category

**🪭Pie Chart :** Revenue Share by MRP Category

**🪭Card KPIs :** Total Revenue, Quantity Sold, Avg Discount, Out of Stock

**🪭Table Visuals :** Top Products by Revenue, Highest Price per Gram

**🪭Stacked Columns :** Product Count vs Quantity Sold

### **⛓️‍💥 Slicers/Filters:**

**🪭Total Revenue**

**🪭Total Quantity**

**🪭Out-of-Stock Status**

**🪭Average of discount_Percent**

## **💹 Power BI Dashboard**
![Image](https://github.com/user-attachments/assets/4b101a90-87ed-4881-a0d1-f473937d6aa6)
![Image](https://github.com/user-attachments/assets/efa95437-fba6-496e-9c48-e7b95d708246)
![Image](https://github.com/user-attachments/assets/c3f11639-6c09-4afd-b582-866af4a6209d)
![Image](https://github.com/user-attachments/assets/b02d59d2-be47-4657-8078-b61e75370e87)

## **📢 Key Business Insights from Dashboard**
#### **🏆 Top Revenue Categories |**	Cooking Essentials, Munchies, and Chocolates generate highest revenue    
#### **❗ Inventory Alert |**	Over 3,700 items are marked out of stock — indicating missed sales
#### **📉 Discount Leverage |**	Categories with highest revenue also have heavy discounting — profitability risk
#### **🧊 High-Margin Products |**	Items like Saffron and Lip Balm generate ₹10,000+ per gram
#### **💡 Skewed Revenue |**	95% of revenue comes from high MRP products, emphasizing reliance on premium pricing
