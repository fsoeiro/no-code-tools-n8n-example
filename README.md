# No-code solutions :: Building a Telegram Diet & Workout Assistant Using n8n

## Introduction

As a healthy lifestyle enthusiast, I have always valued the ability to structure my own diet and workout plans based on trustworthy information. However, finding reliable sources and organizing them into practical daily routines can often be time-consuming. This motivated me to explore how automation and no-code tools could make the process more efficient and accessible — not only for myself but also for others facing similar challenges.

No-code platforms such as **n8n** offer a bridge between non-technical users and automated or more sophisticated solutions. They allow for experimentation, learning, and creation of functional tools without the need for advanced programming skills. Through visual workflows and easy-to-connect integrations, users can quickly prototype useful automations that would otherwise require coding knowledge.

This project was developed as a test case to explore the potential of these tools. The goal was to build a **Telegram chatbot** capable of answering questions related to **diet and workout routines**, using AI to provide clear and practical guidance. The implementation demonstrates how different services — from messaging and AI processing to data logging — can be orchestrated in a single no-code workflow.  
The workflow was entirely developed using **free resources**:  
- n8n’s free trial  
- OpenAI free credits for new accounts (Groq, which is also a free alternative, was also tested, but performed less effectively with agent tools)  
- Telegram integration via a personal bot created using [BotFather](https://core.telegram.org/bots#botfather)  
- Google Sheets for data logging  

Threfore, no costs were incurred throughout the process.

---

## Workflow Overview

The image below (also created by AI) illustrates the interactions within the workflow:

![Telegram Bot Workflow Diagram](https://github.com/fsoeiro/no-code-tools-n8n-example/blob/main/Telegram%20Bot%20Workflow%20Diagram.png)

The workflow connects **Telegram** → **AI Agent** (powered by GPT-4o-mini) → **Telegram reply and Google Sheets logging**, allowing users to chat naturally with an AI assistant specialized in nutrition and fitness. The sequence of nodes ensures smooth conversation handling, contextual memory, and data logging for later review or improvement.

The automation starts when a user sends a message to the Telegram bot. The **Telegram Trigger** node captures the message and passes it to an **AI Agent** node, powered by an **OpenAI language model**. The agent is configured with a structured prompt that positions it as a friendly and knowledgeable coach capable of assisting users with diet and fitness questions. It can clarify exercise execution, suggest substitutions, and explain basic nutrition concepts in a conversational tone.

To maintain context across messages, a **Memory** node stores recent interactions, enabling more natural multi-turn conversations. The **Calculator** and **Date/Time** tools are integrated as AI tools that the agent can invoke when performing numerical or time-related reasoning — for example, estimating calorie needs or adjusting training schedules.

Once the AI generates a response, two actions occur simultaneously:
1. The message is sent back to the user through a **Telegram** node.  
2. A record is appended to a **Google Sheets** log containing the user’s message, the AI’s response, timestamps, and session details.

All credentials, IDs, and sensitive information are redacted in the shared version of this workflow.  
You can explore or reproduce the full setup by reviewing the exported workflow file:

[View the n8n Workflow JSON](https://github.com/fsoeiro/no-code-tools-n8n-example/blob/main/n8n-workflow-healthy-agent.json)

---

## Step-by-Step Breakdown

#### Telegram Trigger  
The workflow begins with the **Telegram Trigger** node, which listens for new messages sent to the bot. It captures key details such as the user’s chat ID, name, username, and message content. Once triggered, the data is passed directly to the **AI Agent** node for interpretation and response generation.  
Telegram was chosen for its ease of setup — bots can be created quickly using [BotFather](https://core.telegram.org/bots#botfather) and connected to n8n from a personal account without requiring business credentials.

#### AI Agent  
At the core of the workflow is the **AI Agent** node. This node defines the assistant’s role and tone through a structured system prompt, positioning it as a friendly and knowledgeable guide for diet and training topics. The agent is designed to communicate clearly, empathetically, and without unnecessary technical language.  
Within n8n, the agent is equipped with several integrated tools:

- **Calculator Tool** – Handles numerical reasoning, such as calorie calculations or macronutrient ratios.  
- **date_time Tool** – Retrieves the current date and time when needed for contextual responses.  
- **Simple Memory** – Maintains a rolling memory of the last seven conversation turns per user, allowing for consistent and contextual interactions.  
- **OpenAI Chat Model (GPT-4o-mini)** – The language model responsible for generating responses, configured with moderate creativity (temperature 0.7).  

The agent dynamically incorporates both the user’s message and the current timestamp into its reasoning, producing timely and context-aware outputs.

#### Simple Memory Node  
The **memoryBufferWindow** node (labeled “Simple Memory”) preserves short-term conversational context, keyed to each user’s unique Telegram chat ID. This ensures the assistant can maintain coherent exchanges across multiple messages within the same session.

#### Telegram (Response) Node  
Once the AI produces its response, the **Telegram** node sends it back to the originating chat. The integration is direct and immediate, delivering the assistant’s message seamlessly into the ongoing conversation without requiring additional configuration.

#### Insert Output Info (Google Sheets)  
To enable monitoring and future improvements, all interactions are logged via the **Google Sheets** node. Each record includes the user’s original message, the AI-generated response, timestamps, chat identifiers, and basic metadata such as username and message ID. These logs are stored in a dedicated *logs* sheet, providing a clear overview of user interactions and the system’s performance over time.

---

### Additional Tools and Configuration

- **OpenAI Model Configuration**: The GPT-4o-mini model was used during OpenAI’s free credit period for n8n new accounts, ensuring no cost was incurred.  
- **Alternative Model Test**: The **Groq** model was also tested as a free option but showed slower and less consistent performance, especially when handling tool-based reasoning within the AI Agent.  
- **Free Setup**: The entire workflow — including Telegram integration, OpenAI access, Google Sheets logging, and all n8n components — was completed using free-tier resources during the n8n trial period.

---

## Key Takeaways

This project demonstrates how no-code tools like **n8n** can dramatically reduce the barrier to entry for automation and AI integration. Even with no programming background, it’s possible to build complex, multi-service systems that combine real-time communication, language models, and structured data storage.

By experimenting with this approach, I learned how no-code workflows can evolve from personal experiments into powerful prototypes — ready to assist, scale, and inspire future projects focused on self-development and well-being.

---
