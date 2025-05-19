# 🧠 Telegram AI SQL Bot (n8n Workflow)

## 🚀 Project Overview

This project began with a simple idea — I wanted a smart assistant that could answer questions about company data effortlessly. Instead of writing SQL, users just ask questions in Thai or English via Telegram. The AI then automatically translates these questions into SQL queries, fetches the data from a PostgreSQL database, and returns an easy-to-read message on Telegram.

### 🎯 Project Goals:
- Allow non-technical users to access database insights using natural language.
- Use AI (Gemini or GPT-4) to automatically generate SQL queries from questions.
- Leverage n8n to build an automated, no-code/low-code workflow.
- Seamlessly integrate Telegram, Google Sheets, PostgreSQL, and AI into one pipeline.

---

## 🔧 Technologies Used

- [n8n](https://n8n.io) – Workflow Automation Platform  
- Telegram Bot API – For receiving and sending messages  
- Google Sheets – For storing results and logs  
- PostgreSQL – Primary data source  
- Gemini AI / GPT – For natural language to SQL generation

---

## 🧩 How It Works (Workflow Summary)
![image](https://github.com/user-attachments/assets/444f9177-0755-495d-bfb2-082d29665489)


1. **📩 Telegram Trigger** – User sends a question via Telegram.
2. **🧠 AI Generate SQL** – The question is sent to Gemini/GPT for SQL conversion.
3. **🗃️ Execute SQL** – SQL is run on the PostgreSQL database.
4. **📝 Format Result** – The result is formatted for readability.
5. **📬 Send Back to Telegram** – The answer is sent back via Telegram.
6. *(Optional)* **📤 Save to Google Sheets** – Log and results are stored for future reference.

---

## 📦 Example Telegram Command

**User sends:**  
> ยอดขายรวมของแต่ละพนักงานคือเท่าไหร่

**Bot replies with something like:**  
👩‍💼 Total Sales by Employee:

Alice: ฿1,200,000

Bob: ฿950,000

Charlie: ฿870,000

pgsql
Copy
Edit

**Including the SQL used:**
```sql
SELECT "Sales Person", SUM(amount) AS total_sales
FROM sales
GROUP BY "Sales Person";
⚙️ Setup Instructions
Create a Telegram Bot and connect it to n8n using the API token.

Set up credentials for PostgreSQL and Google Sheets in n8n.

Import the n8n workflow JSON file.

Customize the nodes: AI provider (Gemini/GPT), database schema, Google Sheet ID, etc.

🔐 Environment Variables
Variable Name	Description
TELEGRAM_TOKEN	Telegram Bot API Token
DB_HOST	PostgreSQL host
DB_USER	PostgreSQL user
DB_PASSWORD	PostgreSQL password
AI_API_KEY	API Key for Gemini or GPT

🙋‍♀️ Future Improvements
- Better understanding of natural Thai language (advanced syntax and idioms).

- Enhance AI accuracy using MCP (Many-shot Context Prompting):

  - Provide a list of example questions with their SQL counterparts.

  - Helps guide the AI to produce better results through contextual learning.
