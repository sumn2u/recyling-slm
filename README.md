# Chat with Local LLMS

This repository is full with examples so that you can interact with local Large
Language Models and challenge yourself in building an application.

There are several examples in the [./examples](examples) directory that you can
use.

## Install the prerequisites

Use the `requirements.txt` to install all dependencies

```bash
python -m venv .venv

source .venv/bin/activate  # On Windows use `.venv\Scripts\activate`

pip install -r requirements.txt
```

### Configure your system


Here is a summary of what this repository will use, including a Retrieval
Augmented Generation Vector database from [Qdrant](https://github.com/qdrant/qdrant):

1. [Qdrant](https://github.com/qdrant/qdrant) for the vector database. We will use an in-memory database for the examples
2. [Llamafile](https://github.com/Mozilla-Ocho/llamafile) or [Ollama](https://github.com/ollama/ollama) for the LLM (alternatively you can use an OpenAI API compatible key and endpoint)
3. [OpenAI's Python API](https://pypi.org/project/openai/) to connect to the LLM after retrieving the vectors response from Qdrant
4. Sentence Transformers to create the embeddings with minimal effort

First, configure your environment variables so that the code examples will know what to load. The `.env` file is a special file that is ignored in the repository but you must create it locally,it ignores the `.env` file to prevent you (and me) from adding these keys by mistake.

This example .env will work for using Phi2 using Ollama:

```
OPENAI_API_BASE="http://localhost:11434/v1"
OPENAI_API_KEY="secret"
MODEL_NAME="phi"
```

And this is for using Llamafile:

```
OPENAI_API_BASE="http://127.0.0.1:8080/v1"
OPENAI_API_KEY="secret"
MODEL_NAME="LLaMA_CPP"
```

### Setup OLLama

For OLLama I recommend using the Phi-2 model. Follow [the instructions for
installation](https://github.com/ollama/ollama?tab=readme-ov-file#ollama) on
your system. These are the steps needed to download Phi2 and run it in your
system:

```
ollama serve
```

And on a separate terminal

```
ollama run phi
```

### Setup Llamafile

For Llamafile I also recommend using the [Phi-2 model](https://github.com/Mozilla-Ocho/llamafile?tab=readme-ov-file#other-example-llamafiles). Download the Llamafile and follow the [instructions for your system](https://github.com/Mozilla-Ocho/llamafile?tab=readme-ov-file#quickstart).



1. Download [phi-2.Q5_K_M.llamafile](https://huggingface.co/jartine/phi-2-llamafile/resolve/main/phi-2.Q5_K_M.llamafile?download=true) (1.97 GB).

2. Open your computer's terminal.

3. If you're using macOS, Linux, or BSD, you'll need to grant permission
for your computer to execute this new file. (You only need to do this
once.)

```sh
chmod +x phi-2.Q5_K_M.llamafile
```

4. If you're on Windows, rename the file by adding ".exe" on the end.

5. Run the llamafile. e.g.:

```sh
./phi-2.Q5_K_M.llamafile --nobrowser
```

6. Your browser should open automatically and display a chat interface.
(If it doesn't, just open your browser and point it at http://localhost:8080)

7. When you're done chatting, return to your terminal and hit
`Control-C` to shut down llamafile.


### Running Small-LM

Navigate to the `examples/small-lm` folder and install the required dependencies. Then, run the following command to start the application:

```sh
uvicorn --host 0.0.0.0 chat:app --env-file .env
```

This will launch the server. You can test the application using the automatically generated FastAPI documentation at:

[http://0.0.0.0:8000/docs](http://0.0.0.0:8000/docs)
