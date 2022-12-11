# Github pages with sphinx

## Create quick start template
    
   $ sphinx-quickstart
   > Separate source and build directories (y/n) [n]: n
   Finished: An initial directory structure has been created.
     

##  Create sphinx-template

1. Install theme
    ```sh
    pip install yummy-sphinx-theme
    ```
2. Set the following in your existing Sphinx documentation’s conf.py file:
    ```sh
    html_theme = 'yummy_sphinx_theme'
    ```