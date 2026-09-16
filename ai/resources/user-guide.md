---
layout: default
title: LLM Lab User Guide
description: Learn how to launch and use your private LLM Lab (AnythingLLM + Ollama) on the Roar cluster.
nav_order: 1
---

# LLM Lab (AnythingLLM + Ollama)

The **LLM Lab** provides a secure, private workspace to interact with small to moderately sized Large Language Models (LLMs). It uses **[AnythingLLM](https://docs.anythingllm.com/)** to provide a ChatGPT-like interface where you can chat with models, upload your own documents, and create custom workspaces. Under the hood, it uses **[Ollama](https://docs.ollama.com/)** to run the models directly on our compute nodes, ensuring your data never leaves the cluster.

---

## 🚀 Getting Started

### 1. Launching a Session
1. Log in to the [**Open OnDemand** portal](https://portal.hpc.psu.edu/).
2. Navigate to **Interactive Apps** > **LLM Lab**.
3. Fill out the resource request form:
   * **Wall Time**: How long you need the session.
   * **CPU Cores & Memory**: Increase these if you plan to upload and process large documents (PDFs, codebases).
   * **GPUs**: Request at least 1 GPU by checking the 'Enable advanced Slurm options' and using the --gres=gpu:1 flag.
4. Click **Launch**.
5. Visit [Roar Documentation](https://docs.icds.psu.edu/) for more information on available resources.

### 2. Connecting to Your Lab
Once your job starts, the status will change to **Running**. 
Click the blue **Connect to LLM Lab** button. 

> **Security Note:** Authentication is handled automatically in the background. You do not need to enter a password. Your session is securely locked to your account—other users cannot access your URL.

---

## 💬 Using AnythingLLM

When you connect, you will be dropped into the AnythingLLM interface. 

### Creating a Workspace
Workspaces are isolated environments. You can have one workspace for "Biology Research" and another for "Coding Help."
1. Click **New Workspace** in the sidebar.
2. Give it a name.
3. You can now chat with the default model.

### Chatting with Documents (RAG)
You can upload your own files (PDFs, Word docs, text, code) and ask the AI questions about them.
1. Open your Workspace.
2. Click the **Document icon** (Data connector) next to the chat bar.
3. Upload your files.
4. Click **Save and Embed**. The system will process your documents so the AI can read them.

### Enabling Web Search (Agent Skills)
You can give your AI the ability to search the live internet to answer questions about current events or recent data.
1. Click the **Settings** icon (gear) in the bottom left corner.
2. Navigate to **Agent Skills** in the settings sidebar.
3. Locate the **Web Search** provider options. 
4. Select a search provider (e.g., DuckDuckGo is a great default as it requires no API keys, or you can configure Google/Bing if you have your own credentials).
5. Click **Save**.
6. To use the search feature, return to your workspace chat, click the **Agent mode** icon (usually a robot or wand icon near the chat input), and ask your question. The AI will now browse the web before generating its response!

---

## 🧠 Managing Models

The LLM Lab is connected to a shared library of models via Ollama. 
To change the model you are chatting with:
1. Click the **Settings** icon (gear) in the bottom left.
2. Go to **LLM Providers**.
3. Ensure **Ollama** is selected.
4. Select a model from the dropdown list (e.g., `llama3`, `gemma4`, `muse-glimmer`).
5. Click **Save**.

---

## 💾 Data Privacy & Storage

**Your data is completely private.**
* Everything you type, upload, and configure is saved in your home directory at `~/.anythingllm_storage/`.
* Your chats and documents persist across sessions. If you close your job today and launch a new one tomorrow, all your workspaces will still be there.
* Because the models run locally on the cluster's GPUs, your prompts and data are **never** sent to OpenAI, Google, or any external third party.

---

## ❓ Troubleshooting

**My session died unexpectedly.**
This usually happens for two reasons:
1. **Time Limit:** Your requested Wall Time ran out.
2. **Out of Memory (OOM):** Processing very large documents requires significant RAM. Try launching a new session and requesting more Memory (GB) in the form.

**I get an "Unauthorized" error when I open the link.**
For security, you must connect to the LLM Lab by clicking the **Connect** button in the Open OnDemand dashboard. If you bookmark the URL and try to visit it later, or share it with a colleague, the security shield will block access.

**How do I completely reset my LLM Lab?**
If you want to wipe all your chats, workspaces, and settings to start fresh:
1. Stop your current LLM Lab session.
2. Open a cluster terminal.
3. Run: `rm -rf ~/.anythingllm_storage/`
4. Launch a new session.
