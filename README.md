<h1 align="center">
    Ollama
</h1>

<p align="center">
     <i>A clean & intuitive,<br>Ollama API wrapper for Arturo</i> 
     <br><br>
     <img src="https://img.shields.io/github/license/eloitor/ollama.art?style=for-the-badge">
    <img src="https://img.shields.io/badge/language-Arturo-orange.svg?style=for-the-badge">
</p>


--- 
 
<!--ts-->

* [What does this package do?](#what-does-this-package-do)
* [How do I use it?](#how-do-i-use-it)
* [API Reference](#api-reference)
* [Type Reference](#type-reference)
* [License](#license)   

<!--te-->
 
---

### What does this package do?

This package provides a clean wrapper around [Ollama](https://ollama.com/), allowing you to easily integrate Ollama's capabilities into your Arturo applications. It handles all the API communication, message formatting, and response parsing, providing both low-level access to the full API and convenient high-level methods for common use cases.

### How do I use it?

First, install ollama and download some model. Run `ollama serve`. Then simply `import` the package and initialize a client:

```red
import "ollama"!

; Initialize with your API key
claude: to :ollamaAPI @[ø]!

; Ask a simple question
answer: ollama\ask "What is the capital of France?"
print answer

; Have a more complex conversation
response: ollama\chat [
    createMessage "user" "What's quantum computing?"
    createMessage "assistant" "Quantum computing uses quantum mechanics..."
    createMessage "user" "Can you explain qubits?"
]

; Use custom parameters
response: ollama\chat
  .temperature: 0.9
  .numPredict: 2000
[
    createMessage "system" "You are a creative writing expert"
    createMessage "user" "Write a creative story"
]
```

### API Reference

#### `ollamaAPI`

##### Description

The main client class for interacting with Ollama's API.

##### Methods

###### `chat`

Send messages to Ollama and get responses.

<pre>
<b>chat</b> <ins>messages</ins> <i>:block</i>
</pre>

**Attributes**

| Option | Type | Description |
|----|----|----|
| model | :string | Specify Claude model to use (default: claude-3-sonnet) |
| system | :string | Specify system message |
| temperature | :floating | Set temperature (0.0-1.0) |
| maxTokens | :integer | Set max tokens for response |
| topP | :floating | Set top_p value (0.0-1.0) |
| topK | :integer | Set top_k value |

**Returns**
- *:dictionary* - The complete API response

###### `ask`

Simplified method for single-turn questions.

<pre>
<b>ask</b> <ins>question</ins> <i>:string</i>
</pre>

**Returns**
- *:string* - Ollama's response text

###### Configuration Methods

- `setModel [model :string]` - Set default model
- `setMaxTokens [tokens :integer]` - Set default max tokens
- `setTemperature [temp :floating]` - Set default temperature
- `setTopP [topP :floating]` - Set default top_p

### Type Reference

#### `message`

##### Description

Represents a single message in a conversation.

##### Usage

```red
msg: createMessage "user" "Hello, Ollama!"
```

or

```red
msg: to :message ["user" "This is my message"]
```

##### Fields
- `role` - Either "user" or "assistant"
- `content` - The message content

<hr/>

### License

MIT License

Copyright (c) 2024 Yanis Zafirópulos
Copyright (c) 2024 Eloi Torrents

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
