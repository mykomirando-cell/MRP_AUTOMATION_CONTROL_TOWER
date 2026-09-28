# MRP Application - Functional Specification

## Overview
Convert an Excel-based MRP system into a modern web application focusing on an "Exception-first" design. The system is designed to transition from a local Excel-driven prototype to a cloud-based, database-driven production application.

## Data Evolution Strategy
- **Phase 1 (Prototype):** Direct read from `.xlsb` files using `pyxlsb` for immediate validation.
- **Phase 2 (Hybrid):** Excel as the "Import Source," with data stored in a temporary database for faster querying.
- **Phase 3 (Production):** Full cloud deployment with a database (SQL/NoSQL) and API integrations, moving away from manual Excel dependency.

## Tab Definitions & Data Requirements

### 1. 🏠 Dashboard (Tactical View)
**Purpose:** Daily "firefighting" and inventory execution.
- **Core Features:**
    - **Exception Engine:** Prioritize items with critical shortages or stockout risks.
    - **MRP Execution Matrix:** High-density view of SOH, Forecast, DTL, and Incoming stock.
    - **Action Drawer:** Quick-access tool for buffer adjustments, PO generation, and stock transfers.
- **Data Requirements:**
    - Real-time SOH per warehouse.
    - Weekly Demand Forecasts.
    - Calculated Days to Last (DTL).
    - Incoming Deliveries (PO/Transfers).
    - Exception Flags (Critical/Warning thresholds).

### 2. 📦 Planning (Strategic View)
**Purpose:** Setting the "Rules of the Game" and managing parameters.
- **Core Features:**
    - **Safety Stock Master:** Bulk management of buffers across all SKUs.
    - **Lead Time Matrix:** Configuration of supplier delivery windows.
    - **Seasonal Adjustments:** Applying demand multipliers for peak periods.
    - **Supplier Management:** Tracking vendor reliability and contact details.
- **Data Requirements:**
    - Safety Stock levels per SKU/Warehouse.
    - Supplier Lead Times.
    - Demand Multipliers.
    - Supplier Master Data.

### 3. 📊 Analytics (Audit View)
**Purpose:** Performance tracking and MRP validation.
- **Core Features:**
    - **Accuracy Tracking:** Forecast vs. Actual sales comparison.
    - **Stockout Analysis:** History and duration of stockouts.
    - **Financial View:** Total inventory value per warehouse.
    - **SLA Tracking:** Response time for resolving critical exceptions.
- **Data Requirements:**
    - Historical Sales Data.
    - Stockout timestamps.
    - Unit costs per SKU.
    - Alert resolution logs.

### 4. ⚙️ Settings (System View)
**Purpose:** Configuration and administration.
- **Core Features:**
    - **Data Connection:** Management of source file paths or API endpoints for cloud data.
    - **Access Control:** Role-based permissions (Planner, Supervisor, Manager).
    - **Threshold Configuration:** Defining what constitutes "Critical" or "Warning" DTL.
- **Data Requirements:**
    - System connection strings/paths.
    - User role mapping.
    - Global alert threshold variables.

## Technical Constraints
- **Backend:** Python (initially `pyxlsb`, evolving to a REST API with a database).
- **Frontend:** HTML/CSS/JS (SPA architecture for easy cloud deployment).
- **Design Philosophy:** Item descriptions > Item codes; Exception-first layout.
