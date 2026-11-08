1. Cleaning Log
 Issue 1: Column Names Mismatch
  Action Taken: Renamed original columns to match the standard project fields (e.g., invoice_id to Invoice ID, customer_name to Customer, total_amount to Amount).
  Reason: To ensure standardisation across the project modules.
  Rows Affected: All 2,000,000 rows.

 Issue 2: Missing Values & Duplicates Check
  Action Taken: Audited the dataset for nulls and duplicated Invoice IDs.
  Reason: Missing or duplicate data can cause data leakage and errors in ML models.
  Rows Affected: 0 (Dataset was already clean).

 Issue 3: Audit Impossible Dates & Negative Amounts
  Action Taken: Parsed dates to datetime format. Checked for Amount < 0 and Due Date < Invoice Date.
  Reason: To ensure financial integrity of the data.
  Rows Affected: 0 invalid rows found

  2. Data Dictionary & Column Mapping
 Original Column 	Mapped Project Field   	Data Type	    Meaning
 invoice_id	           Invoice ID	        int64	        Unique identifier for each invoice
 customer_name 	        Customer	        object (str)   	Name of the billed client
 invoice_date	       Invoice Date	        datetime64	    Date the invoice was generated
 due_date	            Due Date	        datetime64	    Date the payment is expected
 payment_date	     Payment Date/Status    datetime64	    Date the invoice was actually paid
 total_amount	         Amount  	        float64	        Total invoice billing value
 currency	            Currency	        object (str)	Currency of the invoice (e.g., USD)
 customer_country	    Country	            object (str)	Country of the customer

 
 3. New Engineered Columns
 days_to_pay: Payment Date - Invoice Date (Total days taken to settle).
 delay: Payment Date - Due Date (Positive = late, Negative = early).
 paid_late_flag: 1 if delayed, 0 if paid on time or early.
 open_paid_flag: 'Paid' for all rows since no payment dates were missing.