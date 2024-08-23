# Getting Started

## Prerequisites

In order to get started, you'll need the following:

1. A basic understanding of **git** and a GitHub account.
2. A command line interface to run commands (often Terminal on macOS and Linux, and Command Prompt or PowerShell on Windows).
3. An installation of **pipx** or **pip**.

## Setup

Below, we walk through how to quickly set up your new project. This README provides two different setup flows for different expertise and preference profiles. If you would prefer, you are welcome to deviate from these setup flows and make choices as you see fit. More details can be found in [the documentation](https://cookiecutter-data-science.drivendata.org).
### *Standard*
- Allows you to choose between using **pip** & **venv** **conda** for dependency and virtual environment management
- If you plan to deploy a package, **Flit** will be the default tool to use.
- This set up will be best for those who want to use the more traditional `requirements.txt` file for dependency management, or for users who want more flexibility for more complex projects.
### *Poetic*
- Basic setup with a few extra steps to start using **Poetry** for all of dependency management, virtual environment generation, and package publication.
- This setup may be simpler for those who plan to only use Python code and packages in their project.
- The downside of this set up is that sharing code with other users takes an extra step if they do not have (and do not want to use) **Poetry** for dependency management.

While **Poetry** can be set up for the *Standard* installation as well, the *Poetic* set up best takes advantage of the unification that *Poetry* provides.


### Install `ccds`
`cookiecutter-data-science` uses a command line tool called `ccds` to run the setup.
Install ccds
With pipx (recommended)
```shell
pipx install cookiecutter-data-science
```
With pip
```shell
pip install cookiecutter-data-science
```
## Shared Setup
Run `ccds` from the parent directory where you want your project stored
```shell
# From the parent directory where you want your project
ccds
```
Begin filling out the template. These can all be changed later.
- Enter the `project_name`
- Enter the `repo_name`. Choose a name that has not been used for a repository on your GitHub account.
- Enter the `module_name`. If you choose to export your standalone code, this will be the name of the Python package.
- Enter the `author_name`. This can be your full name.
- Enter the `description`.
- Enter the `python_version_number`. As of mid-2024, using a version >=3.9 is recommended.
- Select the `dataset_storage`.
  - For large datasets or CSVs, it is recommended they be stored on a cloud storage if possible. If you have details for those cloud storage providers, go ahead and choose the one you use and provide the credentials.
  - If you do not currently use one of those providers but plan to do so eventually, you can select it now and use the default values for the credentials. This will create the convenient scripts in the `Makefile`, and later when you set up the cloud storage you can modify the details in the `Makefile` to reflect the relevant credentials (bucket name, etc).
  - Eventually, we will recommend using the SCL Network Attached Storage (NAS) that is hosted in Cambridge for data storage. See the section **Using the SCL Network Attached Storage (NAS)** below for instructions on how to set up the NAS for data storage. If you will use the SCL NAS, select `none` for `dataset_storage`.

For the remaining choices, refer to the chosen setup flow below.
## *Standard* Setup
### Complete template setup
- Select the `environment_manager` of your choice. Select `none` if you wish to set up an environment manager that is not listed.
- Select the `dependency_file` of your choice.
- For `pydata_packages`, select `basic` if you would like the following packages added from the start: ipython, jupyterlab, matplotlib, notebook, numpy, pandas, scikit-learn.
- Choose `open_source_license`. `MIT` is recommended if the repository will be public.
- Choose `docs`. If you would prefer to use [Read the Docs](https://about.readthedocs.com) instead, you can select `none` and set that up independently.
- Choose `code_scaffold`. It is recommended to select `yes` to include some useful boilerplate code. If you are an experienced Python developer, you may prefer to avoid the prebuilt boilerplate and select `no`.

### Create a Python virtual environment
If you used the *Standard* setup, you can use the following command to create a new environment using a recipe provided by the template in the Makefile:
```shell
make create_environment
```
You will then need to activate that environment using the environment manager you've chosen. See [Create a Python virtual environment](https://cookiecutter-data-science.drivendata.org/using-the-template/#create-a-python-virtual-environment) for more information.

## *Poetic* Setup
### Complete template setup
- For `environment_manager`, select `none`.
- For `dependency_file`, select `requirements.txt`. At the end of the setup, we will remove this and use `pyproject.toml` instead.
- For `pydata_packages`, select `none`.
- Choose `open_source_license`. `MIT` is recommended if the repository will be public.
- Choose `docs`. If you would prefer to use [Read the Docs](https://about.readthedocs.com) instead, you can select `none` and set that up independently.
- Choose `code_scaffold`. It is recommended to select `yes` to include some useful boilerplate code. If you are an experienced Python developer, you may prefer to avoid the prebuilt boilerplate and select `no`.

### Set up Poetry
In the *Poetic* setup flow, we will manage dependencies using [Poetry](https://python-poetry.org). This will make it so you only need one tool to cover the following: manage dependencies, create local environments, and publish your package to PyPI.

#### Install Poetry
Simple installation with `pipx`
```shell
pipx install poetry
```
See detailed instructions [here](https://python-poetry.org/docs/#installation).
#### Select Python version
Use the Python version specified in the template setup.
```shell
python env use 3.12
```
or specify the path directly
```shell
poetry env use /path/to/preferred/python/version
```
You can see the path to your Python version by running `which python3.12` on macOS / Linux, or `py -0p` on Windows.
#### Configure in-project virtual environments
```shell
poetry config virtualenvs.in-project true
```
#### Install to download dependencies and setup environment
```shell
poetry install
```
This creates a virtual environment that stored in the project folder at `/.venv`. This folder is hidden to git thanks to the `.gitignore` file, so your local environment does not take up storage in GitHub.
This makes it so if someone else wants to run your code, they can clone or download your repository from GitHub, and run `poetry install` themselves to have a copy of the virtual environment you are using.

#### Delete the requirements.txt

In order to avoid confusion, it is recommended that you delete the `requirements.txt` file as it will remain out of date.

### pyproject.toml
It will be useful to familiarize yourself with the `pyproject.toml` file. This file is the current best practice method for defining project parameters and dependencies. Poetry will populate and use this file as you add dependencies. Other build tools like Flit, Hatch, and Setuptools also use the `pyproject.toml`.
You can read more about https://python-poetry.org/docs/pyproject/
#### What happened to requirements.txt?
When using Poetry, all your dependencies are managed in the `pyproject.toml` file.
It is possible to use a `requirements.txt` to populate your dependencies in your `pyproject.toml` with Poetry.
```shell
poetry add $(cat requirements.txt)
```
Similarly, it is possible to export your dependencies from the `pyproject.toml` to a `requirements.txt` if needed.
```shell
# Export dependencies to requirements.txt
poetry export -f requirements.txt --output requirements.txt

# If you want to include development dependencies as well
poetry export -f requirements.txt --output requirements.txt --dev
```
## Connect to GitHub
Whichever setup flow you chose, your final step will be to connect your local folder to a new repo on GitHub.

In order to complete this step, ensure you have the [GitHub command-line interface (CLI)](https://cli.github.com) installed. Then you can run the following commands to connect your local repository to GitHub.

```shell
# Navigate to your newly created project folder
cd newly-created-project-folder

git init                        
git add .                       
git commit -m "CCDS defaults"   

# Use GitHub CLI to create a new repo on your account. This will prompt you for further details.
gh repo create
```

Your project is now ready to go!