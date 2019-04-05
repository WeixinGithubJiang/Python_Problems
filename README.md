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

## 3. how to check python version and path?
> in terminal
```bash
which python
python --version
```

> in notebook/script
```python
from platform import python_version
print(python_version())
```
```python
import sys
print(sys.executable)
```

## 4. how to create or remove ipython kernel for jupyter notebook?
> 1. check existing ipython kernel
```bash
jupyter kernelspec list
```

> 2. check if ipykernel package has been installed
```bash
conda list
```
> if not, install it
```bash
python -m pip install ipykernel
```

> 3. create a new kernel with an existing env
```bash
python -m ipykernel install --user --name new_env_name --display-name "Python3 (new_env_name)"
```

> 4. remove an existing kernel
```bash
jupyter kernelspec remove ipykernel_name
```

