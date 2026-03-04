# Basic Chatbot

Create a basic, interactive CLI chatbot using a causal language model from Hugging Face. This project implements a conversational agent using the `meta-llama/Llama-3.1-8B-Instruct` model.

**Author:** Hein Thet Naung

## Features

- **4-Bit Quantization**: Uses the `bitsandbytes` library to load the model efficiently in 4-bit precision, significantly reducing VRAM requirements while maintaining quality.
- **Custom Stopping Criteria**: Implements a custom `StopOnSubsequence` class to prevent the LLM from simulating the user's side of the conversation by halting token generation when reserved tags (like `\nUser:`) are detected.
- **Jira Ticket Formatter Agent**: Configured with a strict system prompt to act as a Jira Ticket Formatter. It helps users write detailed, well-structured Jira tickets (Title, Type, Priority, Description, Labels, Attachments, Reporter, Acceptance Criteria).
- **Interactive CLI**: Provides an interactive chat session loop for real-time conversations.

## Requirements

Ensure you have the following packages installed:

```bash
pip install torch transformers accelerate bitsandbytes huggingface_hub
```

## Setup & Execution

1. **Authentication**: The notebook requires authentication with the Hugging Face Hub. Set your `hf_token` variable in the notebook with a valid access token to download restricted models like Llama-3.1.
2. **Run Notebook**: Execute the cells in `Basic Chatbot.ipynb` sequentially. The model will initialize (which may take a few minutes depending on your hardware).
3. **Chat**: Once initialized, type your prompts into the interactive prompt. Type `exit` or `quit` to end the session.

## Components Breakdown

- **Model Initialization**: Sets up 4-bit quantization config and loads the tokenizer and causal language model.
- **Stopping Criteria**: Defines halting logic to ensure the bot doesn't generate dialogue for the user.
- **Generation Logic**: Manages context limits, bounds conversational length to prevent Out-Of-Memory errors, formats prompts, and runs inference.
