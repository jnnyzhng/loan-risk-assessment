# Loan Risk Assessment System

An AI-powered loan risk assessment system that combines n8n workflow automation, AI agents, and a web-based application form to evaluate loan applications based on credit scores, account status, and residency criteria.

## Overview

This project implements an intelligent loan risk analysis system for banking institutions. It uses AI agents to retrieve customer data, consult policy documents, and generate risk assessment reports following strict compliance workflows.

## Features

- **AI-Powered Risk Assessment**: Automated loan risk evaluation using OpenAI GPT and Google Gemini models
- **Multi-Source Data Integration**: Connects to Supabase database for credit scores, account status, and PR status
- **RAG (Retrieval Augmented Generation)**: Vector store for policy documents (Risk Policy & Interest Rate Policy)
- **Guardrails & Compliance**: Multiple validation layers including jailbreak detection, topical alignment, and PII sanitization
- **Interactive Web Form**: Loan application form with embedded AI chatbot assistant
- **Dual View Modes**: Customer view and Employee view with internal risk indicators
- **Print to PDF**: Generate formatted loan application reports

## Project Structure

```
NYP 122/
├── README.md                              # Project documentation
├── .gitignore                             # Git ignore file
├── workflows/                             # n8n workflow definitions
│   └── LoanRiskAssesment.json            # Main AI agent workflow
├── database/                              # Database scripts
│   ├── schema/
│   │   └── Create table.sql              # Table creation script
│   └── seed-data/
│       ├── Customer_Credit_Score_rows.sql
│       ├── Government_PR_Status_rows.sql
│       └── Customer_Account_Status_rows.sql
├── web/                                   # Web interface
│   └── loan_application_form_5.html      # Loan application form with chatbot
└── docs/                                  # Documentation
    ├── presentations/
    │   └── 122_Assignment_Presentation_FINAL.pptx
    └── reference/
        ├── Bank Loan Interest Rate Policy.pdf
        └── Bank Loan Overall Risk Policy.pdf
```

## System Architecture

### 1. n8n Workflow Components

**Data Loading Flow:**
- Form trigger for uploading policy documents
- Vector store for RAG implementation
- Google Gemini embeddings

**Chat Flow:**
- Webhook-based chat trigger
- AI Agent with system prompt for loan risk analysis
- Multiple guardrails for security and compliance

**Tools & Integrations:**
- `Customer_Credit_Score` - Supabase tool for credit scores
- `Customer_Account_Status` - Supabase tool for account status
- `Government_PR_Status` - Supabase tool for PR verification
- Vector Store - Policy document retrieval

### 2. Web Application

- Responsive loan application form
- Customer/Employee toggle view
- Embedded AI chatbot (n8n webhook)
- Risk indicators dashboard (employee view only)
- PDF export functionality

### 3. Database Schema

**Tables:**
- `Customer_Credit_Score` - Credit score records
- `Customer_Account_Status` - Account standing (good, delinquent, closed)
- `Government_PR_Status` - Permanent Resident status for non-Singaporeans

## Risk Assessment Workflow

1. **Data Retrieval**: Fetch credit score and account status
2. **Residency Validation**: Check nationality and PR status for non-Singaporeans
3. **Risk Determination**: Apply policy rules to determine Low/Medium/High risk
4. **Interest Rate Mapping**: Assign appropriate interest rate based on risk level
5. **Final Decision**: Generate recommendation (RECOMMENDED/NOT RECOMMENDED)

## Setup Instructions

### Prerequisites

- n8n instance (cloud or self-hosted)
- Supabase account
- OpenAI API key
- Google Gemini API key

### Database Setup

1. Create a Supabase project
2. Run the schema creation script:
   ```sql
   -- Execute: database/schema/Create table.sql
   ```
3. Load sample data:
   ```sql
   -- Execute files in database/seed-data/
   ```

### n8n Workflow Setup

1. Import `workflows/LoanRiskAssesment.json` into your n8n instance
2. Configure credentials:
   - Supabase API credentials
   - OpenAI API key
   - Google Gemini API key
3. Upload policy PDFs to the vector store using the form trigger
4. Activate the workflow

### Web Application Setup

1. Open `web/loan_application_form_5.html`
2. Update the chatbot iframe URL (line 966) to your n8n webhook endpoint:
   ```html
   <iframe src="YOUR_N8N_WEBHOOK_URL"></iframe>
   ```
3. Deploy to your web server or open locally

## Usage

### For Customers

1. Open the loan application form
2. Select your profile from the dropdown
3. Review and update loan details
4. Submit for risk analysis or use the AI chat assistant
5. Print to PDF if needed

### For Bank Employees

1. Toggle to "Employee" view mode
2. View internal risk indicators:
   - Credit Score
   - Debt-to-Income ratio
   - Income Multiple
   - Overall Risk Assessment
3. Review policy-based recommendations

### Using the AI Chatbot

The chatbot can answer questions about:
- Loan eligibility criteria
- Risk assessment factors
- Interest rate policies
- Application workflow
- Specific customer assessments (by NRIC)

## Security Features

- **Jailbreak Detection**: Prevents prompt injection attacks
- **Topical Alignment**: Ensures queries are within business scope
- **PII Sanitization**: Automatically masks sensitive NRIC information
- **Access Control**: Employee-only sections in web form

## Technologies Used

- **Workflow Automation**: n8n
- **AI Models**: OpenAI GPT-4.1-mini, Google Gemini
- **Database**: Supabase (PostgreSQL)
- **Frontend**: HTML5, CSS3, JavaScript
- **Vector Store**: n8n In-Memory Vector Store
- **Embeddings**: Google Gemini embeddings

## Sample Data

The system includes three sample customers:
- **George (ID: 6666)**: High Risk, Closed Account
- **Jonny (ID: 7777)**: High Risk, Delinquent Account
- **Shufeng (ID: 8888)**: Low Risk, Good Standing

## License

This project is for educational purposes as part of NYP Assignment 122.

## Contributors

NYP Assignment Team - 2025
