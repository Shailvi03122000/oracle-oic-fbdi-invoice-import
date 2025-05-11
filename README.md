# 📦 Oracle Integration Cloud – FBDI Invoice Import to ERP Cloud

## 📌 Project Overview

This Oracle Integration Cloud (OIC) project demonstrates how to **import AP invoices into Oracle ERP Cloud** using the **FBDI (File-Based Data Import)** approach. 
The integration retrieves a zipped CSV file from a secure FTP location and uploads it to ERP Cloud using the **ERP Cloud Adapter**.

---

## 🧩 Use Case

- AP invoice data is prepared offline in Oracle-provided Excel templates (FBDI format).
- These files are zipped and dropped onto a secure FTP server.
- OIC picks up the `.zip` file, uploads it to Oracle ERP Cloud, and initiates the **Import Payables Invoices** process.
- Result of the import is tracked and visible in ERP’s Payables > Invoices screen.

---

## ⚙️ Technologies Used

- **Oracle Integration Cloud (OIC)**
- **FTP Adapter** (to fetch FBDI zip file)
- **ERP Cloud Adapter** (to upload and import file)
- **File-Based Data Import (FBDI)**
- **Email Notifications** (optional)

---

## 🪜 Step-by-Step Integration Flow

### 🔹 1. Prepare Input Files

- Use **`GSEPayablesStandardInvoiceImportTemplate.xlsm`** to populate:
  - `AP_INVOICES_INTERFACE`
  - `AP_INVOICE_LINES_INTERFACE`
- Generate CSV and zip files:
  - `apinvoiceimport.zip`
    - Contains: `ApInvoiceInterface.csv`, `APInvoiceLinesInterface.csv`, and `APTEST.PROPERTIES`

### 🔹 2. Upload to FTP Server

- Upload `apinvoiceimport.zip` to:  
  `/home/user1/ora038` using **WinSCP** or another SFTP tool.

### 🔹 3. Create OIC Connections

- **FTP Adapter**: To read the zipped invoice file
- **ERP Cloud Adapter**: To upload the file and trigger the import process

### 🔹 4. Build OIC Integration

- **Type**: Scheduled Orchestration
- **Steps**:
  1. **Trigger**: Scheduled to run periodically
  2. **Read File** from FTP (`ReadAPInvoicesFileFromFTP`)
  3. **Invoke ERP Adapter** (`ImportAPInvoicestoERPCloud`)
     - Action: `Import Bulk Data`
     - Business Object: `Import Payables Invoices`
  4. **Data Mapping**:
     - Map File Reference, Directory, and Filename from FTP to ERP input
  5. **(Optional)**: Add notification or fault handling
 
  6. ### 📷 Integration Flow Diagram
![Integration Flow]([images/integration-flow.png](https://github.com/Shailvi03122000/oracle-oic-fbdi-invoice-import))

### 🔹 5. Activate and Run 

- Activate the integration
- Run manually or wait for the schedule
- Track the instance from **OIC > Observe > Instances**

### 🔹 6. Verify in ERP Cloud

- Go to Oracle ERP Cloud > Payables > Invoices
- Search by invoice number used in FBDI template
- Confirm successful import

---

## 📂 Repository Contents

| Path                     | Description                                    |
|--------------------------|------------------------------------------------|
| `FBDI_IMPORT.car`        | Exported OIC integration archive               |
| `docs/FBDI.pdf`          | Full setup and process documentation           |
| `templates/`             | Excel template and sample CSV files            |
| `README.md`              | This file                                      |

---

## ✅ Benefits

- Eliminates manual AP invoice entry
- Scalable and reusable for bulk invoice import
- Demonstrates end-to-end use of FBDI with OIC

