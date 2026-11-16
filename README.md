<img width="1077" height="822" alt="grafik" src="https://github.com/user-attachments/assets/e75b783a-7446-4709-95b8-5116657a284a" />

# Musical Instrument Rental

A database project for managing a musical instrument rental business. The system supports instrument inventory, customer management, rental and return workflows, rental price calculation, and the identification of instruments available for sale.

## 🛠️ Toolstack

![Microsoft SQL Server](https://img.shields.io/badge/Microsoft_SQL_Server-Database-CC2927?logo=microsoftsqlserver&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Database_Development-4479A1?logo=postgresql&logoColor=white)
![Visual Studio](https://img.shields.io/badge/Visual_Studio-IDE-5C2D91?logo=visualstudio&logoColor=white)

## Project Overview

The application is designed for a business that rents musical instruments to:

- Private individuals
- Music schools
- Music bands

Instruments can also be offered for sale. Each instrument is assigned an instrument type and an instrument group and stores information such as its serial number, purchase price, condition, residual value, rental eligibility, sale status, and number of previous rentals.

The rental price depends on three factors:

- Instrument type
- Instrument condition
- Rental period

## Data Base Diagramme

<img width="1314" height="826" alt="grafik" src="https://github.com/user-attachments/assets/31883a42-cb50-4d65-bc13-adb534ae6699" />

## Main Features

### Instrument and Inventory Management

- Store instrument details, including serial number, type, group, purchase price, condition, and residual value.
- Mark instruments as unavailable for rental or as sold.
- Track the number of previous rentals.
- Review inventory quantities through database views.

### Customer Management

The system supports three customer types: private individuals, music schools, and music bands.

When a customer is created, a trigger assigns an individual customer ID and records the appropriate customer type in the customer table.




### Rental Workflow

1. Search for instruments of a selected type that are available for the requested rental period.
2. Validate the rental input.
3. Select the first instrument matching the requested criteria.
4. Calculate the planned rental price based on instrument type, condition, and rental duration.
5. Create a rental record containing the customer, instrument, condition at handover, rental start date, planned return date, and rental price.

### Return Workflow

1. Validate the return information.
2. Compare the actual return date with the planned return date.
3. Recalculate the rental price if the return date differs.
4. Update the instrument's condition using the condition recorded at return.
5. Apply checks to ensure that the returned condition is not better than the condition at handover, preventing unrecorded repairs or incorrect condition entries.

### Sales

A table-valued function and a related view make it possible to find instruments that are eligible for sale based on a maximum residual price and a minimum condition requirement.

## Database Functionality

The project uses several database objects to implement its business logic:

- **Tables, constraints, and indexes** for storing and validating data.
- **Triggers** to assign customer IDs and customer types when customer records are created.
- **Views** for displaying available instruments, inventory quantities, customer names, and instruments eligible for sale.
- **Table-valued functions** to search for available instruments and instruments for sale.
- **Scalar functions** for rental price calculation and rental-count information.
- **Stored procedures** to process rentals and returns, including input validation and business-rule checks.

Examples of documented views and functions include:

- `InstrumenteAusleihbar` – displays instruments available for a specified rental period.
- `view_WieVieleinstrumenteHabenWir` – summarizes the instrument inventory.
- `view_KundenNamen` – displays customer names across the supported customer types.
- `tf_SucheInstrumenteZuVerkaufen` – searches for instruments that meet sale criteria.

## Repository Structure

The project documentation describes the following folders and files:

| Folder | Main file(s) | Purpose |
|---|---|---|
| `001-DB-Create-Scripts` | `09_Create_DataBase_Gesamt.sql` | Combined script for creating database objects and generating data |
| `001-DB-Create-Scripts` | `09_00_Create_DataBase.sql` | Creates the `MusikInstrumentVerleih` database |
| `001-DB-Create-Scripts` | `09_01_Create_Table_Constraint_Index.sql` | Creates tables, constraints, checks, and indexes |
| `002-Abfragen und View` | `09_02_Create_View.sql` | Creates database views |
| `003-StoredFunctions` | `09_03_Function.sql` | Creates table-valued and scalar functions |
| `004-StoredProcedures` | `09_04_Stored_Procedure.sql` | Creates stored procedures |
| `005-DML-Trigger` | `09_05_Create_Trigger.sql` | Creates triggers for the different customer types |
| `006-BackUp` | `MusikInstrumentVerleih_20251212_Final.bak` | Final database backup |
| `007-Datenimport` | `09_06_Daten_Import.sql` | Generates data for testing the business logic |
| `008-Testskript_Praesentation` | `09_07_01_Test_Procedure_Ausleihvorgang.sql` and `09_07_02_Test_Procedure_Rueckgabe.sql` | Tests the rental and return procedures |
| `008-Testskript_Praesentation` | `09_07_03_Test_AusleihPreisBerechnen.sql` to `09_07_06_Test_InstrumentAnzahlAusleihen.sql` | Tests the documented functions |
| `008-Testskript_Praesentation` | `09_08_DemoSkriptMusikinstrumentVerleih.sql` | Script for the project presentation |
| `009-Dokumentation` | `Projektdokumentation_Musikinstrumentverleih.docx` | Project documentation |

> The folder and file names above follow the supplied project documentation. If the repository uses slightly different names, update this table to match the actual Git structure.


## Testing

The supplied test scripts cover:

- Rental procedure
- Return procedure
- Rental price calculation
- Search for instruments eligible for sale
- Search for instruments available during a rental period
- Instrument rental-count function

## Project Team

- Paulina Staus
- Lucie Teubner
- Waldemar Baron


**Project date:** 12 December 2025

