# MaterialRequirementPlanning-optimization

Project Overview

This project develops a Material Requirement Planning (MRP) and procurement optimization model using Python. The model calculates material requirements based on production plans and the Bill of Materials (BOM), considers current inventory and safety stock, calculates EOQ, and optimizes supplier allocation based on cost, lead time, MOQ, and supplier capacity.

Objectives
Calculate gross material requirements from production plans and BOM.
Calculate safety stock and net material requirements.
Identify materials requiring procurement.
Calculate Economic Order Quantity (EOQ).
Compare EOQ-based ordering cost with a single-order approach.
Identify suppliers that can meet the required lead time.
Optimize procurement quantities across suppliers.
Consider supplier MOQ and maximum capacity constraints.
Identify materials with unmet requirements.
Methodology
1. Material Requirement Calculation

The production plan is combined with the BOM to calculate the gross requirement of each material.

Gross Material Requirement = Quantity per Unit × Planned Production Quantity

The gross requirements are then aggregated by material.

2. Inventory and Safety Stock

Current inventory is combined with gross material requirements.

Safety stock is calculated as:

Safety Stock = Safety Stock % × Current Stock

The net material requirement is calculated as:

Net Requirement = Safety Stock + Gross Requirement − Current Stock

Negative requirements are set to zero.

3. Lead-Time Analysis

The earliest due date for each material is identified from the production plan.

The available time for procurement is calculated as:

Days Available = Earliest Due Date − Project Reference Date

Suppliers are considered feasible only when:

Supplier Lead Time ≤ Days Available

4. EOQ Analysis

Economic Order Quantity is calculated using:

EOQ = √(2DS / H)

Where:

D = Material demand
S = Ordering cost per order
H = Holding cost per unit

The project calculates EOQ-based ordering cost, single-order cost, and estimated savings.

5. Supplier Optimization

The project uses PuLP and Linear Programming to minimize total procurement cost.

The optimization considers:

Material requirements
Supplier price
Supplier MOQ
Supplier maximum capacity
Supplier lead time

The objective is:

Minimize Total Procurement Cost = Σ(Order Quantity × Supplier Price)

The model also identifies materials where procurement is not feasible because of lead-time or MOQ/capacity constraints.

Project Workflow
Production Plan
       ↓
      BOM
       ↓
Gross Material Requirement
       ↓
Current Inventory + Safety Stock
       ↓
Net Material Requirement
       ↓
Lead-Time Feasibility
       ↓
Supplier Selection
       ↓
MOQ & Capacity Constraints
       ↓
Linear Programming Optimization
       ↓
Optimized Procurement Plan
Dataset Files
production_plans.xlsx – Planned production quantities and due dates.
bom1.xlsx – Bill of Materials and material quantities required per product.
inventory1.xlsx – Current inventory, safety stock percentage, ordering cost, and holding cost.
supplier_data1.xlsx – Supplier prices, lead times, MOQ, and maximum capacity.
procurement_plan.xlsx – Generated procurement results.
Output

The model generates procurement_plan.xlsx with three sheets:

Allocation Plan

Contains the optimized supplier allocation, order quantities, supplier prices, total procurement cost, and lead times.

Unmet Materials

Contains materials that could not be procured and the corresponding reason, such as lead-time infeasibility or MOQ/capacity constraints.

MRP Summary

Contains material-level MRP calculations including gross requirement, current inventory, safety stock, net requirement, earliest due date, days available, EOQ, ordering cost, and EOQ savings.

Technologies Used
Python
Pandas
NumPy
PuLP
OpenPyXL
Jupyter Notebook
How to Run

Install the required libraries:

pip install pandas numpy openpyxl pulp

Open the Jupyter Notebook and ensure all Excel input files are located in the same directory as the notebook.

Run the notebook cells sequentially to generate the optimized procurement plan.

Business Value

This project demonstrates how data-driven MRP and optimization can support inventory planning and procurement decisions by connecting production requirements with inventory availability and supplier constraints.

The model helps identify material shortages, evaluate EOQ-based ordering, determine feasible suppliers, and minimize procurement cost while considering operational constraints.
