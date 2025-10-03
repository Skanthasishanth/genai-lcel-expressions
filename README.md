## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:

In this experiment we are implementing LangChain Expression Language with two prompt parameters and three key components, where we can generate the prompt output in 4-5 ways depending on the complexity of the prompt such as Simple Chain, More Complex Chain, Bind, Fallbacks, Interface and so on.In this experiment we have include SImple chain and More Complex Chain for better output results.

### DESIGN STEPS:

#### STEP 1:

Load necessary libraries like openai, langchain.prompts, and langchain.chat_models, and set the API key using dotenv.

#### STEP 2:

Create a ChatPromptTemplate, use ChatOpenAI for the model, and StrOutputParser for parsing the output. Chain components using the | operator, provide input, and execute the chain to generate a response.

#### STEP 3:

Create DocArrayInMemorySearch from a list of texts with OpenAIEmbeddings() and set up the retriever.

#### STEP 4:

Use ChatPromptTemplate to combine the retrieved context and user-provided question into a single prompt.Map functions to fetch relevant documents and the question, then invoke the chain to generate a response.

### PROGRAM:

```py
import os
import openai
from dotenv import load_dotenv, find_dotenv
from langchain.prompts import ChatPromptTemplate
from langchain.chat_models import ChatOpenAI
from langchain.schema.output_parser import StrOutputParser

# Load environment variables from a .env file
_ = load_dotenv(find_dotenv()) 
openai.api_key = os.environ['OPENAI_API_KEY']

# 1. Define the ChatPromptTemplate with two parameters
prompt = ChatPromptTemplate.from_template(
    "Tell me a short fun fact about {topic} in a {style} style."
)

# 2. Initialize the model
model = ChatOpenAI()

# 3. Initialize the output parser
output_parser = StrOutputParser()

# Create the LCEL chain
# The chain connects the prompt, model, and output parser
chain = prompt | model | output_parser

# Invoke the chain with the two parameters
# This is where the prompt parameters are supplied
print(f"Fun fact about 'space' in a 'fascinating' style:\n")
response = chain.invoke({"topic": "space", "style": "fascinating"})
print(response)

print("\n" + "="*50 + "\n")

# Another example with different parameters
print(f"Fun fact about 'animals' in a 'humorous' style:\n")
response = chain.invoke({"topic": "animals", "style": "humorous"})
print(response)
```

### OUTPUT:

<img width="1341" height="270" alt="Screenshot 2025-10-03 114917" src="https://github.com/user-attachments/assets/2d6be8cc-8e2f-47fd-9e9a-0bdaf5c3bc62" />


### RESULT:
Thus, the implementation of a LangChain Expression Language (LCEL) is successfully executed.
