# tensorflow_apple
Repo for reproducing Tensorflow Keras issues for Apple Silicon workstations.

## Problem statement

Keras model training kills Python process under certain circumstances.

```
2025-12-03 12:22:01.210583: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:306] Could not identify NUMA node of platform GPU ID 0, defaulting to 0. Your kernel may not have been built with NUMA support.
2025-12-03 12:22:01.210632: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:272] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 0 MB memory) -> physical PluggableDevice (device: 0, name: METAL, pci bus id: <undefined>)
2025-12-03 12:22:21.379296: I tensorflow/core/grappler/optimizers/custom_graph_optimizer_registry.cc:117] Plugin optimizer for device_type GPU is enabled.
2025-12-03 12:22:21.419260: E tensorflow/core/grappler/optimizers/meta_optimizer.cc:961] model_pruner failed: INVALID_ARGUMENT: Graph does not contain terminal node Adam/AssignAddVariableOp.
2025-12-03 12:45:32.968301: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:306] Could not identify NUMA node of platform GPU ID 0, defaulting to 0. Your kernel may not have been built with NUMA support.
2025-12-03 12:45:32.968343: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:272] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 0 MB memory) -> physical PluggableDevice (device: 0, name: METAL, pci bus id: <undefined>)
2025-12-03 12:45:38.269923: I tensorflow/core/grappler/optimizers/custom_graph_optimizer_registry.cc:117] Plugin optimizer for device_type GPU is enabled.
2025-12-03 12:45:38.310917: E tensorflow/core/grappler/optimizers/meta_optimizer.cc:961] model_pruner failed: INVALID_ARGUMENT: Graph does not contain terminal node Adam/AssignAddVariableOp.
2025-12-03 12:59:07.352877: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:306] Could not identify NUMA node of platform GPU ID 0, defaulting to 0. Your kernel may not have been built with NUMA support.
2025-12-03 12:59:07.352897: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:272] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 0 MB memory) -> physical PluggableDevice (device: 0, name: METAL, pci bus id: <undefined>)
2025-12-03 12:59:14.666099: I tensorflow/core/grappler/optimizers/custom_graph_optimizer_registry.cc:117] Plugin optimizer for device_type GPU is enabled.
2025-12-03 12:59:14.706545: E tensorflow/core/grappler/optimizers/meta_optimizer.cc:961] model_pruner failed: INVALID_ARGUMENT: Graph does not contain terminal node Adam/AssignAddVariableOp.
```




## Versions compatibility 

This is relevant only for Apple Silicon machines.

Python | Tensorflow libs | Marks
--- | --- | ---
3.13 | tensorflow 2.19.1 | works without tensorflow-macos
3.13 | tensorflow (version supports 3.13) < (2.17.0) < ? | fails ???
3.13 | tensorflow < (version supports 3.13) ? | not supported
3.13 | tensorflow-macos + tensorflow-metal | not supported + plans?
3.12 | tensorflow 2.18.1 + tensorflow-metal 1.1.0 | works
3.11 | tensorflow-macos 2.15.0 + tensorflow-metal 1.1.0 | works

## Setup and configuration:

### training data

Download: https://drive.google.com/file/d/1WhDq3xo2T-a8BAbx0ByoF8K1zvrHE5f2/view?usp=sharing

Unpack sub-folders with image classes to: data/images


### env1: Python 3.13

```bash
/opt/homebrew/opt/python@3.13/bin/python3.13 -m venv .venv; \
source .venv/bin/activate
```

```bash
pip install --upgrade pip setuptools wheel; \
pip install -r env_setup/requirements.txt; \
python -m ipykernel install --user --name=venv --display-name "CV project Python 3.13 (venv)"
```

RESTART VS Code after that to see the new env in the Jupyter Kernel list.


### TODO:
- create a script that creates custom env for Python and lib versions

-------

## External resources
- [Google Collab notebook for this project](https://colab.research.google.com/github/Funnear/tensorflow_apple/blob/main/notebooks/main.ipynb)


## Other resources
- [tensorflow lib + Python 3.13 issue](https://github.com/tensorflow/tensorflow/issues/78774)
- [tensorflow-metal quick-start guide](https://developer.apple.com/metal/tensorflow-plugin/)
- [tensorflow-metal + Python 3.13 discussion](https://www.reddit.com/r/learnpython/comments/1mksrqj/is_tensorflowmetal_supported_by_python_3132/)
- [TBD](https://github.com/mitmul/tensorflow-metal-sample)
- [Tensorflow with GPU on Google Collab](https://colab.research.google.com/notebooks/gpu.ipynb)
- [Google Cloud CPUs list](https://docs.cloud.google.com/compute/docs/cpu-platforms)