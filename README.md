<div align="center">
  <h1> lazyllm </h1>
</div>

TUI interface for LLMs. 

## Featues
- Syntax highlights
- Chat history
- Save chats to files
- Vim keybinding (most common ops)
- Copy text from/to clipboard (works only on the prompt)
- Multiple backends

<br>

## 💎 Supported LLMs

- [x] ChatGPT
- [x] llama.cpp
- [x] ollama

<br>

## 🚀 Installation

### 📥 Binary releases

You can download the pre-built binaries from the [release page](https://github.com/breezykermo/lazyllm/releases)

### 📦 crates.io

`lazyllm` can be installed from [crates.io](https://crates.io/crates/lazyllm)

```shell
cargo install lazyllm 
```

### ⚒️ Build from source

To build from the source, you need [Rust](https://www.rust-lang.org/) compiler and
[Cargo package manager](https://doc.rust-lang.org/cargo/).

Once Rust and Cargo are installed, run the following command to build:

```shell
cargo build --release
```

This will produce an executable file at `target/release/lazyllm` that you can copy to a directory in your `$PATH`.

## ⚙️ Configuration

Lazyllm can be configured using a TOML configuration file. The file should be located in :

- Linux : `$HOME/.config/lazyllm/config.toml` or `$XDG_CONFIG_HOME/lazyllm/config.toml`
- Mac : `$HOME/Library/Application Support/lazyllm/config.toml`

### General settings

Here are the available general settings:

- `archive_file_name`: the file name where the chat will be saved. By default it is set to `lazyllm.archive`
- `llm`: the llm model name. Possible values are:
  - `chatgpt`
  - `llamacpp`
  - `ollama`

```toml
archive_file_name = "lazyllm.archive"
llm  = "chatgpt"
```

### Key bindings

Lazyllm supports customizable key bindings.
You can modify some of the default key bindings by updating the `[key_bindings]` section in the configuration file.
Here is an example with the default key bindings

```toml
[key_bindings]
show_help = '?'
show_history = 'h'
new_chat = 'n'
save_chat = 's'
```

ℹ️ Note

> To avoid overlapping with vim key bindings, you need to use `ctrl` + `key` except for help `?`.

## Chatgpt

To use `chatgpt` as the backemd, you'll need to provide an API key for OpenAI. There are two ways to do this:

Set an environment variable with your API key:

```shell
export OPENAI_API_KEY="YOUTR KEY HERE"
```

Or

Include your API key in the configuration file:

```toml
[chatgpt]
openai_api_key = "Your API key here"
model = "gpt-3.5-turbo"
url = "https://api.openai.com/v1/chat/completions"
```

The default model is set to `gpt-3.5-turbo`. Check out the [OpenAI documentation](https://platform.openai.com/docs/models/gpt-3-5) for more info.

## llama.cpp

To use `llama.cpp` as the backemd, you'll need to provide the url that points to the server :

```toml
[llamacpp]
url = "http://localhost:8080/v1/chat/completions"
```

If you configure the server with an api key, then you need to provide it as well:

Setting an environment variable :

```shell
export LLAMACPP_API_KEY="YOUTR KEY HERE"
```

Or

Include your API key in the configuration file:

```toml
[llamacpp]
url = "http://localhost:8080/v1/chat/completions"
api_key = "Your API Key here"
```

More infos about llama.cpp api [here](https://github.com/ggerganov/llama.cpp/blob/master/examples/server/README.md)

## Ollama

To use `ollama` as the backemd, you'll need to provide the url that points to the server with the model name :

```toml
[ollama]
url = "http://localhost:11434/api/chat"
model = "Your model name here"
```

More infos about ollama api [here](https://github.com/ollama/ollama/blob/main/docs/api.md#generate-a-chat-completion)

<br>

## ⌨️ Key bindings

### Global

These are the default key bindings regardless of the focused block.

`ctrl + n`: Start a new chat and save the previous one in history.

`ctrl + s`: Save the current chat or chat history (history pop-up should be visible first) to `lazyllm.archive` file in the current directory.

`Tab`: Switch the focus.

`j` or `Down arrow key`: Scroll down

`k` or `Up arrow key`: Scroll up

`ctrl + h` : Show chat history. Press `Esc` to dismiss it.

`ctrl + t` : Stop the stream response

`q` or `ctrl + c`: Quit the app

`?`: Show the help pop-up. Press `Esc` to dismiss it

### Prompt

There are 3 modes like vim: `Normal`, `Visual` and `Insert`.

#### Insert mode

`Esc`: to switch back to Normal mode.

`Enter`: to create a new line.

`Backspace`: to remove the previous character.

#### Normal mode

`Enter`: to submit the prompt

<br>

`h or Left`: Move the cursor backward by one char.

`j or Down`: Move the cursor down.

`k or Up`: Move the cursor up.

`l or Right`: Move the cursor forward by one char.

`w`: Move the cursor right by one word.

`b`: Move the cursor backward by one word.

`0`: Move the cursor to the start of the line.

`$`: Move the cursor to the end of the line.

`G`: Go to the end.

`gg`: Go to the top.

<br>

`a`: Insert after the cursor.

`A`: Insert at the end of the line.

`i`: Insert before the cursor.

`I`: Insert at the beginning of the line.

`o`: Append a new line below the current line.

`O`: Append a new line above the current line.

<br>

`x`: Delete one char under to the cursor.

`dd`: Cut the current line

`D`: Delete the current line and

`dw`: Delete the word next to the cursor.

`db`: Delete the word on the left of the cursor.

`d0`: Delete from the cursor to the beginning of the line.

`d$`: Delete from the cursor to the end of the line.

<br>

`C`: Change to the end of the line.

`cc`: Change the current line.

`c0`: Change from the cursor to the beginning of the line.

`c$`: Change from the cursor to the end of the line.

`cw`: Change the next word.

`cb`: Change the word on the left of the cursor.

<br>

`u`: Undo

`p`: Paste

#### Visual mode

`v`: Switch to visual.

`y`: Yank the selected text

<br>

## ⚖️ License

GPLv3
