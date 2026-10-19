# 📝 AI Resume Generator

An AI-powered resume generator built with **Python**, **Gradio**, and **Ollama**. Users enter their personal and professional details through a simple web interface, and the app sends them to a locally hosted language model (`deepseek-r1`) to generate resume content.

## ✨ Features

- **Simple web UI** built with Gradio.
- **Custom inputs** for name, target job role, years of experience, skills, education, and professional summary.
- **AI-generated resume text** using the Ollama API and the `deepseek-r1` model.
- **HTTP error feedback** when the model endpoint returns an unsuccessful status.

## 🧰 Tech Stack

- Python
- Gradio — interactive web interface
- Requests — HTTP requests to Ollama
- Ollama — local model runtime
- DeepSeek-R1 — configured language model

> **Current implementation note:** Although `fpdf` is installed and imported, the notebook currently returns generated text in the Gradio interface. PDF export has not been implemented yet.

## 🏗️ How It Works

1. The user fills out the fields in the Gradio interface.
2. `gen_resume()` builds a prompt from the submitted details.
3. The app sends a JSON request to the configured Ollama endpoint with the `deepseek-r1` model name.
4. If the endpoint responds with HTTP `200`, the app displays the model's `response` text.
5. If the request fails with another HTTP status, the app displays an error message.

## 📋 Requirements

- Python 3.9+ (a recent Python version compatible with the installed packages is recommended)
- [Ollama](https://ollama.com/) installed and running
- The `deepseek-r1` model pulled in Ollama
- A configured Ollama API endpoint

## 🚀 Setup

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

### 2. Install Python dependencies

```bash
pip install gradio requests fpdf
```

Or, if using the notebook, run the dependency-installation cell first.

### 3. Configure Ollama

Make sure Ollama is running and the model is available:

```bash
ollama pull deepseek-r1
```

Set `OLLAMA_URL` in the notebook to the endpoint for your Ollama API. For a local Ollama server, the common generation endpoint is:

```python
OLLAMA_URL = "http://localhost:11434/api/generate"
```

If Ollama is running on another machine or in a hosted notebook environment, use an endpoint reachable from that environment. `localhost` refers to the machine running the Python process, not necessarily your own computer.

### 4. Run the app

Run the notebook cells in order. The final cell launches the Gradio interface.

Alternatively, move the code into a Python script and run it with:

```bash
python app.py
```

## 🖥️ Usage

1. Open the Gradio app after it launches.
2. Enter your name and target job role.
3. Set your years of experience.
4. Add comma-separated skills, education, and a summary.
5. Submit the form and review the generated resume text.

## 📁 Project Structure

```text
.
├── resume.ipynb    # Notebook containing the app implementation
└── README.md       # Project documentation
```

## ⚠️ Limitations & Improvements

- `OLLAMA_URL` is blank in the provided notebook and must be configured before making requests.
- The code uses `requests.post()` without a timeout or exception handling; connection failures may raise an exception.
- The prompt requests resume content, but output formatting and factual validation are not enforced.
- `fpdf` is imported but not currently used to create a downloadable PDF.
- The example test block references `generate_resume`, while the implemented function is named `gen_resume`; that test block would need correction if used.
- Resume quality depends on the accuracy of the input details and the model response. Review generated content before using it for applications.

## 🔐 Privacy

The app sends the entered details to the configured Ollama endpoint. With a local Ollama instance, inference can run on your own machine; if you configure a remote endpoint, the data is sent to that server. Avoid entering sensitive information unless you understand where it will be processed.

## 🛣️ Possible Future Enhancements

- Generate and download a formatted PDF resume.
- Add resume templates and role-specific prompts.
- Improve error handling and request timeouts.
- Add validation and editable output.
- Support export to DOCX and plain text.
- Add options for tone, seniority, and ATS-friendly formatting.

## 📄 License

No license is specified in the provided notebook. Add a `LICENSE` file if you intend to publish or distribute the project.
