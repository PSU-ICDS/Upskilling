---
layout: default
title: LLM Lab User Guide
description: Learn how to launch and use your private LLM Lab (AnythingLLM + Ollama) on the Roar cluster.
nav_order: 1
---

# LLM Lab (AnythingLLM + Ollama)

The **LLM Lab** provides a secure, private workspace to interact with small to moderately sized Large Language Models (LLMs). It uses **[AnythingLLM](https://docs.anythingllm.com/)** to provide a ChatGPT-like interface where you can chat with models, upload your own documents, and create custom workspaces. Under the hood, it uses **[Ollama](https://docs.ollama.com/)** to run the LLM model directly on Roar compute nodes.

---

## Starting a AnythingLLM Session

1. Log in to the [**Open OnDemand** portal](https://portal.hpc.psu.edu/).
2. Click the **[My Interactive Sessions icon](!../../assets/window-restore.png) My Interactive Sessions** button (may appear as just an icon) to navigate to the [My Interactive Sessions page](https://portal.hpc.psu.edu/pun/sys/dashboard/batch_connect/sessions), then select **LLM Lab** from the left sidebar.
3. Fill out the resource request form:
   * **Account**:  ICDS credit account this job is to be charged to.
   * **Partition**: Standard.
   * **Number of hours**: How long you need the session.
   * **Number of cores**:  Specify at least one CPU core.[^1]
   * **Memory (GB)**: Specify at least 8 GB.[^1]  
   * **Enable advanced Slurm options**:  You _must check this box_ in order to specify that you'll need a GPU (unless you're session is for embedding only).
   * **GPUs**: Add one of the following strings to request a GPU:
      * **A100 GPU**[^2] (40GB VRAM, max 1,555GB/s: `--gres=gpu:a100:1`
      * **A40 GPU** (48GB VRAM, max 768 GB/s):   `--gres=gpu:a40:1`
      * **V100 GPU** (32GB VRAM, max 900GB/s): `--gres=gpu:v100:1`
      * **P100 GPU**[^3] (16GB RAM, max 732 GB/s): `--gres=gpu:p100:1`
      * Any NVIDIA GPU[^4]: `--gres=gpu:1`
4. Click **Launch**.
5. Once your job starts, the status will change to **Running**.  Wait until a blue button **Click to Connect to LLM Lab** appears.  Click it.
6. Start exerimenting with AnythingLLM.  

You can find more detailed documentation at:
  * **[Getting Started](#getting-Started-using-anythingllm) section** below.
  * **[AnythingLLM documentation](https://docs.anythingllm.com/)** for info about more advanced features in Anything LLM.
  * **[Roar Documentation](https://docs.icds.psu.edu/)** for more information on using Roar.

**Footnotes:**

1: Since most AnythingLLM + Ollama sessions rely primarily on the GPU, there is usually not significant benefit to requesting additional CPU cores or RAM for LLM Lab sessions.  It may be advantageous to specify more CPU cores and/or RAM if you plan to upload and process large documents (PDFs, codebases) that will make use of CPU for tools or mcp servers.  It is generally recommended to only run LLM models that fit within the GPU's VRAM.  In some cases, requesting substantially more CPU RAM may allow you to run larger models, but at a much slower speed.

2: Recently, the A100 GPUs have often been in high demand, resulting in long wait times for jobs submitted to these nodes.  

3: The P100 GPUs are older, but optimized for double-precision arithmetic.  These are not well suited for typical LLM-workflows.

4: You will be charged for whichever GPU your job is assigned.  Check the [current rates page](https://icds.psu.edu/services/roar/details-rates/) for details.

---

## Getting Started using AnythingLLM

Once you connect to your LLM Lab session, you will be dropped into the AnythingLLM web interface. 
You will need to create a workspace and to select a model, before beginning a chat.

### Creating a Workspace
Workspaces are isolated environments. For example, you could have one workspace for "Preliminary Literature Review", another for "Prototyping my new algorithm", and a third for "Skills to query arXiv".
1. In the sidebar, click the **+** button (that will reveal a tooltip with **New Workspace**).
2. Enter a unique name for your workspace.
3. Click Save.
4. If you get an error message, first try clicking the back button.  If that doesn't work, go back to the Open OnDemand portal's [My Interactive Sessions page](https://portal.hpc.psu.edu/pun/sys/dashboard/batch_connect/sessions) and click the blue "Click to Connect to LLM Lab" button again.
5. Before you can start a chat session within that workspace, _make sure_ there is a LLM model name (e.g., `gemma4:e4b`) listed in the upper left.  If not, you need to [select a model](#selecting-an-llm-model) before beginning your chat session.
6. [Start a simple chat session] by typing in the main box (with light "Send a message") and click the ⬆️ button (with tooltip "Submit prompt message to workspace").

### Selecting an LLM Model
1. In the upper left, click on the model name (e.g., `gemma4:e4b`, `llama3.1:8b`, `gemma3:12b`, `muse-glimmer:30b`).  The FAQ provides [recommendations for which models to try with with GPUs](#which-models-run-well-on-which-gpus)

2. A dropdown will appear with LLM model providers on the left.  Select "Ollama".
3. Under Available Models for Ollama, select one of the available models from the drop-down menu on the right.  Click "Use this model".

### Start a simple chat session
1. Type your prompt the main textbox (overwriting the light *Send a message*). 
2. Click the [⬆️/up arrow](!../../assets/anythingllm-up-arrow.jpg) button (with tooltip "Submit prompt message to workspace").
3. Wait for the AI's response.
4. Decide how you want to proceed:
   - If you want to continue the thread, building on the previous prompts and responses in this thread, type your next prompt in text box at bottom and repeat.
   - If you want to revise your previous prompt and try again, then scroll up to the grey box with your last prompt, hover your mouse over it, and click the pencil (with tooltip `Edit prompt`).  Edit your prompt and click `Submit`.
   - If you want to continue the thread, but first make edits to the last response before continuing the thread, hover your mouse below the response (just to the right of the speaker icon), and click the pencil (with tooltip `Edit response`).  Edit the response, click `Save`, and the continue your chat session (as described in the first bullet).
   - If you want to delete the response from this thread, then hover your mouse below the response (just to the right of the speaker icon), and click the triple dots (with tooltip `More actions`) and then the trash can (tooltip `Delete`).
   - If you want to create a copy or **fork** of this thread, then hover your mouse below the response (just to the right of the speaker icon), and click the triple dots (with tooltip `More actions`) and then the Fork icon (tooltip `Fork`).  (If you get an error message, first try clicking your web browser's back button.  If that doesn't work, go to the Open OnDemand portal's [My Interactive Sessions page](https://portal.hpc.psu.edu/pun/sys/dashboard/batch_connect/sessions) and click the blue "Click to Connect to LLM Lab" button again.)   Now, there should be two threads with the same name under your workspace name on the left.  
5.  Repeat

### Enabling Web Search (and other Agent Skills)
You can give your AI the ability to search the live internet to answer questions about current events or recent data.  If you turn on web search, then you are asking for the LLM to choose to send data from your prompts, responses, and associated documents over the internet to a search engine.  Whenever working with data that you want to keep local, you should ensure that Web Search is turned **off**.

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
6. To use the search feature, return to your workspace chat (by cliking the ↩ button with tooltip `Back to workspaces`), select a workspace click the **Agent mode** icon (usually a robot or wand icon near the chat input), and enter your prompt question. The AI will now browse the web before generating its response!

---

## Managing Models

The LLM Lab provides access to any of a shared library of LLM models via Ollama. 

### Changing Model for One Workspace

To change the LLM model for a specific workspace:
1. Click the gear icon next to your workspace's name.
2. Click **Chat Settings** tab.
3. Select your preferred model from the **Workspace Chat model**
4. Click blue **Update Workspace** button.
5. Click the ↩/back arrow near upper left of the main pane to return to your workspace.
6. Create a new thread within your workspace, and enter your prompt in the chat box.

### Changing Default Model for Future Workspaces

To change the default model for your future workspaces:
1. Click the **Settings** icon (wrench) at the bottom of the left-hand pane.
2. Navigate to **AI Providers**, **LLM**.
3. Ensure **Ollama** is selected.
4. Select a model from the dropdown list.  (E.g., `gemma4`, `llama3`, `muse-glimmer`).
5. To adjust the maximum context window size, look under Advanced Settings, and enter a specific Model context window length in tokens.  This value should not exceed the maximum context window allowed for that model.  (See [FAQ](#faq))
5. Click **Save changes**.
6. Click **Anthing LLM** in the upper left to return to the list of your workspaces.

---

## Providing LLM with access to documents

### Attaching a document to a prompt.
You can upload your own files (PDFs, Word docs, text, code) and ask the LLM questions about them.
1. Open your Workspace.
2. Click the plus icon or **Upload a Document** button below the textbox to enter a prompt.
3. Upload your files.
4. Enter and upload your prompt.

### Retrieval-Augmented Generation (RAG): Chatting with a specific collection of documents
Sometimes it is useful to be able to submit prompts that have access to a specific collection of documents that may be much larger than the context window of your LLM.  
You can upload your own collection of files (text, markdown, code, csv, PDFs, Word docs, and more) or specify a website with data that that you want this workspace to have access to.  
Using **Connectors**, you have it index data such as a GitHub repository or YouTube transcripts.  

1. Click on a Workspace name in the left pane.
2. Click the Upload icon next to the workspace name (tooltip name "Upload documents to this workspace for RAG indexing").
3. Select files to be incorporated.  For example, "Click to upload or drag and drop" allows you to upload documents from your local computer to Roar.  After uploading a file, it will appear in the file manager box on the left.  Then click **Move to Workspace** and **Add to queue**.
4. The system will process your documents so that future prompts submitted within that workspace can decide which of your documents to bring into context before generating a response.
5. 

Note that embedding is currently performed on the CPU rather than the GPU.  If you want to embed a large number of documents, then you may want to create an LLM Lab session on a standard compute node with no GPUs to perform the embeddings.  Once they're complete, you can open a new LLM Lab session on a GPU node to prompt the LLM to use RAG on the documents you previously embedded.


---

## Data Privacy & Storage

While Roar is approved for both [Level 1 and Level 2 data](https://security.psu.edu/awareness/icdt/), during the pilot, users should restrict their usage to Level 1 data.  ICDS staff will likely need to make configuration changes repeatedly, as they incorporate feedback from users.  Once the beta testing period is complete, ICDS hopes to offer an official AI-as-a-service that can support both level 1 & 2 data.  See [Penn State policies on information classification](https://security.psu.edu/awareness/icdt/).

### Keeping Data Local
* Because AnythingLLM is preconfigured to call Ollama which runs local open-weight models locally on Roar, your prompts and data are not sent to OpenAI, Anthropic, Google, Meta, or other third party when using AnythingLLM (with the default settings).  
* If you update your settings, you may cause data to leave the Roar cluster.  For example, if you enable web search, then AnythingLLM will submit search queries to an external search enginge.  Those queries may contain data from that thread's prompts, responses, and attached or connected documents.
* If you setup connectors, then you are asking AnythingLLM to exchange data between Roar and an external site.  While this maybe a reasonable for some use cases, for others it may introduce unacceptable data privacy issues.  Use your own judgement before setting up any connectors.  

### Workspace Persistance
* Your chats and workspaces persist across sessions. If you close your job today and launch a new one tomorrow, you can still access your workspaces stored on Roar.  
* Everything you type, upload, and configure is saved in your home directory at `~/.anythingllm_storage/`. 
* Any users you grant access to  `~/.anythingllm_storage/` will be able to read your past sessions.
 
### Authentication to AnythingLLM Sessions
Authentication is handled automatically by the usual Penn State authentication process. 
You do not need to enter a separate password to access AnythingLLM. 
Your AnythingLLM session is securely linked to your Penn State account.  
Other users cannot access your session, even if you share the URL.

---

## FAQ

### Choosing models and GPU combinations

#### Which models run well on which GPUs?

| Model                                                                                 | A100 ?0GB | A40 48GB             | V100 32GB         | P100 16GB | CPUs |
|:------------------------------------------------------------------------------------- | --------- | -------------------- | ----------------- | --------- | --------- |
|[muse-glimmer:30b](https://huggingface.co/meta-models/Muse-Glimmer-30B) (Q4_K)         | ✅   | ⚠️ (~2.7T/s)     | ⚠️ (~3.8T/s)  | 🔴           | 🔴 | 
|[llama3.1:8b Instruct](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct) (Q4_K) | ✅   | ✅ (~2.8T/s)     | ✅ (~4.9T/s)  | ⚠️           | 🔴 | 
|[gemma3:12b](https://huggingface.co/google/gemma-3-12b-it)                             | ✅   | ✅ (~5.5T/s)     | ✅ (~3.7T/s)  | ⚠️           | 🔴 | 
|[gemma4:e4b](https://huggingface.co/google/gemma-4-E4B) (Q4_K)                         | ✅   | ✅ (~4.6T/s)     | ✅ (~4.2T/s)  | ✅ (~3.1T/s) | 🔴 | 
|[RAG embedding only](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)    | -    | -                | -              | -            | ✅ |

Key Status Legend:
- ✅ Green Check Mark: The model fits in the GPU's VRAM with room to spare for the stated context window.
- ⚠️ Yellow Yield Sign: The model fits in the GPU's VRAM, but the context window is bottlenecked strictly by the remaining VRAM footprint or the performance is slow for interactive use.
- 🔴 Red Light:  The GPU has insufficient VRAM to load the model weights, resulting in heavy system RAM offloading and slow responses.  Not recommended.

Benchmarks (tokens per second) list above are based on a single initial test and will likely be improved before long.

#### Where can I find current cost of GPU nodes?
See [Roar rates](https://icds.psu.edu/services/roar/details-rates/) page for current rates.


#### Which models are good for what?

| Model | Maximum Context Window | Inputs | Notes |
|:------| -----------------------| ------ | ----- |
|[muse-glimmer:30b](https://huggingface.co/meta-models/Muse-Glimmer-30B) (Q4_K)         | 131,072 | Text/images      | For reasoning | 
|[llama3.1:8b Instruct](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct) (Q4_K) | 131,072 | Text only        | Good for summarizing text | 
|[gemma3:12b](https://huggingface.co/google/gemma-3-12b-it)                             | 128,000 | Text/image       | Old, deprecated model | 
|[gemma4:e4b](https://huggingface.co/google/gemma-4-E4B) (Q4_K)                         | 128,000 | Text/image/audio | Small, fast model, can be deployed on edge devices | 
|[RAG embedding only](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)    |   256   | Text only        | Currently CPU-only  |

Using a context window larger than ~16K will require explicitly setting the maximum context window length.  
See [Managing Models](#managing-models) for instructions.
Using a larger context window can result in slower outputs.  


#### Why aren't bigger models avaliable now?

ICDS aims to order a new GPU cluster optimized for AI workflows soon.  
The new cluster will include more GPUs with more  VRAM and allow ICDS to serve larger local open-weight models to many more users.  
In the mean time, ICDS aims to help users develop experience working with small to medium-size open-weight models and welcomes feedback to inform future purchasing decisions.

#### Why aren't Qwen models avaliable?

ICDS is still seeking permission to make Qwen models avaliable to the ICDS community.  

#### I'd like a specific LLM model to be made avaliable.

Please let us know which models you would like and your intended use case.  
If you have a specific quantization in mind, feel free to include that information.  
Please also let us know whether you need low latency or intend for this model to be used primarily for batch processing where a higher latency would be acceptable.

### Purpose of ICDS AI-as-a-Service

#### Why is ICDS serving small to medium-size open-weight models when Penn State already has AI Studio providing access to frontier-class models?

Open weight models have many advantages.  Using open-weight models gives users more control.  For example, users can: 
- Select from specific models trained for specific purposes.
- Fine-tune an open-weight model on their own datasets for a specific purpose.
- Be confident that they'll be able to reprocess data consistently years later (even if commercial offerings change).  
- Keep data on Penn State controlled systems for greater data privacy.

Additionally, local open-weight models have the potential to:
- Have lower latency than commerical cloud services, and
- Meet many needs more economically and more efficiently.  

Through this pilot, users can begin to explore potential benefits and ICDS can gain experience to provide more robust open-weight AI-as-a-service offerings in the future.

#### Should I expect open-weight models to replace commercial AI models?

No.  It seems likely that open-weight models will continue to trail the capabilities of the latest commerical, frontier models.  
As the gap between open and frontier models narrows, open-weight models may become more attractive, and ICDS anticipates that many users will want to use a combination of open-weight and frontier models. 


### Troubleshooting

#### My session died unexpectedly.
This usually happens for two reasons:
1. **Time Limit:** Your requested Wall Time ran out.
2. **Out of Memory (OOM):** Processing very large documents requires significant RAM. Try launching a new LLM Lab session and requesting more CPU memory (GB) in the web form.  

#### I get an "Unauthorized" error when I open the link.
For security, you must connect to the LLM Lab by clicking the **Connect** button in the Open OnDemand dashboard. If you bookmark the URL and try to visit it later, or share it with a colleague, the security shield will block access.  

#### The response to my first prompt is slow to appear.
Loading the LLM model from disk into VRAM can take a few minutes.  If you submit multiple prompts to the same LLM model (without a gap of more than 5 minutes), the model will stay in VRAM and responses should start to appear more quickly.


#### How do I completely reset my LLM Lab?
If you want to wipe all your chats, workspaces, and settings to start fresh:
1. Stop your current LLM Lab session.
2. Open a cluster terminal.
3. Run: `rm -rf ~/.anythingllm_storage/`
4. Launch a new session.


### Feedback

#### How can I provide feedback?
Send email to icds@icds.psu.edu or complete [this webform](#feedback) **TODO ADD LINK**.

#### Why should I provide feedback?
The primary purpose of the pilot is to help ICDS better understand which use cases are likely to be common.  We look forward to hearing which models and features are most useful to the ICDS Community and which new models users would like to see added.
