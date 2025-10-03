# Carbon & Energy Dashboard Normalized Data

This repository contains a normalized version of the carbon and energy dataset, structured as a Star Schema for efficient business intelligence (BI) analysis.

## 💾 Normalized Data Files

The original single-sheet dataset has been split into three CSV files:
1.  **`Fact_Measurements.csv`**: Contains all the metrics (emissions, cost, production) and foreign keys.
2.  **`Dim_Product.csv`**: Lookup table for product types.
3.  **`Dim_Plant.csv`**: Lookup table for plant location details.

## 💡 Data Schema (Star Schema)

The normalization follows a Star Schema model, linking the central Fact Table to the Dimension Tables via Primary (PK) and Foreign (FK) Keys.

```mermaid
erDiagram
    Fact_Measurements {
        int Measurement_ID PK
        datetime Date
        int Product_Key FK
        int Plant_Key FK
        int Production_Units
        float Electricity_kWh
        float Fuel_Tons
        float Renewable_Percent
        float Scope1_Emissions_tCO2
        float Scope2_Emissions_tCO2
        int Energy_Cost_USD
        int Carbon_Tax_USD
    }

    Dim_Product {
        int Product_Key PK
        string Product
    }

    Dim_Plant {
        int Plant_Key PK
        string Plant_ID
        string Location
    }

    Dim_Product ||--o{ Fact_Measurements : used_in
    Dim_Plant ||--o{ Fact_Measurements : located_at
