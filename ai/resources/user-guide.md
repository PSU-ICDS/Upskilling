---
layout: default
title: LLM Lab User Guide
description: Learn how to launch and use your private LLM Lab (AnythingLLM + Ollama) on the Roar cluster.
nav_order: 1
---

# LLM Lab (AnythingLLM + Ollama)

The **LLM Lab** provides a secure, private workspace to interact with small to moderately sized Large Language Models (LLMs). It uses **[AnythingLLM](https://docs.anythingllm.com/)** to provide a ChatGPT-like interface where you can chat with models, upload your own documents, and create custom workspaces. Under the hood, it uses **[Ollama](https://docs.ollama.com/)** to run the models directly on our compute nodes, ensuring your data never leaves the cluster.

---

## 🚀 Starting a AnythingLLM Session

1. Log in to the [**Open OnDemand** portal](https://portal.hpc.psu.edu/).
2. Navigate to **Interactive Apps** > **LLM Lab**.
3. Fill out the resource request form:
   * **Account**:  ICDS credit account this job is to be charged to.
   * **Partition**: Standard.
   * **Number of hours**: How long you need the session.
   * **Numbs of cores**:  Specify at least one CPU core.^1^
   * **Memory (GB)**: Specify at least 8 GB.^1^  
   * **Enable advanced Slurm options**:  You _must check this box_ in order to specify that you'll need a GPU.
   * must
   * **GPUs**: Add one of the following strings to request a GPU:
      * Any GPU `--gres=gpu:a100:1`
      * Any GPU `--gres=gpu:p100:1`
      * Any GPU `--gres=gpu:v100:1`
      * Any GPU `--gres=gpu:a40:1`
4. Click **Launch**.
5. Once your job starts, the status will change to **Running**.  Wait until a blue button **Click to Connect to LLM Lab** appears.  Click it.
6. Use AnythingLLM.  
7. Learning more
  * See [Getting Started](#Getting-Started-using-AnythingLLM) section below.
  * See [Roar Documentation](https://docs.icds.psu.edu/) for more information on using Roar and available resources.

^1^:   Since most AnythingLLM + Ollama sessions rely primarily on the GPU, there is usually not significant benefit to requesting additional CPU cores or RAM for LLM Lab sessions.  It may be advantagous to specify more CPU cores and/or RAM if you plan to upload and process large documents (PDFs, codebases).  It is generally recommended to only run LLM models that fit within the GPU's VRAM.  In some cases, requested substantially more CPU RAM may allow you to run larger models, but at a much slower speed.

---

## 💬 Getting Started using AnythingLLM

Once you connect to your LLM Lab session, you will be dropped into the AnythingLLM web interface. 
You will need to create a workspace and to select a model, before beginning a chat.

### Creating a Workspace
Workspaces are isolated environments. For example, you can have one workspace for "Literature Review" and another for "Coding Help."
1. In the sidebar, click the **+** button (that will reveal a tooltip with **New Workspace**).
2. Enter a unique name for your workspace.
3. Click Save.
4. If you get an error message, first try clicking the back button.  If that doesn't work, go back to the Open OnDemand portal's [My Interactive Sessions page](https://portal.hpc.psu.edu/pun/sys/dashboard/batch_connect/sessions) and click the blue "Click to Connect to LLM Lab" button again.
5. Before you can start a chat session within that workspace, _make sure_ there is a LLM model name (e.g., `gemma4:e4b`) listed in the upper left.  If not, you need to [select a model](#Selecting-an-LLM-Model) before beginning your chat session.
6. [Start a simple chat session] by typing in the main box (with light "Send a message") and click the up-arrow buttom (with tooltip "Submit prompt message to workspace").

### Selecting an LLM Model
1. In the upper left, click on the model name (e.g., `gemma4:e4b`, `llama3.1:8b`, `gemma3:12b`, `muse-glimmer:30b`).
2. A dropdown will appear with LLM model providers on the left.  Select "Ollama".
3. Avaliable Models for Ollama, select one of the avaliable available models from the drop-down menu on the right.  Click "Use this model".

### Start a simple chat session
1. Type your prompt the main textbox (overwriting the light *Send a message*). 
2. Click the [up-arrow](!../assets/anythingllm-up-arrow.jpg) button (with tooltip "Submit prompt message to workspace").
3. Wait for the AI's response.
4. Decide how you want to proceed:
   - If you want to continue the thread, building on the previous prompts and responses in this thread, type your next prompt in text box at bottom and repeat.
   - If you want to revise your previous prompt and try again, then scroll up to the grey box with your last prompt, hover your mouse over it, and click the pencil (with tooltip `Edit prompt`).  Edit your prompt and click `Submit`.
   - If you want to continue the thread, but first make edits to the last response before continuing the thread, hover your mouse below the responce (just to the right of the speaker icon), and click the pencil (with tooltip `Edit response`).  Edit the response, click `Save`, and the continue your chat session (as described in the first bullet).
   - If you want to delete the response from this thread, then hover your mouse below the responce (just to the right of the speaker icon), and click the triple dots (with tooltip `More actions`) and then the trash can (tool tip `Delete`).
   - If you want to create a copy or **fork** of this thread, then hover your mouse below the responce (just to the right of the speaker icon), and click the triple dots (with tooltip `More actions`) and then the Fork icon (tool tip `Fork`).  (If you get an error message, first try clicking the back button.  If that doesn't work, go to the Open OnDemand portal's [My Interactive Sessions page](https://portal.hpc.psu.edu/pun/sys/dashboard/batch_connect/sessions) and click the blue "Click to Connect to LLM Lab" button again.)   Now, there should be two threads with the same name under your workspace name on the left.  
5.  Repeat

### Enabling Web Search (and other Agent Skills)
You can give your AI the ability to search the live internet to answer questions about current events or recent data.

#### Turning Web Search on/off quickly
1.  Click the **Tools** button next to the plus at the button of the text box for your next prompt.  
2.  Select **Agent Skills**
3.  Click **Web Search** to push the slider to the right and green (web search is on) or to the left and grey (web search is disabled)
4.  Click in the textbox to enter your next prompt.

#### Configuring Web Search
1. Click the **Settings** icon (wrench) at the bottom of the left pane.
2. Click **Agent Skills** in the settings sidebar.
3. Click **Web Search** in the middle pane.  
4. Click the slide in the upper right, so it turns green.
5. Select a search provider (e.g., DuckDuckGo is a great default as it requires no API keys, or you can configure your prefered search engine like Tavily or Perplexity if you have your own credentials).
5. Click **Save**.
6. To use the search feature, return to your workspace chat (by cliking the loop back arrow with tooltip `Back to workspaces`), select a workspace click the **Agent mode** icon (usually a robot or wand icon near the chat input), and enter your prompt question. The AI will now browse the web before generating its response!

### Chatting with a single document
You can upload your own files (PDFs, Word docs, text, code) and ask the LLM questions about them.
1. Open your Workspace.
2. Click the plus icon or **Upload a Document** button below the textbox to enter a prompt.
3. Upload your files.
4. Enter and upload your prompt.

### Chatting with a collection of Documents (RAG)
You can upload your own files (PDFs, Word docs, text, code) and ask the LLM questions about them.
1. Open your Workspace.
2. Click the plus icon or **Upload a Document** button below to the chat bar.
3. Upload your files.
4. Click **Save and Embed**. The system will process your documents so the AI can read them.

---

## 🧠 Managing Models

The LLM Lab is connected to a shared library of models via Ollama. 
To change the model you are chatting with:
1. Click the **Settings** icon (wrench) at the bottom of the left-hand pane.
2. Go to **AI Providers**, **LLM**.
3. Ensure **Ollama** is selected.
4. Select a model from the dropdown list (e.g., `llama3`, `gemma4`, `muse-glimmer`).
5. To adjust the maximum context window size, look under Advanced Settings, and you may Model context window
5. Click **Save changes**.
6. Click **Anthing LLM** in the upper left to return to the list of your workspaces.

---

## 💾 Data Privacy & Storage

* Everything you type, upload, and configure is saved in your home directory at `~/.anythingllm_storage/`.
* Your chats and documents persist across sessions. If you close your job today and launch a new one tomorrow, all your workspaces will still be there.
* Because the models run locally on the cluster's GPUs, your prompts and data are **never** sent to OpenAI, Google, or any external third party.

> **Security Note:** Authentication is handled automatically in the background. You do not need to enter a password. Your AnythingLLM session is securely locked to your account.  Other users cannot access your URL.

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
