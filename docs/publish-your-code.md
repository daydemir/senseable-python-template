# Publish your code
This template is a starting point for researchers who want to write python code, use Jupyter notebooks, and potentially publish the code they have written for their research.

There are essentially three ways to publish your code so it can be reused (and potentially cited):

1. Publish the code as is in a repository
2. Publish a Python package to PyPI
3. Publish as peer-reviewed software (to [pyOpenSci](https://www.pyopensci.org) or the [Journal of Open Source Software](https://joss.theoj.org))



## Methods of publishing code

|Tool   |Description   |Supports   |
|---|---|---|
|[GitHub](https://github.com)  |Public repository. If structured and documented well, easy to share and reuse code.​  |Supports versioning and tagging releases.  |
|[Zenodo](https://zenodo.org), [Figshare](https://figshare.com)   |Formal research code archival.​   |Creates DOIs for uploaded code. Zenodo automates this using a GitHub integration.​   |
|[pyOpenSci](https://www.pyopensci.org)   |Community for open-source Python packages for scientific research.​   |Provides peer review, endorses packages, and promotes community discovery.​   |
|[Journal of Open Source Software](https://joss.theoj.org)   |Journal for simple publishing of code as a standalone paper. ​   |Indexed by Google Scholar. Software must be non-trivial (multi-month project).​   |

## Building a Python package

These instructions will be useful if you intend to release your module as a Python package on PyPI.

### How to decide

Would this module be useful to other researchers or developers? Releasing the reusable elements of your code as a package on PyPI makes it easy for others to use, and to have a formal way of releasing improvements over time. See more on python packages [here](https://www.pyopensci.org/python-package-guide/tutorials/intro.html).

If you add your repo to Zenodo, then you will have a unique DOI (separate from the DOI of any papers you've published) that can be cited by others when they use your library.

If you would like to have your package peer-reviewed and its visibility increased, you can consider submitting to [pyOpenSci](https://www.pyopensci.org) or the [Journal of Open Source Software](https://joss.theoj.org). pyOpenSci is a peer-review process that increases the visibility among the scientific community. The Journal of Open Source Software requires that the software be non-trivial by checking number of lines of code and the amount of time it took to write the software. More details on the submission requirements for the JOSS [here](https://joss.readthedocs.io/en/latest/submitting.html).

### Publishing the package

If you are ready to publish your module as a Python package, make sure that your git working tree is clean by running `git status` and ensuring that you see that there is nothing to commit.

#### Decide on a version
Every time you want to update the package, you'll need to decide what the version should be of the next package update. It is recommended that version updates adhere to semantic versioning standards. [More on semantic versioning available here](https://devhints.io/semver)

#### Prepare release metadata
Add a CODE_OF_CONDUCT. [pyOpenSci recommends](https://www.pyopensci.org/python-package-guide/documentation/repository-files/code-of-conduct-file.html#why-you-need-a-code-of-conduct) using the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).

Add a CHANGELOG, and update it with new releases. More details on good practices at [pyOpenSci](https://www.pyopensci.org/python-package-guide/documentation/repository-files/changelog-file.html#what-does-it-look-like).

Examples of the above can be found in this repository.


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
Follow these instructions to let Zenodo connect to your GitHub repository and automatically create a new DOI everytime you publish a new release version.

- Create a Zenodo account (either log in with GitHub, or connect with GitHub after creating the account)
- ⁠⁠Go to https://zenodo.org/account/settings/github/ and toggle on the repository you want to create the DOI for.
- ⁠In your GitHub repo, create a Tag to mark your release version (e.g. `v0.1.0`), and then create a Release using that tag.

Now, Zenodo will create a new DOI every time you create a new Release on GitHub. If desired, you can add a badge to the README to link to the latest Zenodo DOI using [these instructions](https://gist.github.com/seignovert/ae6771f400ca464d294261f42900823a).


### Consider submitting to pyOpenSci or JOSS

[pyOpenSci](https://www.pyopensci.org)

[Journal of Open Source Software](https://joss.theoj.org)



### More resources on publishing code
* https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content
* https://figshare.com
* https://github.com/audreyfeldroy/cookiecutter-pypackage
* https://the-hitchhikers-guide-to-packaging.readthedocs.io/en/latest/creation.html
* https://docs.python-guide.org/writing/structure/