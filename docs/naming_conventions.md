# 🏗️ **Data Warehouse Naming Conventions**

> **A comprehensive guide to standardized naming conventions for schemas, tables, views, columns, and objects across all data warehouse layers.**

---

## 📋 **Table of Contents**

- [🎯 General Principles](#-general-principles)
- [📊 Table Naming Conventions](#-table-naming-conventions)
  - [🥉 Bronze Layer Rules](#-bronze-layer-rules)
  - [🥈 Silver Layer Rules](#-silver-layer-rules)
  - [🥇 Gold Layer Rules](#-gold-layer-rules)
- [📝 Column Naming Conventions](#-column-naming-conventions)
  - [🔑 Surrogate Keys](#-surrogate-keys)
  - [⚙️ Technical Columns](#️-technical-columns)
- [🔧 Stored Procedure Conventions](#-stored-procedure-conventions)

---

## 🎯 **General Principles**

### Core Rules for All Database Objects

| **Principle** | **Rule** | **Example** |
|---------------|----------|-------------|
| **Case Style** | Use `snake_case` with lowercase letters | `customer_orders` ✅ <br> `CustomerOrders` ❌ |
| **Word Separation** | Use underscores (`_`) to separate words | `order_line_items` ✅ <br> `orderlineitems` ❌ |
| **Language** | English only for all naming | `customer` ✅ <br> `cliente` ❌ |
| **Reserved Words** | Avoid SQL reserved words | `user_data` ✅ <br> `order` ❌ |

---

## 📊 **Table Naming Conventions**

### 🥉 **Bronze Layer Rules**
*Raw data ingestion layer - preserving source system structure*

```
Pattern: <sourcesystem>_<entity>
```

**Components:**
- **`<sourcesystem>`**: Source system identifier (e.g., `crm`, `erp`, `sap`)
- **`<entity>`**: **Exact** table name from source system (no modifications)

**Examples:**
- `crm_customer_info` → Customer data from CRM system
- `erp_order_details` → Order details from ERP system
- `sap_financial_records` → Financial records from SAP

### 🥈 **Silver Layer Rules**
*Cleaned and standardized data layer*

```
Pattern: <sourcesystem>_<entity>
```

**Components:**
- **`<sourcesystem>`**: Source system identifier (e.g., `crm`, `erp`, `sap`)
- **`<entity>`**: **Exact** table name from source system (no modifications)

**Examples:**
- `crm_customer_info` → Cleaned customer data from CRM
- `erp_order_details` → Standardized order details from ERP
- `sap_financial_records` → Validated financial records from SAP

### 🥇 **Gold Layer Rules**
*Business-ready, modeled data layer*

```
Pattern: <category>_<entity>
```

**Components:**
- **`<category>`**: Business role/purpose of the table
- **`<entity>`**: Business-aligned, descriptive name

**Examples:**
- `dim_customers` → Customer dimension table
- `fact_sales_transactions` → Sales transaction fact table
- `report_monthly_revenue` → Monthly revenue report table

#### 📚 **Category Pattern Glossary**

| **Pattern** | **Purpose** | **Description** | **Examples** |
|-------------|-------------|-----------------|--------------|
| `dim_` | **Dimension Tables** | Master data entities with descriptive attributes | `dim_customer`, `dim_product`, `dim_time` |
| `fact_` | **Fact Tables** | Transactional/measurable business events | `fact_sales`, `fact_inventory`, `fact_web_analytics` |
| `report_` | **Report Tables** | Pre-aggregated data for specific reporting needs | `report_sales_monthly`, `report_customer_summary` |

---

## 📝 **Column Naming Conventions**

### 🔑 **Surrogate Keys**
*System-generated primary keys for dimension tables*

```
Pattern: <table_name>_key
```

**Components:**
- **`<table_name>`**: Name of the entity/table
- **`_key`**: Suffix indicating surrogate key

**Examples:**
- `customer_key` → Primary key in `dim_customers` table
- `product_key` → Primary key in `dim_products` table
- `date_key` → Primary key in `dim_date` table

### ⚙️ **Technical Columns**
*System-generated metadata and audit columns*

```
Pattern: dwh_<column_name>
```

**Components:**
- **`dwh`**: Prefix exclusively for data warehouse metadata
- **`<column_name>`**: Descriptive purpose of the technical column

**Common Technical Columns:**

| **Column Name** | **Purpose** | **Data Type** |
|-----------------|-------------|---------------|
| `dwh_load_date` | Record load timestamp | `DATETIME` |
| `dwh_update_date` | Last update timestamp | `DATETIME` |
| `dwh_source_system` | Source system identifier | `VARCHAR(50)` |
| `dwh_batch_id` | ETL batch identifier | `VARCHAR(100)` |
| `dwh_is_current` | Current record flag (SCD Type 2) | `BOOLEAN` |

---

## 🔧 **Stored Procedure Conventions**
*ETL and data loading procedures*

```
Pattern: load_<layer>
```

**Components:**
- **`load`**: Action prefix for data loading procedures
- **`<layer>`**: Target data warehouse layer

**Examples:**
- `load_bronze` → Procedure for loading raw data into Bronze layer
- `load_silver` → Procedure for data cleansing and Silver layer loading
- `load_gold` → Procedure for business modeling and Gold layer loading

---

## ✅ **Quick Reference Checklist**

Before implementing any database object, ensure:

- [ ] **Case Convention**: All names use `snake_case`
- [ ] **Language**: English names only
- [ ] **Reserved Words**: No SQL reserved words used
- [ ] **Layer Compliance**: Follows appropriate layer naming rules
- [ ] **Business Alignment**: Gold layer names reflect business terminology
- [ ] **Technical Prefixes**: System columns use `dwh_` prefix
- [ ] **Key Suffixes**: Surrogate keys end with `_key`

---

## 🎨 **Benefits of Following These Conventions**

| **Benefit** | **Impact** |
|-------------|------------|
| **🔍 Discoverability** | Easy to locate and understand objects across environments |
| **🤝 Consistency** | Uniform naming reduces confusion and errors |
| **📈 Scalability** | Standards support growth and new team member onboarding |
| **🔧 Maintainability** | Clear patterns make maintenance and troubleshooting efficient |
| **📊 Business Alignment** | Gold layer names match business terminology |

---

*This document serves as the authoritative guide for all data warehouse naming conventions. Adherence to these standards is mandatory for all development teams.*