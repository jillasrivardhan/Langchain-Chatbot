# 🤖 LangChain Chatbot with Ollama

A simple and professional **AI conversational chatbot** built using **LangChain, Ollama, and Streamlit**.

This project demonstrates how to build a locally running chatbot using LangChain's **ChatPromptTemplate**, **MessagesPlaceholder**, conversation history, and an Ollama-hosted Large Language Model (LLM).

The chatbot can maintain conversation context and provides a simple Streamlit interface for interacting with the locally running model.

---

## 🚀 Features

* 🤖 AI chatbot powered by Ollama
* 🦜🔗 Built using LangChain
* 💬 Maintains conversation history
* 🧠 Context-aware conversations
* 🖥️ Simple Streamlit web interface
* 💻 Can also run as a terminal chatbot
* 🔒 Runs the LLM locally through Ollama
* ⚡ No paid API key required for Ollama
* 🧩 Customizable system prompt
* 🧹 Clear chat functionality
* 🎛️ Temperature configured for consistent responses

---

## 🛠️ Technologies Used

| Technology | Purpose                   |
| ---------- | ------------------------- |
| Python     | Programming language      |
| LangChain  | LLM application framework |
| Ollama     | Local LLM runtime         |
| Qwen 2.5   | Default language model    |
| Streamlit  | Web-based user interface  |

---

# 🧠 How the Project Works

The chatbot follows a simple pipeline:

```text
User
  │
  ▼
Streamlit / Terminal
  │
  ▼
Conversation History
  │
  ▼
ChatPromptTemplate
  │
  ▼
LangChain
  │
  ▼
Ollama
  │
  ▼
Local LLM
  │
  ▼
AI Response
  │
  ▼
Conversation History
```

The conversation history is continuously passed to the model so that it can understand previous messages and maintain context.

---

# 📂 Project Structure

```text
Langchain-Chatbot/
│
├── app.py
├── chatbot.py
├── prompt.py
├── requirements.txt
├── README.md
│
└── screenshots/
    └── chatbot-ui.png
```

### `app.py`

Contains the **Streamlit web interface** for the chatbot.

It handles:

* Streamlit UI
* User input
* Chat messages
* Conversation history
* Ollama model interaction
* Clear chat functionality

---

### `chatbot.py`

Contains the **terminal-based chatbot implementation**.

It demonstrates how to create a conversational chatbot using:

* `ChatOllama`
* `ChatPromptTemplate`
* `MessagesPlaceholder`
* `HumanMessage`
* `AIMessage`

---

### `prompt.py`

Contains the chatbot's **system prompt**.

The system prompt defines the chatbot's:

* Behavior
* Accuracy rules
* Conversation style
* Explanation style
* Limitations
* Handling of future/unknown information

---

### `requirements.txt`

Contains the Python dependencies required to run the project.

---

# 🦙 Ollama Setup

This project uses **Ollama to run the LLM locally**.

Before running the chatbot, you must install Ollama on your computer.

## 1. Install Ollama

Download and install Ollama from its official website:

[Download Ollama](https://ollama.com/?utm_source=chatgpt.com)

After installation, verify that Ollama is available:

```bash
ollama --version
```

You should see the installed Ollama version.

---

# 📥 2. Pull an LLM Model

This project uses:

```text
qwen2.5:3b
```

by default.

Pull the model using:

```bash
ollama pull qwen2.5:3b
```

You can test it with:

```bash
ollama run qwen2.5:3b
```

---

# 💻 Choose a Model According to Your PC

**You do not have to use `qwen2.5:3b`.**

One of the advantages of Ollama is that you can choose a model based on your computer's available:

* RAM
* GPU VRAM
* CPU
* Storage
* Overall performance

For example:

```bash
ollama pull qwen2.5:1.5b
```

or:

```bash
ollama pull qwen2.5:3b
```

or another compatible model available through Ollama.

### General guideline

| Hardware      | Suggested Model Size                            |
| ------------- | ----------------------------------------------- |
| Low-end PC    | ~1B–3B                                          |
| 8 GB RAM      | ~1B–3B                                          |
| 16 GB RAM     | ~3B–8B                                          |
| 32 GB+ RAM    | Larger models may be practical                  |
| Dedicated GPU | Larger models may be possible depending on VRAM |

> ⚠️ These are general guidelines, not strict requirements. Actual performance depends on quantization, context size, GPU/CPU, available RAM/VRAM, and the specific model.

**Choose a model that your PC/laptop can comfortably run.**

After choosing your model, update the model name in `app.py` and `chatbot.py`:

```python
chatmodel = ChatOllama(
    model="your-model-name",
    temperature=0,
    max_completion_tokens=5
)
```

For example:

```python
model="qwen2.5:3b"
```

---

# 🐍 Python Environment Setup

Clone the repository:

```bash
git clone https://github.com/jillasrivardhan/Langchain-Chatbot.git
```

Move into the project directory:

```bash
cd Langchain-Chatbot
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the virtual environment on Windows:

```bash
.venv\Scripts\activate
```

For macOS/Linux:

```bash
source .venv/bin/activate
```

---

# 📦 Install Dependencies

Install the required packages:

```bash
pip install -r requirements.txt
```

If necessary, you can install the Ollama LangChain integration separately:

```bash
pip install langchain-ollama
```

---

# ▶️ Running the Streamlit Application

Make sure Ollama is installed and your selected model has been pulled.

Then run:

```bash
streamlit run app.py
```

Streamlit will start the application locally.

Open the local URL displayed in your terminal.

---

# 💬 Running the Terminal Chatbot

You can also run the original terminal version:

```bash
python chatbot.py
```

You can then interact with the chatbot directly through the terminal.

To exit the terminal chatbot:

```text
exit
```

---

# 🧩 LangChain Components Used

## 1. ChatOllama

`ChatOllama` connects LangChain with the locally running Ollama model.

```python
from langchain_ollama import ChatOllama

chatmodel = ChatOllama(
    model="qwen2.5:3b",
    temperature=0
)
```

---

## 2. ChatPromptTemplate

`ChatPromptTemplate` defines the structure of messages sent to the LLM.

```python
prompt = ChatPromptTemplate.from_messages(
    [
        ("system", prompt),
        MessagesPlaceholder(variable_name="history")
    ]
)
```

---

## 3. MessagesPlaceholder

`MessagesPlaceholder` is used to insert the conversation history into the prompt.

```python
MessagesPlaceholder(variable_name="history")
```

This allows the chatbot to receive previous user and AI messages.

---

## 4. HumanMessage

Represents a message sent by the user.

```python
HumanMessage(content=user_input)
```

---

## 5. AIMessage

Represents a response generated by the AI.

```python
AIMessage(content=chatmodel_response.content)
```

---

# 🧠 Conversation Memory

The project maintains conversation history using a Python list.

```python
history = []
```

User messages are added as:

```python
history.append(
    HumanMessage(content=user_input)
)
```

AI responses are added as:

```python
history.append(
    AIMessage(content=chatmodel_response.content)
)
```

In the Streamlit application, the history is stored using:

```python
st.session_state.history
```

This is important because Streamlit reruns the application whenever the user interacts with the UI.

---

# 🔗 LangChain Pipeline

The chatbot creates a simple LangChain pipeline:

```python
chain = prompt | chatmodel
```

The flow is:

```text
Prompt Template
       │
       ▼
   ChatOllama
       │
       ▼
   Local LLM
       │
       ▼
   AI Response
```

The chain is then invoked using:

```python
chatmodel_response = chain.invoke(
    {
        "history": history,
        "input": user_input
    }
)
```

---

# 🎯 System Prompt

The chatbot uses a custom system prompt defined in `prompt.py`.

The prompt instructs the model to:

* Be helpful and conversational
* Answer questions clearly
* Maintain conversation context
* Avoid intentionally making up information
* Clearly communicate uncertainty
* Avoid pretending to know future events
* Explain complex topics simply
* Adapt explanations to the user's level
* Avoid claiming access to real-time information when it does not have it

This helps create a more reliable and useful conversational experience.

---

# 🛡️ Handling Unknown and Future Information

The system prompt specifically instructs the chatbot not to present unknown future events as facts.

For example, if someone asks:

```text
Who won the IPL match in 2030?
```

The chatbot should not invent an answer.

Instead, it should explain that future match results are not known and that it does not have the ability to predict future events as confirmed facts.

This is an important design principle for reducing **hallucinated information**.

> Note: A system prompt can reduce undesirable behavior, but it cannot guarantee that an LLM will never hallucinate.

---

# 🌡️ Model Configuration

The chatbot currently uses:

```python
temperature=0
```

A temperature of `0` generally encourages more deterministic and consistent responses.

The project also contains:

```python
max_completion_tokens=5
```

This value is intentionally kept from the original project configuration, but **5 tokens is extremely small for normal conversation**.

For longer chatbot responses, consider increasing it or removing the limit depending on your installed `ChatOllama` version and model configuration.

For example:

```python
max_completion_tokens=512
```

---

# 🔐 Privacy

One of the main advantages of using Ollama is that the model can run locally on your computer.

```text
User
  │
  ▼
Local Streamlit App
  │
  ▼
Local Ollama
  │
  ▼
Local LLM
```

This means the project does not require sending every prompt to a paid cloud LLM API.

However, privacy depends on your overall system, installed software, model, and configuration.

---

# 📸 Application Preview

Add your project screenshot here:

```text
screenshots/
└── chatbot-ui.png
```

You can also embed it in your README:

```markdown
![LangChain Chatbot UI](screenshots/chatbot-ui.png)
```

---

# ⚙️ Customization

You can customize the chatbot by modifying:

### Change the model

```python
model="qwen2.5:3b"
```

### Change temperature

```python
temperature=0
```

### Change the system prompt

Edit:

```text
prompt.py
```

### Customize the Streamlit interface

Edit:

```text
app.py
```

---

# 🚧 Possible Future Improvements

Some improvements that can be added to this project:

* [ ] Ollama model selector in Streamlit
* [ ] Streaming responses
* [ ] Model performance information
* [ ] Chat export
* [ ] Download conversation history
* [ ] Multiple chat sessions
* [ ] Persistent conversation storage
* [ ] Markdown response rendering
* [ ] Token usage information
* [ ] RAG support
* [ ] Document-based question answering
* [ ] LangChain agents
* [ ] Tool calling
* [ ] Voice input/output

---

# 🎓 What I Learned

This project helped demonstrate practical concepts such as:

* Connecting Ollama with LangChain
* Running an LLM locally
* Creating chat prompts
* Using `ChatPromptTemplate`
* Using `MessagesPlaceholder`
* Managing conversation history
* Working with `HumanMessage` and `AIMessage`
* Building an LLM pipeline using LangChain
* Creating a chatbot UI using Streamlit
* Designing prompts to reduce hallucination
* Running open-source LLMs locally

---

# 🤝 Contributing

Contributions, suggestions, and improvements are welcome.

1. Fork the repository
2. Create a new branch

```bash
git checkout -b feature/your-feature
```

3. Make your changes
4. Commit your changes

```bash
git commit -m "Add new feature"
```

5. Push the branch

```bash
git push origin feature/your-feature
```

6. Open a Pull Request

---

# 📄 License

This project is intended for educational and learning purposes.

You can add an appropriate open-source license such as MIT if you decide to distribute the project under that license.

---

# ⭐ Support

If you found this project useful:

* ⭐ Star the repository
* 🍴 Fork the repository
* 🐛 Report issues
* 💡 Suggest improvements

---

## 👨‍💻 Author

**Jilla Srivardhan**

Built with ❤️ using **Python + LangChain + Ollama + Streamlit**.

---

## 🔑 Quick Start

For experienced users:

```bash
# Clone repository
git clone https://github.com/jillasrivardhan/Langchain-Chatbot.git

# Enter project
cd Langchain-Chatbot

# Create virtual environment
python -m venv .venv

# Activate environment - Windows
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install LangChain Ollama integration if required
pip install langchain-ollama

# Install/pull an Ollama model
ollama pull qwen2.5:3b

# Run Streamlit application
streamlit run app.py
```

> 💡 **Important:** Before running the project, install **Ollama locally** and pull a model that matches your PC/laptop's hardware capabilities. You can use `qwen2.5:3b` as the default model or replace it with another Ollama-compatible model and update the model name in the Python files.
