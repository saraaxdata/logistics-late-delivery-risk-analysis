# 🚚 Late Delivery Risk Analytics
Supply Chain Dataset | Power BI + DAX + Power Query | Ad-hoc analysis

<br>

## 📘 Project Overview
LogisticsCo faced hidden customer retention risk despite meeting revenue targets.

Conducted ad-hoc supply chain risk analysis on ~181K shipment records using **Power BI** to *surface operational blind spots, identifying customer concentration, geographic bottlenecks, and service tier failures* with $18M+ in at-risk revenue through risk-focused analytics framework.  
Built an interactive single-page Power BI dashboard transforming raw data into risk-focused KPIs that shifted leadership focus from volume to retention risk.


<img width="1439" height="803" alt="image" src="https://github.com/user-attachments/assets/4a771ab7-0b27-4a61-a849-c595ece58f97" />



## 💼 Business Problem

LogisticsCo is a nationwide logistics provider operating across multiple service tiers (Standard, First Class, Second Class, Same Day). In competitive shipping markets, protecting customer relationships is critical to sustainable growth.

> Despite strong revenue growth, LogisticsCo faces hidden SLA breach risk.
Standard KPI dashboards show "acceptable" aggregate performance (throughput up, revenue growing), but customer complaints are rising. Some consignees experience 80%+ late delivery rates, specific distribution hubs show systematic failures, and high-value accounts are experiencing repeated service failures—all masked by aggregate metrics.

The company needs actionable insights to identify which failures represent the greatest business risk and prioritize interventions based on shipper impact, not just shipment volume.

**Develop a risk-focused analytics framework that reframes standard logistics metrics to surface hidden operational and customer risk.**

<br>

## ❓ Business Questions
To guide the analysis, the project addresses the following questions:

1. What is the total revenue associated with late deliveries?
2. How does revenue per shipment compare between on-time and late deliveries?
3. What shipping service levels are mostly used by delays?
4. Which product categories experience the highest delay rates?
5. Are late deliveries concentrated in specific cities or regions?
6. Which customers experience the highest frequency of late deliveries?

<br>

## 💡 Key Findings
1. Systemic Performance Failure
     * 54.83% delay rate across 181K shipments
     * 99K shipments delivered late
     * Maximum delay: 4 days beyond scheduled delivery

2. Identified $18M at-risk revenue - 55% of total tied to failed operations.  The business generates more revenue from failed deliveries than successful ones. This creates a dangerous false signal—revenue dashboards look healthy while customer experience deteriorates.

3. Found critical bottleneck - 1 location  - Caguas with 37K failures (18x higher than others)

4.  Flagged retention risk - Top customer - Mary Smith with 13.2K repeat failures.These top customers represent concentrated revenue exposure. Losing Mary Smith alone would be catastrophic.

5. 41% of late deliveries uses Standard class.Premium services (First Class, Same Day) show relatively better performance, but Standard class with the highest volume is failing most frequently.  Are Standard class SLA commitments realistic, or are we over-promising to win price-sensitive customers?

6.  Top Categories with Late Deliveries:
     * Cleats: 13,500
     * Men's Footwear: 12,100
     * Women's Apparel: 11,500
     * Indoor/Outdoor Games: 10,600
     * Fishing: 9,500  
  Are these categories inherently harder to deliver (size, weight, packaging), or do they share common routes/carriers?

<br>

## ✅ Business Recommendations 

1.  Implement Priority Customer Recovery Protocol
    * Contact top 20 customers with highest late delivery frequency within 48 hours
    * Offer service credits, guaranteed delivery windows, or premium shipping upgrades

2. Launch immediate investigation into Caguas operations
    * Analyze routing efficiency and last-mile logistics
    * Review carrier contracts and performance in region

3.  Re-evaluate Second Class service commitments
     * Analyze whether current pricing supports reliable delivery
     * Segment customers by price sensitivity vs. delivery reliability preference
     * Consider extending delivery windows or repricing service

<br>


## 🛠️ Tools
* PowerBI - Dashboard development & data modeling
* PowerQuery - Data extraction & transformation
* DAX - Calculated measures & KPIs

<br>

## 📊 Dataset
  * Dataset: Kaggle [DataCo Supply Chain Dataset](https://www.kaggle.com/datasets/evilspirit05/datasupplychain) 
  * Records: ~181k shipment transactions, ~50 columns
  * Format: CSV
  * Type: Synthetic/academic dataset designed for supply chain ML analysis

<br>

## 🔄 Approach

1. PowerQuery
       *  Imported dataset from CSV
       *  Validated data types (dates, numerics, categories)
       *  Removed columns and filtered to relevant fields for analysis
       *  Created calculated columns
           ```powerquery
               customer_name = orders[customer_fname] & " "  & orders[customer_lname]
            ```
          ```powerquery
               delay_days = orders[actual_shipping_days]-orders[scheduled_shipping_days]
           ``` 
   

2. DAX measures
   ```dax
   Total Shipments = COUNT(orders[order_id])
   ```

   ```dax
   Total Revenue = SUM(orders[order_sales])
   ```

    ```dax
    Total Late Deliveries = CALCULATE([Total Shipments], orders[delivery_status]="Late delivery")
   ```

     ```dax
     Shipment Delay Rate % = DIVIDE( [Total Late Deliveries],  [Total Shipments],0)
   ```

      ```dax
      Revenue at Risk due to Delays = CALCULATE(SUM(orders[order_sales]),orders[delivery_status]= "Late delivery")
   ```

   ```dax
   Maximum Delivery Delay (Days) = CALCULATE( MAX(orders[delay_days]),orders[delivery_status]= "Late delivery")
   ```

 3. Dashboard Design
    * Generated KPIs
    * Grouped late deliveries by customer, city, product
    * Calculated revenue at risk
    * Assessed customer retention exposure
    * Enabled Date range slicer (Order Date: 2015-2018) and Country filter (Order Country)

<br>

## 🚀 Future Improvements 

1. Build classification model using Late_delivery_risk flag
2. Root Cause Analysis using weather, carrier, route datasets
3. Combine late delivery patterns with customer lifetime value and build churn risk prediction model
