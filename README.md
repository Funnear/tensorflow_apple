# tensorflow_apple
Repo for reproducing Tensorflow issues for Apple Silicon


## Setup and configuration:

### training data

Download: https://drive.google.com/file/d/1WhDq3xo2T-a8BAbx0ByoF8K1zvrHE5f2/view?usp=sharing

Unpack subfolders with image classes to: data/images


### env1: Python 3.13

```bash
/opt/homebrew/opt/python@3.13/bin/python3.13 -m venv .venv; \
source .venv/bin/activate
```

```bash
pip install --upgrade pip setuptools wheel; \
pip install -r env1_setup/requirements.txt; \
python -m ipykernel install --user --name=venv --display-name "CV project Python 3.13 (venv)"
```

RESTART VS Code after that to see the new env in the Jupyter Kernel list.



### env2: Python 3.11

