
# Getting Started




## Installing LangChain

To start using LangChain, you need to install it. You can do this using pip:

```bash
pip install langchain
```

Depending on the specific use case or model you want to integrate, you might also need additional dependencies. For example, to use OpenAI's models, you would install `langchain-openai`:

```bash
pip install langchain-openai
```

### Example Workflow

Here's a simple example of creating a chain that generates a short summary about a topic using LangChain:

#### 1. Setup the Environment

First, set your API key environment variables for the model you want to use. For OpenAI, it might look like this:

```python
import os
os.environ["OPENAI_API_KEY"] = "your_openai_api_key"
```

#### 2. Create the Prompt

Define what the model should respond with:

```python
from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_template("Provide a short summary about {topic}")
```

#### 3. Initialize the Model

Load the model you want to use:

```python
from langchain_openai import ChatOpenAI

model = ChatOpenAI(model="gpt-3.5-turbo")
```

#### 4. Setup the Output Parser

Define how to handle the model's output:

```python
from langchain_core.output_parsers import StrOutputParser

output_parser = StrOutputParser()
```

#### 5. Create the Chain

Combine these components into a chain:

```python
chain = prompt | model | output_parser
```

#### 6. Run the Chain

Finally, invoke the chain with input to get the output:

```python
result = chain.invoke({"topic": "Python programming"})
print(result)
```

This setup uses a prompt to ask for a short summary about a given topic, passes the prompt to the language model, and then uses an output parser to get the final result.

By following these steps, you can easily start building your applications using LangChain to perform various tasks, like generating summaries, answering questions, or even more complex operations.


