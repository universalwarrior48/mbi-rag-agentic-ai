# LangChain

**Engineering Note:**
Ollama runs locally. Before running this code, ensure you have installed Ollama and pulled a model (e.g., `ollama pull llama3.2`).

## Ollama & LangChain Cheat Sheet

| Package/Method | Description | Code Example |
| --- | --- | --- |
| **pip install** | Installs the necessary LangChain libraries for Ollama integration. | `!pip install langchain-ollama langchain-core` |
| **OllamaLLM** | Facilitates interaction with locally hosted Ollama models. Replaces `WatsonxLLM`. | `from langchain_ollama import OllamaLLM` `llm = OllamaLLM(model="llama3.2", temperature=0.5, num_predict=256, top_p=0.9)` |
| **llm_model Function** | Wrapper function to invoke the Ollama model with specific prompts and dynamic parameters. | `def llm_model(prompt_txt, params=None):` `config = {"num_predict": 256, "temperature": 0.5, "top_p": 0.2}` `if params: config.update(params)` `llm = OllamaLLM(model="llama3.2", **config)` `response = llm.invoke(prompt_txt)` `return response` |
| **llm_model Function** | Wrapper function to invoke the Ollama model with specific prompts and dynamic parameters. | <pre>def llm_model(prompt_txt, params=None):<br>    config = {<br>        "num_predict": 256,<br>        "temperature": 0.5,<br>        "top_p": 0.2<br>    }<br>    if params:<br>        config.update(params)<br>    llm = OllamaLLM(model="llama3.2", **config)<br>    response = llm.invoke(prompt_txt)<br>    return response</pre> |
| **Parameters** | Dictionary for controlling text generation. Note: Ollama uses `num_predict` instead of `max_new_tokens`. | `params = {"num_predict": 128, "temperature": 0.5, "top_k": 40, "top_p": 0.9}` `response = llm_model("The wind is", params)` |
| **Basic Prompt** | Direct text input without special formatting. | `params = {"num_predict": 128, "temperature": 0.7}` `prompt = "The wind is"` `response = llm_model(prompt, params)` `print(f"Response: {response}")` |
| **Zero-shot Prompt** | Asking the model to perform a task without prior examples. | `prompt = """Classify this statement as true or false: 'The Eiffel Tower is located in Berlin.' Answer:"""` `response = llm_model(prompt)` |
| **One-shot Prompt** | Providing a single example to guide the output format. | `prompt = """Example: English: "How are you?" French: "Comment ça va?" Task: English: "Where is the nearest supermarket?" French:"""` `response = llm_model(prompt)` |
| **Few-shot Prompt** | Providing multiple examples (2-5) to establish a pattern. | `prompt = """Statement: 'I won the lottery!' -> Emotion: Joy Statement: 'I lost my keys.' -> Emotion: Frustration Statement: 'My friend is moving away.' -> Emotion: Sadness Statement: 'The movie was terrifying.' -> Emotion:"""` `response = llm_model(prompt)` |
| **Chain-of-Thought (CoT)** | Asking the model to "think step-by-step" to improve logic. | `prompt = """Problem: A store had 22 apples. They sold 15 and got 8 new ones. How many apples are left? Let's think step by step:"""` `response = llm_model(prompt)` |
| **PromptTemplate** | Reusable structure for prompts with variables (from `langchain_core`). | `from langchain_core.prompts import PromptTemplate` `template = "Tell me a {adjective} joke about {content}."` `prompt = PromptTemplate.from_template(template)` `formatted = prompt.format(adjective="funny", content="Linux")` |
| **LCEL Pattern** | Using the pipe `|` syntax to compose chains (`Prompt | LLM |

For a visual walkthrough of setting up these models locally and understanding the difference between simple scripts and proper engineering workflows, this video is highly relevant.

[LangChain RAG Tutorial](https://www.youtube.com/watch?v=2xxziIWmaSA)

This video demonstrates how to move beyond basic prompt scripts to building full RAG applications using local models like Ollama, reinforcing the LCEL concepts covered above.
