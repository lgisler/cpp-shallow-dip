# cpp-shallow-dip<a name="cpp-shallow-dip"></a>

Collection of commonly encountered C++ things

# Work in progress<a name="work-in-progress"></a>

- [core.md](docs/core.md)

## Setup Instructions

```sh
# Install Node 20 using nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# Install node 20
nvm install 20
nvm use 20

# Install pyenv
curl -fsSL https://pyenv.run | bash

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
