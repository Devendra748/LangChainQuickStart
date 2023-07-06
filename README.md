# LangChain README

This README provides an overview of the LangChain library and demonstrates its usage through code examples.

LangChain is a Python library that facilitates working with various language models and AI agents. It simplifies the process of generating text, engaging in conversational exchanges, executing actions based on prompts, and managing conversation chains. The library includes the following modules:

## LLMs

The `langchain.llms` module provides access to language models. The example below demonstrates how to use the OpenAI language model.

```python
import os
os.environ["OPENAI_API_KEY"] = "sk-..."

from langchain.llms import OpenAI

llm = OpenAI(temperature=0.9)
llm.predict("What would be a good company name for a company that makes colorful socks?")
# >> Feetful of Fun
# >> Rainbow Hosiery
```

## Chat models

The `langchain.chat_models` module allows you to engage in chat-based conversations with AI models. The example below demonstrates how to use the ChatOpenAI model.

```python
from langchain.chat_models import ChatOpenAI
from langchain.schema import AIMessage, HumanMessage, SystemMessage

chat = ChatOpenAI(temperature=0)
chat.predict_messages([HumanMessage(content="Translate this sentence from English to French. I love programming.")])
# >> AIMessage(content="J'aime programmer.", additional_kwargs={})
# >> AIMessage(content="J'adore la programmation.", additional_kwargs={}, example=False)
chat.predict("Translate this sentence from English to French. I love programming.")
# >> J'aime programmer
# >> J'adore la programmation.
```

## Prompt templates

The `langchain.prompts` module provides a convenient way to create prompt templates. The example below demonstrates how to create a prompt template and format it with specific values.

```python
from langchain.prompts import PromptTemplate

prompt = PromptTemplate.from_template("What is a good name for a company that makes {product}?")
prompt.format(product="colorful socks")
# >> What is a good name for a company that makes colorful socks?
```

## Chains

The `langchain.chains` module enables the creation and execution of conversation chains with language models. The example below demonstrates how to create an LLMChain.

```python
from langchain.chains import LLMChain

chain = LLMChain(llm=llm, prompt=prompt)
chain.run("colorful socks")
# >> BrightSteps Socks.
# >> Cheery Toes.
```

## Agents

The `langchain.agents` module allows the creation and management of AI agents that can execute actions based on prompts. The example below demonstrates how to initialize an agent and interact with it.

```python
import os
os.environ["SERPAPI_API_KEY"] = "SERPAPI_API_KEY"
pip install google-search-results

from langchain.agents import AgentType, initialize_agent, load_tools
from langchain.llms import OpenAI

llm = OpenAI(temperature=0)
tools = load_tools(["serpapi", "llm-math"], llm=llm)
agent = initialize_agent(tools, llm, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True)

agent.run("What was the high temperature in SF yesterday in Fahrenheit? What is that number raised to the .023 power?")
```

## Memory

The `langchain.memory` module provides a way to create and manage conversational memory. The example below demonstrates how to use the `ConversationChain` class.

```python
from langchain import OpenAI, ConversationChain

llm = OpenAI(temperature=0)
conversation = ConversationChain(llm=llm, verbose=True)

conversation.run("Hi there!")
# >> " Hi there! It's nice to meet you. How can I help you today?"

conversation.run("I'm doing well! Just having a conversation with an AI.")
# >> " That's great! It's always nice to have a conversation with someone new. What would you like to talk about?"
```

These code examples should give you a good starting point for using the LangChain library. Feel free to explore the documentation and experiment with different modules and functionalities to suit your specific needs.
