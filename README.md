# A Senseable Python Template

In order to get started with a new Python project at the MIT Senseable City Lab, it is strongly recommended that [cookiecutter-data-science](https://cookiecutter-data-science.drivendata.org) is used to create the skeleton for your project.

[Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/README.html) is a tool to quickly build out your project structure using a command line utility. There are [many different cookiecutter templates](https://github.com/search?q=cookiecutter&amp%3Btype=Repositories&type=repositories&s=stars&o=desc) that can be used for different project setups with different focuses and strengths. We specifically recommend the template *cookiecutter-data-science* because it is widely adopted for use in research environments and presents an easy-to-share and flexible starting off point. As stated in their documentation:
> *A logical, flexible, and reasonably standardized project structure for doing and sharing data science work.*

It is recommended that you read about [the opinions reflected in the template](https://cookiecutter-data-science.drivendata.org/opinions/), and use them to guide your own work and to inform any choice to deviate from the recommended structure.

### The Resulting Directory Structure
This is the directory structure that is created after completing the setup with this template.
```
├── LICENSE            <- Open-source license if one is chosen
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default mkdocs project; see www.mkdocs.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── pyproject.toml     <- Project configuration file with package metadata for 
│                         {{ cookiecutter.module_name }} and configuration for tools like black
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.cfg          <- Configuration file for flake8
│
└── {{ cookiecutter.module_name }}   <- Source code for use in this project.
    │
    ├── __init__.py             <- Makes {{ cookiecutter.module_name }} a Python module
    │
    ├── config.py               <- Store useful variables and configuration
    │
    ├── dataset.py              <- Scripts to download or generate data
    │
    ├── features.py             <- Code to create features for modeling
    │
    ├── modeling                
    │   ├── __init__.py 
    │   ├── predict.py          <- Code to run model inference with trained models          
    │   └── train.py            <- Code to train models
    │
    └── plots.py                <- Code to create visualizations   
```

# Getting Started

## Prerequisites

In order to get started, you'll need the following:
1. A basic understanding of **git** and a GitHub account.
2. A command line interface to run commands (often Terminal on macOS and Linux, and Command Prompt or PowerShell on Windows)
3. An installation of **pipx** or **pip**

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

For the remaining choices, refer to the setups below.
## *Standard* Setup
### Complete template setup
- Select the `environment_manager` of your choice. Select `none` if you wish to set up an environment manager that is not listed.
- Select the `dependency_file` of your choice.
- For `pydata_packages`, select `basic` if you would like the following packages added from the start: ipython, jupyterlab, matplotlib, notebook, numpy, pandas, scikit-learn.
- Choose `open_source_license`. `MIT` is recommended if the repository will be public.
- Choose `docs`. If you would prefer to use [Read the Docs](https://about.readthedocs.com) instead, you can select `none` and set that up independently.
- Choose `code_scaffold`. It is recommended to select `yes` to include some useful boilerplate code. If you are an experienced Python developer, you may prefer to avoid the prebuilt boilerplate and select `no`.
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
#### What happened to `requirements.txt`?
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

# Best Practices
See the below sections for more information and best practices.
## Make
As part of this template, a `Makefile` is created with some initial scripts that can be used to simplify set up and reuse of your repo.

## Version Control

Version control makes it easy to go back to previous versions of your project and create different branches for different lines of work. When connected to a remote repository on GitHub, this makes it so even if your local files are lost or corrupted, you can always retrieve the latest versions from the remote repository.

If you have not used **git** and GitHub before, you may find it useful to download the [GitHub Desktop Application](https://desktop.github.com/download/). This provides a user interface to easily see what has changed and make commits. Many code editors (like Visual Studio Code) will also have some **git** tools integrated into their interface.

It is best practice to commit and push your changes to the remote repository frequently. Include messages that are short and that describe the included changes.

If you would like a crash course on how to use **git**, you may try [Learn Git Branching](https://learngitbranching.js.org).

## Structuring your code
#### Jupyter Notebooks

## Dependency Management
If the *Standard* setup was used, you can use the dependency manager of your choice (likely `pipx` or `conda`), and the file of your choice as well (likely `requirements.txt`).
If the *Poetic* setup was used, you can add packages using the following command in the command line:
```shell
poetry add numpy
```
See more details on how to add dependencies with **Poetry** [here](https://python-poetry.org/docs/cli/#add).

### Development environment dependencies
When adding dependencies, it is important to know if the dependency should be added to the whole project, or just to the development environment. 

If a package is being added to the whole project, it should be one that is required for the core code to run. The easiest way to think about this is to decide, *if* I were publish the core code in this project as a package, would this dependency need to be bundled in the package? If yes, then add the dependency to the whole project using the standard commands above.

If a dependency is only used for some extra work that you are doing with your core code or for extra tooling, and is not a dependency that your core code directly uses, then you can add that package to your development environment. This makes it so when you are sharing your code or publishing a package, it is clear which packages are required to run your code and extraneous dependencies are not unnecessarily bundled in. Some standard examples of development environment dependencies include `ipykernel` and `notebooks` for Jupyter Notebooks, since notebooks would not likely be considered part of a core module to be reused by others.

**If you do not expect to publish a Python package or share your code with others, this distinction is not very important and you can add all dependencies directly to the whole project using the steps above.**

#### Development dependencies with requirements.txt
If you use a `requirements.txt` file for your dependencies, you can create a second `requirements-dev.txt` file to manage development environment dependencies. A quick guide on how to do this can be found [here](https://www.packetcoders.io/pip-trick-for-splitting-dev-requirements/).

#### Development environment dependencies with Conda
In order to set up different environments and sets of dependencies, see [Managing Environments in Conda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

#### Development dependencies with Poetry
In **Poetry**, you can use *groups* to manage dependencies for different environments.
```shell
poetry add ipykernel --group dev
```
See [Dependency Groups in Poetry](https://python-poetry.org/docs/managing-dependencies/#dependency-groups) for more information.

## Data Management
Generally, it is important to keep your work reproducible. This means that given an initial dataset and your code, it should be possible to recreate all the intermediary steps and data outputs. This makes it possible for someone else to come in later and use your code to reproduce the results you've achieved.

For this reason, this template uses the following structure within the `data` folder
```
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
```
### Data Storage
It is preferred that the datasets be stored on the Senseable NAS, or on some form of cloud storage (hence the `dataset_storage` option at initial set up).
The `data` folder is included in the `.gitignore` file by default, so no files in the data folder will be synced to GitHub. This is generally good practice in order to keep large data files off of GitHub. GitHub will reject files over 100MB.
If you think it is important to include the data files in GitHub, you can modify the `.gitignore` as needed. If your files are larger than a few MB, it is recommended to use [git-lfs](https://git-lfs.com) to keep your git history lean and repo fetching fast. Be mindful that storing the datasets on a public GitHub repository will make the datasets themselves public as well.
### Using the SCL Network Attached Storage (NAS)
[Pending instructions on connecting your data to the Senseable NAS]

## Secret Keys and Tokens
API keys or access tokens you've generated for yourself should be hidden from git and not be uploaded to GitHub. If you upload them to a public repo, even if you remove them in a future commit they will be compromised and should be deleted.
Instead, store it locally in a file that is ignored by git and thus will not be uploaded to GitHub. The standard way to do this is to create a `.env` file in the folder of your project and add your API key. The `.env` file is already included in the `.gitignore` of this template.

Create the `.env` and add your API keys as needed:

```shell
EXAMPLE_API_KEY="your-secret-api-key-here"
ANOTHER_API_KEY="another-super-secret-key-here"
```

Once this file is created, you can use the `dotenv` package to access your token from your local environment

```python
import dotenv

dotenv.load_dotenv()
api_key = os.getenv('EXAMPLE_API_KEY')
# use api_key wherever you would use your API key normally
```
If you chose `yes` on the `code_scaffolding` option, you should see `load_dotenv()` being called in the generated `config.py` file. That would be a good place to retrieve the environment variables to make them available to the rest of your code.

## Using SCL BIZON
[Pending instructions for how to connect to and use the SCL BIZON workstation]

# Publish your code
This template is a starting point for researchers who want to write python code, use Jupyter notebooks, and potentially publish the code they have written for their research.

There are essentially three ways to publish your code so it can be reused (and potentially cited):

1. Publish the code as is in a repository
2. Publish a Python package to PyPI
3. Publish as peer-reviewed software (to [pyOpenSci](https://www.pyopensci.org) or the [Journal of Open Source Software](https://joss.theoj.org))


## Building a Python package

These instructions will be useful if you intend to release your code as a Python package on PyPI.

### How to decide

Would your code be useful to other researchers or developers? Releasing the reusable elements of your code as a package on PyPI makes it easy for others to use, and for you (or others) to to improve the code over time. See more on python packages [here](https://www.pyopensci.org/python-package-guide/tutorials/intro.html).

If you add your repo to Zenodo, then you will have a unique DOI (separate from the DOI of any papers you've published) that can be cited by others when they use your library.

If you would like to have your package peer-reviewed and its visibility increased, you can consider submitting to [pyOpenSci](https://www.pyopensci.org) or the [Journal of Open Source Software](https://joss.theoj.org). pyOpenSci is a peer-review process that increases the visibility among the scientific community. The Journal of Open Source Software requires that the software be non-trivial by checking number of lines of code and the amount of time it took to write the software. More details on the submission requirements for the JOSS [here](https://joss.readthedocs.io/en/latest/submitting.html).

### Code structure for packaging


 


### Publishing the package
If you are ready to publish your package, make sure that your git working tree is clean by running `git status` and ensuring that you see that there is nothing to commit.

#### Decide on a version
Every time you want to update the package, you'll need to decide what the version should be of the next package update. It is recommended that version updates adhere to semantic versioning standards. [More on semantic versioning available here](https://devhints.io/semver)

#### Prepare release metadata
Add a CODE_OF_CONDUCT. [pyOpenSci recommends](https://www.pyopensci.org/python-package-guide/documentation/repository-files/code-of-conduct-file.html#why-you-need-a-code-of-conduct) using the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).

Add a CHANGELOG, and update it with new releases. More details on good practices at [pyOpenSci](https://www.pyopensci.org/python-package-guide/documentation/repository-files/changelog-file.html#what-does-it-look-like).


#### Publishing with Poetry
If you are using Poetry `poetry` handles incrementing the versions for you, you just need to decide if the update is a `patch`, a `minor` update, or a `major` update. Any update that would break for existing users of the package is always considered `major`.

This template has an initial version of `0.1.0`. You can always see the existing version of the package by checking the `pyproject.toml` file, or by running
```shell
poetry version
```

#### First version
For the first time you publish a package, you need to create an account at [PyPI] generate an API token on your account. After generating the token, copy it and connect it to `poetry` using the following command
```shell
poetry config pypi-token.pypi YOUR-API-TOKEN
```

#### For all releases
Run the following commands to publish a new `major` update to your package.

```shell
poetry version major             #if our current version is 0.1.0, this bumps the package version to 1.0.0
git commit -am 'version bump'    #commit the version update to git
git push                         #push the updated version to GitHub 
poetry build                     #creates the artifacts we need for the python package
poetry publish                   #uploads the package to PyPI
```

#### Create a tag and release
It is good practice to create a release on GitHub to mark an update to the package. This ensures that you know what code is associated with what package version, and is required if you want to use Zenodo's automatic integration with GitHub.

```shell
poetry version     #prints the current version, say 1.0.0
git tag v1.0.0     #standard practice is to prefix version tags with `v`
git push --tags    #push the tag to GitHub
```

After your tag is pushed, you can go to the Tags list on your GitHub, then switch to the Releases list, and create a new Release. Use the tag you just uploaded to create a new release with the same version. It is best practice to describe the changes included in this release in the description.

#### (Optional) Publish on Zenodo
...

### (Pending) Submitting to pyOpenSci or the Journal of Open Source Software

...

### More resources on publishing 
* https://github.com/microsoft/python-package-template/blob/main/README.md
* https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content
* https://github.com/kennethreitz/setup.py?tab=readme-ov-file
* https://github.com/navdeep-G/setup.py
* https://github.com/navdeep-G/samplemod?tab=readme-ov-file
* https://figshare.com
* https://github.com/audreyfeldroy/cookiecutter-pypackage
* https://the-hitchhikers-guide-to-packaging.readthedocs.io/en/latest/creation.html
* https://docs.python-guide.org/writing/structure/


## SCL Published Packages

[B++, Titus Venverloo](https://github.com/Tvenver/Bplusplus) (see branch `package`)