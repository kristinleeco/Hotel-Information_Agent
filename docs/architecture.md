# Architecture

## Overview Diagram

> 🖼️ *[Insert your draw.io diagram here]*
>
> **Alt text:** Flowchart showing four stages: User Input flows into the Azure AI Foundry Agent, which sends the request to the Model for processing, and the Response Output is returned to the user.

A simple version you can recreate in draw.io:

```
┌────────────┐    ┌─────────────────────┐    ┌─────────┐    ┌─────────────────┐
│ User Input │ →  │ Azure AI Foundry    │ →  │  Model  │ →  │ Response Output │
│  (message) │    │ Agent (orchestrator)│    │         │    │  (to the user)  │
└────────────┘    └─────────────────────┘    └─────────┘    └─────────────────┘
```

## How a Request Travels Through the Code

This section maps the **Perception → Reasoning → Action** cycle to the actual code from the Azure AI Foundry playground:

### 1. Authentication (before anything else)

The client authenticates using `DefaultAzureCredential`, which pulls credentials from the environment (Azure CLI login, managed identity, etc.) rather than hardcoded API keys. Secrets, if needed, live in **Azure Key Vault**. This prevents credential leaks in source control.

### 2. Perception — receiving input

The user's message is captured and added to a conversation thread as a message object with a `role` ("user") and `content` (the question text). Data is exchanged in **JSON** (JavaScript Object Notation) — a lightweight, human-readable format both systems understand.

### 3. Reasoning — processing

`create_and_process` kicks off a **run**: the agent takes the thread, applies its instructions (the hotel knowledge and behavior rules), and the model generates a response. This is where configuration parameters like temperature shape the output.

### 4. Action — returning the response

`messages.list` retrieves the updated thread, now containing the assistant's reply, which is parsed from the JSON response and displayed to the user.

## Major Components

| Component | Role |
|---|---|
| **API Endpoint** | The web address where the agent's services are accessed (e.g., `https://YOUR-PROJECT.services.ai.azure.com/...`) |
| **AIProjectClient** | Python client that handles communication with Azure AI Foundry |
| **Agent** | The configured assistant — instructions, model choice, and parameters |
| **Thread** | The conversation container holding the back-and-forth messages |
| **Run** | A single processing pass: input in, reasoning, response out |
| **DefaultAzureCredential** | Secure, keyless authentication |
