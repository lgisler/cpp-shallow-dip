# cpp-shallow-dip<a name="cpp-shallow-dip"></a>

Collection of commonly encountered C++ things

# Work in progress<a name="work-in-progress"></a>

- [core.md](docs/core.md)

## Setup Instructions

Make sure [pyenv](https://github.com/pyenv/pyenv) is installed and initialized
([installation guide](https://github.com/pyenv/pyenv#installation)).

```sh
# Install Python 3.10 (or later) using pyenv
pyenv install 3.10.14

# Set Python version for just the current shell
pyenv shell 3.10.14

# (Optional, but recommended for isolation)
python -m venv .venv
source .venv/bin/activate

# Install project dependencies and pre-commit
pip install --upgrade pip
pip install pre-commit

# Install and run pre-commit hooks
pre-commit install
pre-commit run --all-files
```
