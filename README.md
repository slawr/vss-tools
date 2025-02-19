# VSS Tools Usage

## Contents
1. Prerequisites
2. Project Setup
3. Run Tests
4. Use Project

## 1. Prerequisites
* Python 3.7 installed
* If the installation (pip install) is executed behind a (corporate) proxy, the following environments variables must be set: http_proxy and https_proxy (including authentication e.g., http://${proxy_username):$(proxy_password)@yourproxy.yourdomain)
* If you do not run with administration rights, you may need to configure pip target path to write to your user home directory or consider [using the `pipenv` method](#21-setup-with-pipenv).

```
On Unix and Mac OS X the configuration file is: $HOME/.pip/pip.conf
If the file does not exist, create an empty file with that name.

Add or replace the following lines:
[global]
target=/somedir/where/your/account/can/write/to

On Windows, the configuration file is: %HOME%\pip\pip.ini 
If the file does not exist, create an empty file with that name.

Add or replace the following lines:
[global]
target=C:\SomeDir\Where\Your\Account\Can\Write\To
```

* If you use a custom pip installation directory, set the `PYTHONPATH` environment variable to the directory that you set in the `pip.ini` file.

## 2. Project Setup
* Checkout vss-tools as submodule of the Vehicle Signal Specification repository (git clone --recurse-submodules -j8 https://github.com/GENIVI/vehicle_signal_specification.git)

### 2.1. Setup with `pipenv`
[pipenv](https://pypi.org/project/pipenv/) is a tool that manages a virtual environment and install the package and its dependencies, making the process much simpler and predictable, since the `Pipfile` states the dependencies, while `Pipfile.lock` freezes the exact version in use.

If [`pyenv` shell command](https://github.com/pyenv/pyenv) is not installed, use its [installer](https://github.com/pyenv/pyenv-installer) to get it:

```sh
curl https://pyenv.run | bash  # download and install
exec $SHELL                    # restart your shell using the new $PATH
```

Make sure Python version 3.8.5 is installed:
```sh
pyenv install 3.8.5  # install the versions required by Pipfile
```

Install this project and its dependencies in the local `.venv` folder in this project, then use it (`pipenv shell`):
```sh
export PIPENV_VENV_IN_PROJECT=1 # will create a local `.venv` in the project, otherwise uses global location
pipenv install --dev # install the development dependencies as well
pipenv shell         # starts a shell with configured to use the virtual environment
```

### 2.2. Setup using plain `pip install`
* RUN  ```pip install -e .``` from the vss-tools project root directory
* Run  ```pip install -r requirements.txt```  from the vss-tools project root directory

## 3. Run Tests
Run the following command in your root directory
* RUN ```pytest tests ```

## 4. Use Project

Folder structure for the example below
```bash
.
└── vehicle_signal_specification
    ├── VERSION
    ├── spec
    │   │   ├── VehicleSignalSpecification.id
    │   └── VehicleSignalSpecification.vspec
    ├──vss-tools
    ├── vspec2c.py
    ├── vspec2binary.py
    ├── vspec2csv.py
    ├── vspec2franca.py
    ├── vspec2json.py
    └── vspec2json.py
```

* CSV File generation -> vss.csv:
```sh
python ./vspec2csv.py -i:../tmp/asdasd ../spec/VehicleSignalSpecification.vspec vss.csv
```
