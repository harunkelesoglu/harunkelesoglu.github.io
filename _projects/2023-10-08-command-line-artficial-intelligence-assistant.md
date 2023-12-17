---
layout: default
title: "CLAI"
stack: "Shell"
snippet: "CLAI is a command-line AI assistant tool designed for developers who prefer using the command-line interface (CLI) over a graphical user interface (UI)"
pinned: false
githublink: https://github.com/harunkelesoglu/clai
order: 3
usehighlight: true
---

<h1 style="color: #e03c31;" class="venenosa">CLAI</h1> 

**CLAI** is a command-line AI assistant tool designed for developers who prefer using the command-line interface (CLI) over a graphical user interface (UI). With CLAI, you can interact with OpenAI's GPT models directly from your CLI, eliminating the need to switch to a separate UI.

## Prerequisites

Before using CLAI, ensure you have the following prerequisites:

- Bash shell (typically available on Unix-like systems)
- `curl` command-line tool
- `jq` command-line tool (for JSON parsing)
- OpenAI API key
- Knowledge of your preferred OpenAI model (e.g., "gpt-3.5-turbo" or "gpt-4.0")

## Usage

To use CLAI, follow these steps:

1. Set the required environment variables in your shell profile:

   - `OPENAI_API_KEY`: Your OpenAI API key.
   - `OPENAI_MODEL`: The OpenAI model you want to use.

2. Run CLAI with a user message as an argument:

   ```bash
   ./clai.sh "User's message goes here."

## Installation Instructions

To make CLAI easily accessible, follow these steps:

1. Move the CLAI script to the `/usr/local/bin` directory:
   
   ```bash
   sudo mv clai.sh /usr/local/bin/clai

2. Make the script executable:

   ```bash
   sudo chmod +x /usr/local/bin/clai

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Author

- Harun Keleşoğlu
- Contact: [harun.kelesoglu19@gmail.com](mailto:harun.kelesoglu19@gmail.com)



