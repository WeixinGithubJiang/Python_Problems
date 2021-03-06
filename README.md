# Python Tips


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

> 2. activate the environment and check if ipykernel package has been installed
```bash
conda activate env_name
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

## 4. how to change python version with conda?
```bash
conda search python
```
```bash
conda install python=3.6.8(version_num)
```

## 5. how to interactively show a sequence of images?
```python
from ipywidgets import interact
import matplotlib.pyplot as plt

def viz(t):
  h = plt.imshow(example[:,:,t])
  plt.colorbar(h)
  plt.show()

interactive_plot = interact(viz,t=(min,max))
```

## 6. how to load/save data from/to a file?

> 1. save/load dictionary

>> yaml

```python
import yaml

with open(filename,'r') as f:
  data = yaml.load(f)
  
with open(filename,'w') as f:
  yaml.dump(data,f,default_flow_style=False)
```

## 7. how to plot?

>1. plot with pylab
```python
import matplotlib.pylab as pylab

pylab.rcParams['figure.figsize'] = width, height # set the size of the figure
```

## 8. how to load/save image?

>1. with opencv
```python
import cv2
image = cv2.imread(filename,1) # 1 means color image with channel order BGR
```

>2. with PIL
```python
from PIL import Image
image = Image.open(filename).convert("RGB") # color image with channel order RGB
image.save(filename)
```

## 9. how to manipulate the attributes in a class?

>1. class to dict
```python
dict = vars(class_name)
```

## 10. python class

```python
class ExampleClass():
  def __init__(self,**kwargs):
    pass
    
  def __getitem__(self, idx):
    return xxx
    
  def __len__(self):
    return int_value
    
  def __call__(self, **kwargs):
    return xxx
```

## 11. python tricks
>1. run python in the background
```bash
nohup bash script.sh &
```

>2. run jupyter notebook in the background
```bash
jupyter notebook &
```

## 11. import self-developed module

>1. create a blank __init__.py in the folder

>2. when importing, use "." to represent current folder, use ".." to represent parent folder, use "."xN to represent (N-1) parent folder.

>3. most important, you can never go to the folder that is the parent folder of the main.py
```python
--base
----folder_1
------main.py
------folder_1_1
--------__init__.py
--------func_1_1.py
----folder_2
------__init__.py
------func_2.py
----__init__.py
```
suppose we are trying to import module from func_1_1.py in the main.py, it would fail if func_1_1.py tries to import module from func_2.py, because the root folder is folder_1, folder_2 is outside of folder_1. If we move main.py to the folder of base, than it works.
