# Generative AI Chatbot Projects

This repository contains two local, interactive conversational agents built using the `meta-llama/Llama-3.1-8B-Instruct` model from Hugging Face. Both projects fulfill distinct architectural approaches towards building AI applications.

**Author:** Hein Thet Naung

## 1. Basic Chatbot

A fundamental, interactive CLI chatbot built organically using PyTorch, Transformers, and Hugging Face pipelines.

### Features

- **4-Bit Quantization**: Uses the `bitsandbytes` library to load the model efficiently in 4-bit precision, significantly reducing VRAM requirements while maintaining generation quality.
- **Custom Stopping Criteria**: Implements a custom `StopOnSubsequence` class to intercept dialogue hallucination reliably when reserved tags (like `\nUser:`) are detected.
- **Jira Ticket Formatter Agent**: Configured with a system prompt to function as a Jira Ticket Formatter. Helps structurally formulate Jira tickets (Title, Type, Priority, Description, Labels, Attachments, Reporter, Acceptance Criteria).
- **Interactive CLI**: Exposes a real-time, interactive chat session structure inside your terminal.

## 2. Advance Chatbot

A complete LangChain-driven application integrating memory management, semantic instruction routing, and structured JSON parsing. This assistant provides highly sophisticated features over the basic heuristic model implementation.

### Features

- **LangChain Integration**: Built entirely on top of LangChain components, leveraging `HuggingFacePipeline` and native Runnables.
- **Dual-Identity Chain Routing**: A predictive LLM Judge routes user conversations to either a formalized `jira_chain` or a conversational `normal_chain` based continuously on implicit intent.
- **Self-Correction & Format Repair**: Employs an automated LLM retry loop (`jira_repair_chain`) that intercepts structural validation failures and repairs missing metadata dynamically.
- **Long-Term Memory Compression**: Integrates a recursive Summarization Module that dynamically shrinks `ChatMessageHistory` logs into succinct overlapping context bullets, defending against Out-of-Memory token exhaustion.
- **Pydantic JSON Export**: Seamlessly extracts and coerces finalized ticket representations into strictly validated JSON schemas utilizing the `JsonOutputParser`.

## Requirements

Ensure you have the necessary packages installed depending on which notebook you intend to execute:

```bash
# Core Dependencies
pip install torch transformers accelerate bitsandbytes huggingface_hub

# Advanced Chatbot Dependencies
pip install langchain langchain-huggingface langchain-community pydantic
```

## Setup & Execution

1. **Authentication:**
   Set up your Hugging Face authentication by defining a valid `hf_token` variable inside the notebook or via `huggingface-cli login` to fetch restricted models like Llama-3.1.
2. **Launch a Notebook:**
   Execute the cells within `Basic Chatbot.ipynb` or `Advance Chatbot.ipynb` sequentially. The model initialization may take a few minutes depending on your hardware limits.
3. **Chat Interface:**
   Once initialized, submit requests to the interactive text prompts. Type `exit` or `quit` to end the session.
