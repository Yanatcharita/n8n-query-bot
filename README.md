

# 🧠 AI-Powered SQL Query via Telegram + Google Sheets Integration (n8n Workflow)

This project is an end-to-end automation built with **n8n**, which allows users to:

- Submit natural language questions in **Thai or English** via **Telegram**
- Automatically convert them to **SQL queries** using **Gemini (Google AI)**
- Run the queries on a **PostgreSQL** database
- Return results via **Telegram** and also log them into **Google Sheets**

## 📦 Features

- ✅ Read structured sales data from Google Sheets
- ✅ Insert cleaned data into PostgreSQL (`employee` table)
- ✅ Use Gemini to generate SQL based on natural language questions
- ✅ Run SELECT queries safely only
- ✅ Format results for Telegram and Google Sheets
- ✅ Support for multiple output channels

## 📊 Data Flow

Google Sheets (raw sales data)
↓
Transform & Insert to PostgreSQL
↓
Telegram (user question)
↓
Gemini API (SQL generation)
↓
Run SQL → Return result to:
↳ Telegram (summary)
↳ Google Sheets (append)

yaml
Copy
Edit

---

## 🧰 Requirements

- [n8n](https://n8n.io) (Self-hosted or cloud)
- PostgreSQL instance
- Google Sheet with structured sales data
- Telegram Bot & Chat ID
- Gemini API Key (from Google AI Studio)

---

## 🗃️ PostgreSQL Table Schema

Before using this workflow, make sure your database has the following table:

```sql
CREATE TABLE employee (
  sales_person TEXT,
  country TEXT,
  product TEXT,
  date DATE,
  amount INT,
  boxes_shipped INT
);
🧾 Google Sheets Format (Input)
Sales Person	Country	Product	Date	Amount	Boxes Shipped
Alice	USA	Dark	2024-12-01	$1,200	100
Bob	UK	Milk	2024-12-02	$800	80

This sheet will be read and inserted into the employee table.

💬 Example Telegram Prompt
Copy
Edit
ยอดขายรวมของแต่ละพนักงานคือเท่าไหร่
✨ The workflow sends this to Gemini, which returns:

sql
Copy
Edit
SELECT sales_person, SUM(amount) AS total_sales
FROM employee
GROUP BY sales_person;
Then the result is returned to Telegram and appended to the output Google Sheet.

📤 Output Google Sheet
sales_person	total_sales
Alice	1200
Bob	800

🔐 Environment Setup
🔑 Telegram Bot Token & Chat ID (setup in Telegram Trigger)

🔑 Google Sheets OAuth2 credentials

🔑 Gemini API Key (https://generativelanguage.googleapis.com/...)

🧩 Nodes Summary
Node	Description
Manual Trigger	For manual data import to PostgreSQL
Google Sheets (Read)	Reads the raw sales data
Function (Transform Data)	Maps and parses fields
PostgreSQL (Insert)	Inserts into employee table
Telegram Trigger	Listens to user messages
Code (Extract Question)	Extracts text message from Telegram
HTTP Request (Gemini)	Sends question to Gemini
Code (Extract SQL)	Cleans response and validates SQL
PostgreSQL (Execute Query)	Executes only SELECT statements
Code (Format for Telegram)	Formats DB result into readable message
Telegram (Send Result)	Sends result back to Telegram
Code (Format for Sheets)	Prepares result rows for Google Sheets
Google Sheets (Append)	Appends results to a Google Sheet

📎 How to Import This Workflow
Go to n8n editor

Click Import

Paste the .json content from this repository

Set up your credentials for:

Google Sheets

PostgreSQL

Telegram

Gemini API (HTTP node)
