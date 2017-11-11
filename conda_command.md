# Create and Remove conda environment
## Create from .yml file
conda env create -f xxx.yml
## Create directly
conda create -n xxx python=x.x
## Exporting the environment file
1. Activate the environment to export
2. conda env export > environment.yml
## Add built python module into sys.path
1. move module file into conda/env/xxx/lib/pythonx.x/site-packages/
2. write a .pth file 'module_file'
