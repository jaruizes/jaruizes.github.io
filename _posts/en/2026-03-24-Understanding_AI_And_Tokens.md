---
layout: post
title:  "I don't know"
date:   2026-03-24 09:00 +0300
image: "/images/ai-tokens/header.png"
description: "Everyone is building with AI APIs these days, but most people have no idea what a token actually is — and that ignorance has a real cost."
tags:   [AI, LLM, Architecture]
lang: en
---
Nowadays, AI-related discussions and posts are everywhere. You just have to open LinkedIn to see that around 80% of the content is about AI. I’d even say that 90% of those posts focus on Claude Code and how generating code is easier and faster than ever.

Generaing code does not mean building right solutions. The key to build good solutions is having understanding well the context and the problem (thats includes detecting if there is really a problem) in order to generate just the necessary code.

I wonder whether all those people talking about generating more and more code are actually thinking about architecture—and how that code will scale and evolve over time. I've always believed that the best code is the code that is never written. Not writing code means no bugs, no debugging, no time spent coding, and no maintenance.

I also wonder whether those same people are considering security. More code usually means more potential vulnerabilities and more data to manage.

So… what I’m really getting at is this: **architecture matters**.

<br/>

# Introduction

When we talk about AI, A



# Tokens

When you send a message to a language model, the model does not read your text the way you do. It does not see words. It does not see characters. **It sees tokens**.

A token is a chunk of text. It can be a full word, part of a word, a punctuation mark, or even a single character. The exact chunking depends on the tokenizer, which is the component that converts raw text into a sequence of integer IDs before the model processes it.

For example, the phrase *"understanding tokens"* might be split into tokens like: `["under", "stand", "ing", " tokens"]` — or it might be just two tokens, depending on the tokenizer. The word "tokenization" itself is often split into three or four tokens. And a single emoji? That can cost you anywhere from one to four tokens.

This matters because **everything the model processes, everything you are billed for, and every limit you will hit is measured in tokens — not words, not characters, not sentences**. **And, you are not going to pay only for inputs token but also for output tokens.**



<br/>

# The context (window): short term memory

Now that we understand what a token is, we can talk about the concept that will hit you the hardest in production: **the context window**. **The context window is the maximum number of tokens the LLM can “see” at once**.

If you think about a conversation between two people, each message is "stored" in tne memory of each person and by that reason, the conversation has sense.

To better understand, let's take this questions:

- I'm finding holidays in France, can you tell me the capital of France?
- What is its population?
- Is it a safe place to travel?

When the first people asks "I'm finding holidays in France, can you tell me the capital of France?" and the second one answers "Paris", both people "set" Paris in their (short term) memory so, when the second question is asked, both of them know that the question is about population in Paris. 

When we talk about language models a similar concept exists: the context window. **The context window is the maximum number of tokens it can “see” at once**.



## A practical example

I'm developing a [repository to play with all of these topics](https://github.com/jaruizes/generative-ai-examples). In this repository, there is a practical example to show this concept. If you execute the scenario you'll understand how context is necessary when talking to an LLM. 



For example, if we configure the scenario to not add context between interactions, the conversation has no sense:

```
[USER]: I'm finding holidays in France, can you tell me the capital of France?
[ASSISTANT]: The capital of France is Paris.

[USER]: What is its population?
[ASSISTANT]: Population data depends on the specific location you're asking about. Can you provide the name of the city, country, or region?

[USER]: Is it a safe place to travel?
[ASSISTANT]: Safety varies by destination; check travel advisories and local conditions. Research current situations and heed local guidelines.
```

In the second and third question, the LLM does not know what city is talking about the user.



But, if we configure the scenario to add context between interactions, the conversation has totally sense:

```
[USER]: I'm finding holidays in France, can you tell me the capital of France?
[ASSISTANT]: The capital of France is Paris.

[USER]: What is its population?
[ASSISTANT]: As of 2023, Paris has a population of about 2.1 million.

[USER]: Is it a safe place to travel?
[ASSISTANT]: Paris is generally safe, but travelers should exercise caution, especially in crowded areas.
```

If we examine the messages really sent to the LLM, we'll see that, in this cases, each iteration adds information about the previous iterations, increasing the number of input tokens:

```
Conversation history:

  - Iteration: 1
	  -> Messages: [{'role': 'user', 'content': [{'text': "I'm finding holidays in France, can you tell me the capital of France?"}]}]
	  -> Input tokens: 41
	  -> Output tokens: 8
	  -> Total tokens: 49
	  -> Stop reason: end_turn
	  -> Latency (ms): 265

  - Iteration: 2
	  -> Messages: [{'role': 'user', 'content': [{'text': "I'm finding holidays in France, can you tell me the capital of France?"}]}, {'role': 'assistant', 'content': [{'text': 'The capital of France is Paris.'}]}, {'role': 'user', 'content': [{'text': 'What is its population?'}]}]
	  -> Input tokens: 58
	  -> Output tokens: 14
	  -> Total tokens: 72
	  -> Stop reason: end_turn
	  -> Latency (ms): 271

  - Iteration: 3
	  -> Messages: [{'role': 'user', 'content': [{'text': "I'm finding holidays in France, can you tell me the capital of France?"}]}, {'role': 'assistant', 'content': [{'text': 'The capital of France is Paris.'}]}, {'role': 'user', 'content': [{'text': 'What is its population?'}]}, {'role': 'assistant', 'content': [{'text': "Paris's population is approximately 2.1 million people."}]}, {'role': 'user', 'content': [{'text': 'Is it a safe place to travel?'}]}]
	  -> Input tokens: 84
	  -> Output tokens: 23
	  -> Total tokens: 107
	  -> Stop reason: end_turn
	  -> Latency (ms): 328
```



## Let's go deeper

Today, context windows typically range from around 8,000 tokens (smaller models) to 1M tokens like, for example, OpenAI GPT-5.4 (1,050,000 context window). 

We have also to differentiate input tokens and output tokens: models usually allow more input tokens than output tokens and output tokens are more expensive than input tokens. For example, 

- if we choose using **AWS Bedrock with Claude Opus 4.5 in the *eu-south-2* region in standard capacity**, 1k input tokens cost $0.005 while 1k output tokens cost $0.025. That means **output tokens cost 5 times more**
- if we choose **OpenAI and GPT-5.4 in standard capacity**, 1M tokens cost $2.50 while 1M output tokens cost $15. That means **output tokens cost 6 times more**



So, let's think about a use case, for instance, a public administration building a tool to assist customer support operators in retrieving information while handling a case. A case consists on one or multiple doubts that a citizen has about administration procedures (like taxes, medical concerns, etc...). So, resolving a case could 



On average, one token corresponds to about 3–4 characters of English text, or roughly 0.75 words. That means 8,000 tokens ≈ 6,000 words ≈ ~10 pages of text.

For example, imagine a public administration building a tool to assist customer support operators in retrieving information while handling a case. Each case may involve multiple documents, so it is reasonable to assume that covering a single case could require more than 10 pages of context (i.e., more than 8,000 tokens). Let’s assume an input of 10,000 tokens per request.

Output tokens typically range between 20% and 100% of the input, and they are usually more expensive. For example, when using AWS Bedrock with Claude Opus 4.5 in the *eu-south-2* region, 1,000 input tokens cost $0.005, while 1,000 output tokens cost $0.025 (5× more).

In this example, let’s assume the output is 50% of the input. That means:

- Input: 10,000 tokens → $0.05
- Output: 5,000 tokens → $0.125

Total cost per case ≈ **$0.175**

That may seem cheap, but let’s scale it:

- 1,000 cases per day → $175/day
- 5 days per week → ~$875/week
- Monthly (≈4 weeks) → **~$3,500**

And that’s only for the LLM.



# And the memory?

Now that we understand what a token is, we can talk about the concept that will hit you t



And, what about cost? If we said before that you are going to pay for token usage, if you manage 8000 tokens per input request and you estimate, for example, that there will be 1000 request per day, 

![context-window](/images/ai-tokens/context_window.png)

## What Happens When You Hit the Limit?

This is where things get interesting, and where I have seen the most painful production bugs.

When a conversation or prompt exceeds the context window, you have a few options depending on how you have built the system:

- **Hard truncation**: Older messages get dropped silently. The model has no idea they existed.
- **Summarization**: You summarize older messages and inject the summary back into the context.
- **Sliding window**: You keep only the last N tokens of conversation history.

**None of these is free, and none of them is invisible to the end user**. If you truncate history, the model may contradict itself or forget important context it was given earlier. If you summarize aggressively, you lose nuance. If you use a sliding window, the user may feel like the AI "forgot" what they told it five minutes ago.

The point is: you have to **design** for this. It does not handle itself.

<br/>

# Tokens Are Money

Let me be direct about this: **every token you send to and receive from a language model costs money**. Most providers charge per million tokens of input and per million tokens of output, with output typically costing more than input.

At the time of writing, costs vary widely:

- Some smaller, faster models cost fractions of a cent per million tokens
- The most capable frontier models can cost several dollars per million tokens
- Output tokens are typically 3-5x more expensive than input tokens

This sounds abstract until you start building something real. Let me give you a concrete example from my own experience.

Imagine a customer support agent. The system prompt describes how the agent should behave, the tone to use, the escalation policies, the product catalogue. That system prompt alone might be 2,000 tokens. Now multiply that by every conversation turn. If a user has a 10-turn conversation, you are sending that 2,000-token system prompt 10 times. With 1,000 users per day doing the same thing, that is 20 million tokens per day just from the system prompt — before the actual conversation even starts.

> **Token efficiency is not premature optimization. It is basic engineering hygiene when working with LLMs.**

A few principles that I have found useful in practice:

- **Cache or reuse static context** wherever your provider supports it (several providers now offer prompt caching).
- **Be ruthless about system prompt length**. Every word you add costs you on every request.
- **Measure before you optimize**. Use your provider's token counting APIs to understand your actual usage before making architectural changes.
- **Output length is more expensive than input length**. If you want the model to be concise, say so explicitly — it works.

<br/>

# The Prompt is Not Just a Message

This is the part where a lot of developers get surprised. When you call an LLM API, what you think of as "the prompt" is actually a combination of several things, all of which consume tokens from your context window:

- **System prompt**: Instructions, persona, rules, examples
- **Conversation history**: Every turn of the dialogue so far
- **Injected context**: Documents, retrieved chunks from a RAG pipeline, tool results
- **The current user message**: The actual thing the user just typed
- **Model output**: The response itself, which feeds back into the next request

![prompt-anatomy](/images/ai-tokens/prompt_anatomy.png)

The total of all of these has to fit inside the context window. And here is the trap: as a conversation grows, the context fills up from below (new messages) while the system prompt and early history occupy the top. Eventually, something has to give.

When building with LLMs, I think of the context window like a car boot (trunk). You have a fixed amount of space. The heavier your luggage (system prompt, injected documents), the less room you have for passengers (conversation turns). You have to decide what is worth carrying.

<br/>

# Things Nobody Tells You When You Start

After working with LLMs for a while, there are a few things I wish someone had told me earlier:

**Tokens are not language-neutral.** English is tokenized very efficiently. Other languages, especially those with non-Latin scripts (Chinese, Japanese, Arabic, code in non-ASCII character sets), tend to use more tokens for the same amount of information. If your application supports multiple languages, budget accordingly.

**Whitespace and formatting cost tokens.** A Markdown table, a JSON object, XML tags — all of these add tokens beyond the actual content. If you are injecting structured data into your prompt, consider whether a dense format (CSV, YAML) might be more token-efficient than a verbose one (XML, HTML).

**Model reasoning takes tokens too.** When a model "thinks out loud" (chain-of-thought), it is generating tokens that you pay for. Some providers expose reasoning tokens separately. Either way, verbose reasoning before the final answer adds latency and cost.

**Counting tokens before sending a request is possible and useful.** Most providers offer a tokenizer library (`tiktoken` for OpenAI models, for example) that lets you count tokens locally before making the API call. Use this in your monitoring and alerting.

<br/>

# So, What Should You Actually Do?

I am not going to give you a checklist of "token optimization tips". Instead, I want to leave you with a mental model.

Think of the context window as a whiteboard. Every token you put on that whiteboard takes up space. The model can only reason about what is written there. When the whiteboard is full, you have to erase something to write something new. **What you choose to keep on that whiteboard, and what you decide to erase, is the core design problem of every LLM-powered application.**

The engineers who build great AI products are not the ones who know how to call an API. They are the ones who think carefully about information architecture — what context does the model actually need, at each step, to do its job well? Not more, not less.

This is, in the end, not so different from what we do as software engineers all the time: managing state, deciding what to keep in memory and what to persist to disk, designing interfaces that are explicit about what they need. LLMs just make the cost of that design visible in a new and very direct way.

> **Understanding tokens is not about squeezing pennies. It is about building systems that behave predictably and scale without surprises.**

<br/>

So, I hope you liked it, whether you agree or not with my vision. That's all folks.
