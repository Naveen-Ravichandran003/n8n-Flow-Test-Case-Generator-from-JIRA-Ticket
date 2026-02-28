# Test Case Generator from JIRA Ticket (n8n Workflow)

## Overview
This repository contains an automated n8n workflow designed to analyze user stories from JIRA and generate professional, enterprise-grade QA test cases. The workflow uses an AI Agent powered by Groq to analyse the user story and produce deterministic, reproducible test scenarios which are automatically appended into a Google Sheet.

## Workflow Components
1. **Chat Trigger (User Input):** Serves as the entry point to initiate the test generation process.
2. **AI Agent:** The core processing unit instructed with a robust system prompt using a Role-Instruct-Context-Expected format for precision QA test case generation.
3. **Groq Chat Model (`llama-3.1-8b-instant`):** The specific Large Language Model used to evaluate the JIRA issue and generate the tests.
4. **JIRA Tool:** Connects to Atlassian JIRA to read inputs (e.g., getting data for specific issues like `KAN-229`) which serve as the source user story.
5. **Code Node (Output Formatting):** A JavaScript step that processes the strict JSON array output from the AI, ensuring compatibility and managing string formats (like replacing `<br>` with newline characters in test steps).
6. **Google Sheets Integration:** Maps the generated test cases and appends them line-by-line directly into a designated Google Spreadsheet for test management.

## System Prompt Architecture
The AI replies on a heavily structured system prompt that dictates the following:
- **Role (R):** Senior QA Test Architect (15+ years experience).
- **Instructions (I):** Analyze user stories, generate exactly 8 deterministic test cases, and adhere to strict QA principles.
- **Context (C):** Detailed feature contexts such as testing a "Forgot Password" flow, 24-hr link validity, and account lockouts.
- **Expected Coverage (E):** Enforces a mix of positive, negative, and edge case scenario generation.
- **Parameters (P) & Output Format (O):** Strict instructions demanding a raw JSON array output with no additional text or markdown, formatted explicitly for downstream system parsing.
- **Tone (T):** Professional, enterprise QA standard, structured, and clear.

## Data Structure Extracted
The generated functional test cases strictly map to the following schema within the Sheets execution:
- `Test Case ID`
- `Test Scenario`
- `Test Type`
- `Preconditions`
- `Test Steps`
- `Expected Result`
- `Priority`

## Files
- `Test Case Generator from JIRA Ticket.json`: The exported n8n workflow blueprint containing node configurations, system prompt parameters, data schemas, and integration setups.
- `System Prompt.md`: Can be used for extracting and version-controlling the AI Agent's specific test generation prompt constraint logic (Note: This file appears to be empty in the current directory and should be populated with the text node content from the JSON to centralize prompt tracking).

## Dependencies & Credentials Required (in n8n)
- **Groq API Account**: For invoking the LLM.
- **Jira Software Cloud API Account**: To pull user stories directly from your Atlassian ecosystem.
- **Google Sheets OAuth2 API**: To push the processed and normalized test case data.

## Getting Started
1. Import `Test Case Generator from JIRA Ticket.json` into your local or cloud n8n workspace.
2. Authenticate and select your connections for JIRA, Groq, and Google Sheets in their respective nodes.
3. Update the JIRA tool node to target your desired Jira Issue Key dynamically or test it with an existing item.
4. Configure the Google Sheet node with your target Spreadsheet URL and Tab.
5. Execute the workflow to autonomously generate your test documentation!
