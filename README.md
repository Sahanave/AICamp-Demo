# AICamp Demo

# AI Podcast Generator

An intelligent podcast generation system that creates informative, structured audio content using AI agents, search capabilities, and text-to-speech synthesis.

## Overview

This project provides two different implementations of AI podcast generation:

1. **StateGraph Approach**: A structured workflow with explicit state management
2. **ReAct Agent Approach**: A flexible tool-based approach where the AI decides the workflow

Both implementations search the web for information, structure content using the "3-Steps, 2-Types, 1-Thing" framework, and generate audio using ElevenLabs voice synthesis.

## Features

- 🌐 **Web Search Integration**: Uses Tavily API to gather up-to-date information
- 🗣️ **AI Content Generation**: Leverages LLMs (OpenAI or Google Gemini) to create engaging podcast scripts
- 🎙️ **Text-to-Speech**: Converts scripts to natural-sounding audio using ElevenLabs
- 🧠 **Structured Content**: Organizes information in the 3-2-1 framework for clarity and engagement
- 🔄 **Multiple Architectures**: Choose between state-driven or tool-driven approaches

## Installation

```bash
pip install langchain-openai langchain-google-genai langchain-core langchain-tavily langgraph elevenlabs
```

## API Keys Setup

This project requires multiple API keys:

- **OpenAI API Key** (for OpenAI models)
- **Google API Key** (for Gemini models)
- **Tavily API Key** (for web search)
- **ElevenLabs API Key** (for voice synthesis)

In Google Colab, set up your keys:

```python
from google.colab import userdata

# Set environment variables
import os
os.environ['OPENAI_API_KEY'] = userdata.get('OPENAI_API_KEY')
os.environ['GOOGLE_API_KEY'] = userdata.get('GOOGLE_API_KEY')
os.environ['TAVILY_API_KEY'] = userdata.get('TAVILY_API_KEY')
os.environ['ELEVENLABS_API_KEY'] = userdata.get('ELEVENLABS_API_KEY')
```

## Usage

### StateGraph Implementation

```python
# Initialize the agent
agent = Agent()
agent.llm_prompt = "Prepare me a podcast with 3 (Steps) 2 (Types) 1 (Thing) framework. Keep the conversation under 2 minutes"
agent.initialize()

# Generate a podcast
topic = "The future of AI in healthcare"
result = agent.podcast_topic(topic)
```

### ReAct Agent Implementation

```python
# Initialize the agent
agent = ReActAgent()
agent.llm_prompt = """You are an AI podcast host specialized in creating informative podcasts.
When given a topic, follow these steps:
1. Use the search_tool to gather recent information about the topic
2. Organize the content in a 3-Steps, 2-Types, 1-Thing framework
3. Keep your content under 45 seconds when spoken
4. Use the voice_tool with your complete podcast script to generate audio
"""
agent.initialize()

# Generate a podcast
topic = "The future of AI in healthcare"
result = agent.podcast_topic(topic)
```

## Architecture Comparison

| Feature | StateGraph | ReAct Agent |
|---------|------------|-------------|
| Flow Control | Explicit, predefined | Dynamic, agent-determined |
| Flexibility | Lower | Higher |
| Complexity | Simpler | More complex |
| Reasoning | Less autonomous | More autonomous |
| Best For | Predictable workflows | Complex decision-making |

## Components

### 1. LLM Integration
Uses OpenAI's GPT models or Google's Gemini models for content generation.

### 2. Search Tool
Integrates with Tavily API to gather relevant and up-to-date information.

### 3. Voice Synthesis
Uses ElevenLabs API to convert text to natural-sounding speech.

### 4. Graph Structure
- **StateGraph**: Explicit workflow with search → process → voice nodes
- **ReAct**: Tool-based workflow where the agent decides when to search and generate voice

## Customization

- Change voice by modifying the `voice_id` parameter
- Adjust content framework by updating the prompt
- Change models by updating the `model_name` parameter

## Limitations

- Requires active API keys with sufficient credits
- Audio quality depends on ElevenLabs subscription tier
- Content accuracy depends on search results quality
- May encounter rate limiting with free API tiers

## Future Improvements

- Add conversation memory for follow-up questions
- Implement feedback mechanisms to improve content
- Support for multiple voices/speakers
- Add visualization capabilities for statistics/data
- Implement audio editing features

## License

MIT License

## Acknowledgments

- LangChain for providing the agent frameworks
- ElevenLabs for voice synthesis capabilities
- Tavily for search API integration
