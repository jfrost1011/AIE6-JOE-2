<p align = "center" draggable=”false” ><img src="https://github.com/AI-Maker-Space/LLM-Dev-101/assets/37101144/d1343317-fa2f-41e1-8af1-1dbb18399719" 
     width="200px"
     height="auto"/>
</p>

## <h1 align="center" id="heading">Session 2: Embeddings and RAG</h1>

### [Quicklinks](https://github.com/AI-Maker-Space/AIE6/tree/main/00_AIM_Quicklinks)

| 🤓 Pre-work | 📰 Session Sheet | ⏺️ Recording     | 🖼️ Slides        | 👨‍💻 Repo         | 📝 Homework      | 📁 Feedback       |
|:-----------------|:-----------------|:-----------------|:-----------------|:-----------------|:-----------------|:-----------------|
| [Session 2: Pre-Work](https://www.notion.so/Session-2-Embeddings-Retrieval-Augmented-Generation-RAG-1c8cd547af3d81978a5af041c0d5b30a?pvs=4#1c8cd547af3d818daab3db56a5e631e9)| [Session 2: Embeddings, Retrieval Augmented Generation (RAG)](https://www.notion.so/Session-2-Embeddings-Retrieval-Augmented-Generation-RAG-1c8cd547af3d81978a5af041c0d5b30a) | [Recording](https://us02web.zoom.us/rec/share/gSn6QuqteVM4gYK9SslqMLx4MRVcwVj1S9RT-wJQYUuSVBkJ14-Fj8qY8d7Tyx-9.7ijgK2xRDpWFZ-bu) (lz2MTcF=)| [Session 2: Embeddings and RAG](https://www.canva.com/design/DAGjaSBtoao/n8G0T_O-2OIQHvgTfqyAxg/edit?utm_content=DAGjaSBtoao&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton) | You Are Here! | [Session 2 Assignment: Embeddings & RAG](https://forms.gle/FNkAuvdZe8eiaLTC8)| [AIE6 Feedback 4/3](https://forms.gle/iDTwhJ2nLp5CGkqP6)


### Outline:

🤜 BREAKOUT ROOM #1:
- Task 1: Imports and Utilities
- Task 2: Documents
- Task 3: Embeddings and Vectors
- Task 4: Prompts
- Task 5: Retrieval Augmented Generation
     - 🚧 ACTIVITY #1: Augment RAG

### Steps to Run:

1. Install UV - which you can do through [this resource](https://docs.astral.sh/uv/#getting-started)
2. Run the command `uv sync`
3. Open your Jupyter notebook and select `.venv` for your kernel. 

# Build 🏗️

Run the notebook!

# Ship 🚢

- Add one of the following "extras" to the RAG pipeline:
     - Allow it to work with PDF files
     - Implement a new distance metric
     - Add metadata support to the vector database
- Make a simple diagram of the RAG process
- Run the notebook
- Record a Loom walking through the notebook, the questions in the notebook, and your addition!

# Share 🚀
- Show your App in a loom video and explain the diagram
- Make a social media post about your final application and tag @AIMakerspace
- Share 3 lessons learned
- Share 3 lessons not learned

Here's a template to get your post started!

```
🚀 Exciting News! 🎉

I just built and shipped my very first Retrieval Augmented Generation QA Application using Chainlit and the OpenAI API! 🤖💼 

🔍 Three Key Takeaways:
1️⃣ The power of combining traditional search methods with state-of-the-art generative models is mind-blowing. 🧠✨
2️⃣ Collaboration and leveraging community resources like AI Makerspace can greatly accelerate the learning curve. 🌱📈
3️⃣ Dive deep, keep iterating, and never stop learning. Each project brings a new set of challenges and equally rewarding lessons. 🔄📚

A huge shoutout to the @AI Makerspace for their invaluable resources and guidance. 🙌

Looking forward to more AI-driven adventures! 🌟 Feel free to connect if you'd like to chat more about it! 🤝

#OpenAI #Chainlit #AIPowered #Innovation #TechJourney
```

API Key Setup
Local Development
Create a .env file in the project directory
Add your OpenAI API key:
OPENAI_API_KEY=your_api_key_here
Deployment
GitHub: Use repository secrets
Huggingface: Use Space secrets
Other platforms: Use their environment variable systems
Note: Make sure to add .env to your .gitignore file to keep your API key secure.

❓ Question #1:
The default embedding dimension of text-embedding-3-small is 1536.

Is there any way to modify this dimension?
Answer:
Yes, you can modify the dimension of embeddings from text-embedding-3-small. According to the OpenAI API documentation, you can use the dimensions parameter when creating embeddings. This allows you to request lower-dimensional embeddings (from 1 to 1536).
Answer:
OpenAI uses a technique called dimensionality reduction to achieve this. When you request a lower dimension, the original 1536-dimensional vector is compressed while attempting to preserve as much semantic information as possible. This is likely done through mathematical techniques like Principal Component Analysis (PCA) or similar methods.

❓ Question #2:
What are the benefits of using an async approach to collecting our embeddings?

Answer:
The benefits of using an async approach to collecting embeddings include:

Improved Performance: Async allows the program to continue working on other tasks while waiting for API responses. Since embedding generation requires sending requests to OpenAI's servers and waiting for responses, this can significantly improve throughput.
Batch Processing Efficiency: The async approach allows multiple embedding requests to be sent concurrently rather than sequentially. With hundreds or thousands of text chunks, this means we don't have to wait for each embedding to complete before starting the next one.
Resource Utilization: While waiting for network responses, the CPU can work on other tasks, making better use of available resources.
Scalability: As the corpus size grows, async becomes increasingly important. With sync processing, embedding a large corpus could take hours, while async can reduce this to minutes.
Responsiveness: In an interactive application, async processing keeps the user interface responsive while the embedding work happens in the background.

The core difference between async and sync approaches is that synchronous code executes sequentially (one operation must complete before the next begins), while asynchronous code allows operations to run concurrently, especially during waiting periods for I/O operations like network requests.
In this specific case, embedding generation is an I/O-bound task perfect for async processing, as most of the time is spent waiting for the API response rather than doing CPU-intensive work.

❓ Question #3:
When calling the OpenAI API - are there any ways we can achieve more reproducible outputs?

Answer:
When calling the OpenAI API, we can achieve more reproducible outputs by adjusting the temperature and seed parameters:

Temperature: Setting the temperature parameter to a lower value (closer to 0) makes outputs more deterministic and focused. At temperature=0, the model will always select the most likely next token, making responses more consistent and reproducible.
Seed: Using the seed parameter allows for reproducible outputs across different runs. When you set a seed value and keep other parameters the same, you'll get very similar outputs for the same inputs.
Top_p: Similar to temperature, lowering the top_p value (nucleus sampling) can make outputs more focused and consistent by limiting the tokens the model considers.
Max_tokens: Setting a consistent max_tokens value ensures the length constraint is the same across runs.
Presence_penalty and frequency_penalty: Keeping these values consistent helps maintain similar response patterns.

For maximum reproducibility, you would set temperature=0 and provide a specific seed value. However, even with these settings, 100% identical outputs aren't guaranteed due to how these models work, but they will be much more consistent than with default settings.

❓ Question #4:
What prompting strategies could you use to make the LLM have a more thoughtful, detailed response?

What is that strategy called?

Answer:
A prompting strategy to make the LLM provide more thoughtful, detailed responses is Chain-of-Thought (CoT) prompting.
Chain-of-Thought prompting involves explicitly instructing the language model to break down its reasoning process step by step before arriving at a final answer. This approach encourages the model to:

Think through the problem methodically
Consider different aspects of the question
Evaluate evidence critically
Show its reasoning explicitly
Arrive at more considered conclusions

You could implement this in the RAG system by modifying the system prompt to include instructions like:
"First, analyze what the question is asking. Then, carefully examine the provided context for relevant information. Break down your thinking step by step, considering different interpretations and evidence. After reasoning through the information, provide a comprehensive answer that addresses all aspects of the query."

Chain-of-Thought prompting has been shown to significantly improve performance on complex reasoning tasks and produce more thoughtful, nuanced responses that better reflect the available information.

Activity #1:
(Done in the Pythonic_RAG_Assignment.ipynb notebook)



