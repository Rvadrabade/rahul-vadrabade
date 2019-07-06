======
Sphinx
======

Sphinx is a tool that makes it easy to create intelligent and beautiful documentation using **reStructuredText** .

.. contents::
   :local:

Sphinx Resources
================

Resources to Learn Sphinx. 

* `Sphinx <http://www.sphinx-doc.org/en/master/>`_
* `Read the Docs - Getting started with Sphinx <https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html>`_ 
* `Sphinx with github webpage <https://runawayhorse001.github.io/SphinxGithub/index.html>`_
* Youtube 

Installation
============

Ubuntu/Linux

.. code-block:: bash
    
    apt-get install python3-sphinx

To get latest version, it is advisable to use python virtual environment as follows

.. code-block:: bash
    
    sudo apt install -y python3-venv
    cd ~
    mkdir Virt_Env
    cd Virt_Env/
    python3 -m venv sphinx
    source sphinx/bin/activate
    pip install -U sphinx
    sudo gedit alias VSphinx='source ~/Virt_Env/sphinx/bin/activate'  
    //set alias & from next time use 'VSphinx' to activate virtual environment- 'deactivate' to exit.//
    deactivate

Getting Started
===============

.. code-block:: bash
    
    sphinx-quickstart 

Just answer to  project name and author, keep rest to default or unanswered.

HTML Output
===========

.. code-block:: bash
    
    make html

Open "_build/html/index.html" in chrome or firefox to view output.

Theme 
=====

Detailed Information is available `here <https://www.sphinx-doc.org/en/stable/theming.html>`_

To change default theme, edit **conf.py** and change to different available theme.

.. code-block:: python
    
    html_theme = 'alabaster' # classic/sphinxdoc/scrolls/agogo
    
