This document describes how to setup the provided Python code
(in the directory ``python_skeleton/OIDCRPExample/``).

# Prerequisites

* Python 2.7 or 3.4.3
* Homebrew if using Mac
* PyCharm Community Edition: https://www.jetbrains.com/pycharm/download/

# Setup

## System setup

On Mac:

* Install pip: ( https://pip.pypa.io/en/stable/installing/ )

  ```
  curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
  sudo -H python get-pip.py
  ```
* Install libffi:

  ```
  brew install libffi
  ```  
    
On CentOS:

    yum install libffi-devel
        
On Ubuntu:

    apt-get install python-dev python-pip libssl-dev libffi-dev libsasl2-dev
        
## Project setup

### Optional pre-setup
1. Setup a [virtual environment](http://docs.python-guide.org/en/latest/dev/virtualenvs/).

```
sudo -H pip install virtualenv
````
2. Activate the new virtual environment.
(Note that this 'project' folder was created at the same directly level as the unzip )
```
mkdir project
cd project/
virtualenv venv
. ./venv/bin/activate
```
### Code setup
1. Create a working copy to manipulate
  ```
  cp -r ../openid_course-master/python_skeleton/OIDCRPExample .
  ````
2. Install the dependencies: ``pip install -r requirements.txt``
  ```
  cd OIDCRPExample
  sudo -H pip install -r requirements.txt
  ```
3. If on mac, to prevent this error when running the runner.py command: ImportError: No module named http_cookiejar do this update
  ```
  sudo -H pip install --upgrade six
  ```
4. Test that the project runs by:
  1. **Setting proper paths**

  Edit the settings for the OIDC client by editting the file ``oidc_rp/client.py`` and specify the path to the  directory containing all   necessary files. These are ``client.json``, ``index.html``, etc.  These files are located in the root of the repository you unzipped.
    The variable to edit is  ``ROOT_PATH`` in the ``Client`` class.  Save the file.
  
  2. **Starting a local webserver on port 8090 as the relying party.** 

  Note: This port may be used later in the Apache configuration and may result in collisions if you are running the vagrant managed instance of apache.  If so, stop the instance with: `` vagrant suspend``
Start the  Relying Party (RP) webserver, be sure you are in the ``OIDCRPExample`` directory and execute:
``python runner.py``.
  
  3. **Using Firefox, verify the RP is running by opening the URL at [http://localhost:8090](http://localhost:8090)** 
  
      Firefox is required as Google Chrome has some issues with CherryPy's sessions.
  
### Start adding to the skeleton code to get a working RP:
  1. The missing parts are marked with ``TODO`` in ``oidc_rp/client.py``.
  2. Read the [Python Cookbook](https://dirg.org.umu.se/static/pyoidc/howto/rp.html) for more
     information about how to use the pyOIDC OpenID Connect library.
  3. Make sure to delete cookies and cached data in the browser while
     testing to avoid strange results (e.g. due to the browser caching
     redirects, etc.).
