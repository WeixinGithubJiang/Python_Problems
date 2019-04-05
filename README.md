# Python_Problems


## 1. how to create and remove virtual environment in anaconda?
Virtual environment is quite important when using python, because it kind of provides a independent environment from the original system. The benefits is that we may install libraries/packages whatever we want, and it will not influence other environments.

> Create a new Virtual Environment
```bash
conda create -n env_name python=3
```

> Check the list of all existing environments
```bash
conda env list
```

> Check the configuration of conda
```bash
conda info
```

> Remove an existing environment
```bash
conda env remove --name env_name
```

> Clone an existing environment
```bash
conda create --name clone_env_name --clone existing_env_name
```

> Export an existing environment
```bash
conda activate existing_env_name
conda env export > save_file_name.yml
```

> Recover environment from .yml file
```bash
conda env create -f environment_file_name.yml
``` 

## 2. how to set up a jupyter notebook server and remote access it from terminal?
### Prerequisite: anaconda installed on server/ internet access on server/ port connection(?)
> 1. login into server using ssh (local end)
```bash
ssh id@domain -p port_num
``` 

> 2. run jupyter notebook server (server end)
```bash
jupyter notebook --no-browser --port=port_num --NotebookApp.password=""
``` 

> 3. build port connection (local end)
```bash
ssh -p port_num -N -f -L localhost:local_port:localhost:server_port id@domain
``` 

> 4. open notebook in browser (local end)
```http
localhost:local_port
``` 

## 1. how to choose the ipython kernel for jupyter notebook?
It is a good habit to create a virtual env with anaconda when running some python code. The code can be 
```bash
conda create -n env_name python=3
```
when you activate the new env you create, you may use 
```bash
jupyter kernelspec list
```
to see which kernel is available right now. Sometimes the default kernel is not the python interpretor in the new env. A simple way to check is that:
in termial, you may run 
```bash
which python
python --version
```
which returns the path of the python interpretor and the python version. In notebook, run
```python
from platform import python_version
print(python_version())
```
```python
import sys
print(sys.executable)
```
which return similar things. It might be that you find the info you get from these two ways are different, which means notebook does not use the kernel of the new env. Easy way to fix it is:
First run 
```bash
conda list
```
see if ipykernel is already installed in the new env, if not, run
```bash
python -m pip install ipykernel
```
to install it. Then run 
```bash
python -m ipykernel install --user --name new_env_name --display-name "Python3 (new_env_name)"
```
After running this, when you want to create a new notebook from the browser, you will see there is an option shows "Python3 (new_env_name)".
