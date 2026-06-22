# 🏦 Automated Financial Intelligence Pipeline for MJ Wealth Track

An automated, serverless data pipeline that intercepts financial transactions directly from a Gmail inbox and securely syncs them to the backend database of the **MJ Wealth Track** application via a custom Deno Edge Function proxy.

## 🗺️ System Architecture

```text
┌────────────────┐          (Every 6 Hours)          ┌──────────────────────┐
│  Gmail Inbox   │ ────────────────────────────────> │  Google Apps Script  │
│ (User Receipt) │                                   │ (Scan & Regex Parse) │
└────────────────┘                                   └──────────────────────┘
                                                                │
                                                                │  POST Request (JSON)
                                                                ▼
┌────────────────┐          Silently Saves To        ┌──────────────────────┐
│ MJ Wealth Track│ <──────────────────────────────── │  Base44 Edge Proxy   │
│  DB (App UI)   │       asServiceRole Privilege     │ (subscriptionReminder)│
└────────────────┘                                   └──────────────────────┘
