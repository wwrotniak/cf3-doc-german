How to install Python virtualenv/virtualenvwrapper
==================================================

Virtualenv is a tool which is able to create isolated Python environments. It is mainly used to get rid of problems of dependencies and versions. 
It also does not include permission setup. Generally virtualenvwrapper is a kind of extension for virtualenv. It owns wrappers which are in charge of creating and deleting environments. It is useful supplement for our current subject.

For purposes of this guide we will use virtual machine **vm01** with operating system **Ubuntu 20.04 LTS**.

Log in to your PC and check python version (it should be preinstalled). Next step would be pip install:

::

  eouser@vm01:~$ python3 --version
 
  Python 3.8.10
 
  eouser@vm01:~$ sudo apt install python3-pip

Confirm the pip3 installation by invoke:

::

 eouser@vm01:~$ pip3 -V
 
 pip 20.0.2 from /usr/lib/python3/dist-packages/pip (python 3.8)

Install virtualenvwrapper via pip:

::

  eouser@vm01:~$ pip3 install virtualenvwrapper

Create a new directory to store your virtual environments, for example:

::

  mkdir .virtualenvs

Now we are going to modify **.bashrc** file by adding a row that will adjust every new virtual environment to use Python 3.
We will point virtual environments to the directory we created above (.virtualenvs) and we will also point to the locations of the virtualenv and virtualenvwrapper.
Open .bashrc file using editor, for example:

::

  vim ~/.bashrc

Navigate to the bottom of the .bashrc file and add following rows:

::
 
   #virtualenvwrapper settings:
   export WORKON_HOME=$HOME/.virtualenvs
   export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
   export VIRTUALENVWRAPPER_VIRTUALENV=/home/eouser/.local/bin/virtualenv
   source ./.local/bin/virtualenvwrapper.sh

After that save the .bashrc file. 

Now we've to reload the bashrc script, to do it execute command:

::

  source ~/.bashrc

If everything is set up properly, you should see following lines:

::

  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/premkproject 
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/postmkproject
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/initialize
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/premkvirtualenv
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/postmkvirtualenv
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/prermvirtualenv
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/postrmvirtualenv
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/predeactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/postdeactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/preactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/postactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/get_env_details
  
Now create your first virtual environment **'test'** with 'mkvirtualenv' command.

::

  eouser@vm01:~$ mkvirtualenv test
  created virtual environment CPython3.8.10.final.0-64 in 581ms
   creator CPython3Posix(dest=/home/eouser/.virtualenvs/test, clear=False, no_vcs_ignore=False, global=False)
    seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/home/eouser/.local/share/virtualenv)
     added seed packages: pip==21.3.1, setuptools==60.2.0, wheel==0.37.1
    activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/test/bin/predeactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/test/bin/postdeactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/test/bin/preactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/test/bin/postactivate
  virtualenvwrapper.user_scripts creating /home/eouser/.virtualenvs/test/bin/get_env_details

Now you should see name of your environment in the bracket before username, which means that you're working on your virtual environment.

::

  (test) eouser@vm01:~$ 

If you would like to exit current environment, just type the 'deactivate' command:

::

  (test) eouser@vm01:~$ deactivate
  eouser@vm01:~$

To start working on virtual environment type 'workon' command:

::

  eouser@vm01:~$ workon test
  (test) eouser@vm01:~$ 

To remove virtual environment invoke 'rmvirtualenv':

::

  eouser@vm01:~$ rmvirtualenv test
  Removing test...

To list all virtual environments use 'workon' or 'lsvirtualenv':

::

  eouser@vm01:~$ workon
  test-1
  test-2
  test-3
  eouser@vm01:~$ lsvirtualenv
  test-1
  ======
  test-2
  ======
  test-3
  ======
