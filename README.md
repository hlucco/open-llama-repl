# Open Source LLM REPL

Small repo containing a REPL for playing with the open source LLMs using torch and 🤗 transformers. Requires a GPU for reasonable performance, but you can use gpt4all on CPU.

## Installation

1. [Install torch](https://pytorch.org/get-started/locally/) for your operating system (CUDA 11.7 if windows, Default if mac) 

2. `pip install -r requirements.txt`

3. `python main.py`

## Usage

Commands are entered using the `/` prefix. The value of an environment variable can be be printed by inputing `<VARNAME>`. All other inputs are passed into the currently loaded model as a prompt.

## Commands

- `/exit` terminates process
- `/tokens [num_tokens]` update the max allowed tokens for generation
- `/model [model_name]` load specified model
- `/meta [filename]` load a meta prompt template from the `/meta` directory
- `/load [filename]` load and run a predefined set of input from the `/load` directory
- `/list` list all supported model names
- `/setvar [key] [val]` add a variable to the REPL environment

## Prompt Templates

To add a prompt template, define the template as any type of text/code file in the `/meta` directory. Loading this prompt into the REPL with the `/meta` command:
```
/meta example.md
```
will add every user input prompt to the `<USER_INPUT>` variable defined in the prompt file and then send the entire prompt to the model. Meta prompts can also support other variables. Additional variables can be added to the prompt by adding a variable marker such as 
```
<EXAMPLE_VARIABLE>
```
`EXAMPLE_VARIABLE` is a placeholder that can be replaced with any string. The additional variable can then be set in the environment using
```
/setvar EXAMPLE_VARIABLE EXAMPLE_VALUE
```
See the `/meta` directory for some example meta prompts.

## Load Command

The `/load` command loads a file of inputs seperated by newlines. These inputs can be any valid input to the REPL (command, variable, user input prompt) and will be run in the order they appear in the loaded file. See the `/load` directory for an example load file.

```
/load example_load_list.txt
```