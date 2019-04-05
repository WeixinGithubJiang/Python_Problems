# Python_Problems

## 1. how to choose the ipython kernel for jupyter notebook?
It is a good habit to create a virtual env with anaconda when running some python code. The code can be 
```python
conda create -n env_name python=3
```
when you activate the new env you create, you may use "jupyter kernelspec list" to see which kernel is available right now. Sometimes the default kernel is not the python interpretor in the new env. A simple way to check is that:
in termial, you may run "which python" and "python --version" which returns the path of the python interpretor and the python version. In notebook, run "from platform import python_version; print(python_version())" and "import sys; print(sys.executable)" which return similar things. It might be that you find the info you get from these two ways are different, which means notebook does not use the kernel of the new env. Easy way to fix it is:
First run "conda list" see if ipykernel is already installed in the new env, if not run "python -m pip install ipykernel" to install it. Then run "python -m ipykernel install --user --name new_env_name --display-name "Python3 (new_env_name)"". After running this, when you want to create a new notebook from the browser, you will see there is an option shows "Python3 (new_env_name)".
