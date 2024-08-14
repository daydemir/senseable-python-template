# Senseable Python Template

This template is a starting point for researchers who want to write python code, use Jupyter notebooks, and potentially publish the code they have written for their research.

There are essentially three ways to publish your code so it can be reused (and potentially cited):

1. Publish the code as is in a repository
2. Publish a Python package to PyPI
3. Publish as peer-reviewed software (to [pyOpenSci](https://www.pyopensci.org) or the [Journal of Open Source Software](https://joss.theoj.org))

If you hope to do either (2) or (3), this template provides some guidance on how to structure your code for package deployment and for peer review. If you only plan to do (1), this can still be a useful template to get started with.


## Prerequisites

1. A basic understanding of git and a GitHub account.
2. A command line interface to run commands (often Terminal on macOS and Linux, and Command Prompt or PowerShell on Windows)


## Getting Started

### Use this Template

Click the `Use this template` button on the top right of this repo and select `Create a new repository`.

Once the new repository is created on your own GitHub account, you can clone your repository to your local computer.

### Setup Poetry

In order to maintain clean virtual environments, we recommend managing your dependencies using [Poetry](https://python-poetry.org). This will make it so you only need one tool to cover the following: managing dependencies, creating local environments, and publishing your package to PyPI.

#### Install Poetry 

Simple installation with `pipx`
```shell
pipx install poetry
```

See detailed instructions [here](https://python-poetry.org/docs/#installation).

#### Configure in-project virtual environments
```shell
poetry config virtualenvs.in-project true
```

#### Run install to create virtual environment
```shell
poetry install
```

This creates a virtual environment that stored in the project folder at `/.venv`. This folder is hidden to git thanks to the `.gitignore` file, so your local environment does not take up storage in GitHub.

This makes it so if someone else wants to run your code, they can clone or download your repository from GitHub, and run `poetry install` themselves to have a copy of the virtual environment you are using.


## Writing your code

### Select environment

### Adding dependencies

### Using Jupyter Notebooks

### (Pending) Using the SCL BIZON workstation

[Instructions for connecting your codebase to the BIZON interface go here]

## Building a Python package

These instructions will be useful if you intend to release your code as a Python package on PyPI.

### How to decide

Would your code be useful to other researchers or developers? Releasing the reusable elements of your code as a package on PyPI makes it easy for others to use, and for you (or others) to to improve the code over time. See more on python packages [here](https://www.pyopensci.org/python-package-guide/tutorials/intro.html).

If you add your repo to Zenodo, then you will have a unique DOI (separate from the DOI of any papers you've published) that can be cited by others when they use your library.

If you would like to have your package peer-reviewed and its visibility increased, you can consider submitting to [pyOpenSci](https://www.pyopensci.org) or the [Journal of Open Source Software](https://joss.theoj.org). pyOpenSci is a peer-review process that increases the visibility among the scientific community. The Journal of Open Source Software requires that the software be non-trivial by checking number of lines of code and the amount of time it took to write the software. More details on the submission requirements for the JOSS [here](https://joss.readthedocs.io/en/latest/submitting.html).

### (Pending) Code structure for packaging

[Instructions ]

### Prepare release metadata

Update the following content:
* Update year and name in LICENSE
* Review and update CODE_OF_CONDUCT as desired. This is prefilled using the language provided by the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/) as recommended by the [pyOpenSci documentation](https://www.pyopensci.org/python-package-guide/documentation/repository-files/code-of-conduct-file.html#why-you-need-a-code-of-conduct).
* Note the CHANGELOG, and plan update it with new releases. More details on good practices at [pyOpenSci](https://www.pyopensci.org/python-package-guide/documentation/repository-files/changelog-file.html#what-does-it-look-like).
 
### Publishing your package
If you are ready to publish your package, make sure that your git working tree is clean by running `git status` and ensuring that you see that there is nothing to commit. All 

#### Decide on a version
Every time you want to update the package, you'll need to decide what the version should be of the next package update. `poetry` handles incrementing the versions for you, you just need to decide if the update is a `patch`, a `minor` update, or a `major` update. Any update that would break for existing users of the package is always considered `major`. [More semantic versioning available here](https://devhints.io/semver).

This template has an initial version of `0.1.0`. You can always see the existing version of the package by checking the `pyproject.toml` file, or by running
```shell
poetry version
```

#### Use poetry to publish

##### First version
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

