# PROBLEM STATEMENT ZEPTO
**Crate table zepto**?

ANS:-
CREATE TABLE zepto (
    Id primary key,
    Category VARCHAR(50),
    name VARCHAR(50),
    mrp INT,
    discountPercent INT(10),
    availableQuantity INT(10),
    discountedSellingPrice INT(10),
    weightInGms INT,
    outOfStock BOOLEAN,
    quantity INT
);

# Data exploration

**1) Total MRP Value**

select sum(mrp) from zepto;
 
**2) Total Discounted Sales Value**

SELECT
  SUM(discountedSellingPrice * quantity) AS Total_Discounted_Sales_Value
FROM zepto;
 

**3) Average Discount Percent**

select avg(discountpercent) from zepto; 
 

**4) Out-of-Stock Item Count**

select count(outofstock) from zepto;
 
**5) Total Quantity Available**

select sum(availableQuantity) from zepto;
 
# -- Data Analysis

**6) convert paise to rupees**

update zepto set mrp=mrp/100.0,
discountedsellingprice = discountedsellingprice /100.0;

 

**7) Find products with a discount of more than 20%**

select discountpercent from zepto where discountpercent > 20;
 	

**8) Calculate total available quantity in stock**
SELECT
  SUM(availableQuantity) AS Total_Available_Quantity
FROM zepto;
 

**9) List top 5 most expensive items by MRP**

select mrp from zepto order by mrp desc limit 5;
 

**10) Find the top 5 most expensive products based on their Maximum Retail Price (mrp)**

SELECT mrp FROM zepto
ORDER BY mrp DESC
LIMIT 5;
 
**11) List all products that are currently in stock**

SELECT *FROM zepto
WHERE outOfStock = FALSE;
 
**12) Get the number of unique products**

SELECT COUNT(DISTINCT name) AS unique_product_count
FROM zepto;
 

# Table 2: categories (manually defined)

CREATE TABLE category_info (
    Category VARCHAR(50),
    Department VARCHAR(50),
    Manager VARCHAR(50)
);
**How to insert categories table**

INSERT INTO category_info (Category, Department, Manager) VALUES
('Beverages', 'Grocery', 'Priya'),
('Snacks', 'Grocery', 'Raj'),
('Dairy', 'Perishables', 'Anjali'),
('Bakery', 'Perishables', 'Karan'),
('Fruits', 'Fresh Produce', 'Seema');

select * from categories;
 
**INNER JOIN – Get product info with its department and manager**

SELECT 
    z.name,
    z.Category,
    c.Department,
    c.Manager,
    z.mrp
FROM zepto z
JOIN category_info c
  ON z.Category = c.Category;

**LEFT JOIN – Show all products, even if category has no info in category_info**

SELECT 
    z.name,
    z.Category,
    c.Department,
    c.Manager
FROM zepto z
LEFT JOIN category_info c
  ON z.Category = c.Category;

**Aggregate JOIN – Total MRP per department**

SELECT 
    c.Department,
    SUM(z.mrp) AS total_mrp
FROM zepto z
JOIN category_info c
  ON z.Category = c.Category
GROUP BY c.Department;
JOIN with WHERE condition – High MRP items in 'Grocery
SELECT 
    z.name,
    z.mrp,
    c.Department
FROM zepto z
JOIN category_info c
  ON z.Category = c.Category
WHERE c.Department = 'Grocery'
