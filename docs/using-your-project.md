# Working On Your Project

See the below sections for more information and best practices.

## Version Control

Version control makes it easy to go back to previous versions of your project and create different branches for different lines of work. When connected to a remote repository on GitHub, this makes it so even if your local files are lost or corrupted, you can always retrieve the latest versions from the remote repository.

If you have not used **git** and GitHub before, you may find it useful to download the [GitHub Desktop Application](https://desktop.github.com/download/). This provides a user interface to easily see what has changed and make commits. Many code editors (like Visual Studio Code) will also have some **git** tools integrated into their interface.

It is best practice to commit and push your changes to the remote repository frequently. Include messages that are short and that describe the included changes.

If you would like a crash course on how to use **git**, you may try [Learn Git Branching](https://learngitbranching.js.org).

## Make
As part of this template, a `Makefile` is created with some initial scripts, called "recipes", that can be used to simplify set up and reuse of your repository.

See [Make as a task runner](https://cookiecutter-data-science.drivendata.org/using-the-template/#make-as-a-task-runner) for more information.

## Virtual Environments

During the setup, you will have created a virtual environment where your specified version of python and dependencies will be housed to run your python code. The use of virtual environments keeps dependencies and python versions from clashing between different projects, and makes it easier to quickly run someone else's project when needed.

In your code editor, be sure to select the local virtual environment you created. It will likely be in a folder called `.venv` located within your project folder.

## Structuring your code

It is recommended that you put the "logic" of your workflow into the module folder created by the template, and reference that module in any scripts or notebooks as needed.

This makes it easier to...

1. Share the core components of your code and eventually publish it as a package
2. Separate different types of code conceptually
3. Have someone else come in and review your code
4. Publish your code as a package if so desired

The module folder will be the one with the name you chose at setup and has the `__init__.py` file inside it. 

See [Refactoring code into shared modules](https://cookiecutter-data-science.drivendata.org/using-the-template/#refactoring-code-into-shared-modules) for more information and how to turn on `autoreload` so your Jupyter Notebooks always use the up-to-date code from your module.

#### Jupyter Notebooks

It is recommended that Jupyter Notebooks be used as a way to explore and visualize the data, and not where the actual data manipulation and "logic" happens. It is reasonable to experiment with more functional changes in your notebooks, but it is recommended that the data manipulation code eventually be moved to the module.

One way to think about this is: could someone else ignore your notebooks and use only your module code to reproduce your results? If not, then it is useful to refactor your code to make that possible. If you plan to publish your module as a package, this will be necessary.

In order to access your module code instantly without having to reload your notebook, add a cell to the top of your notebook containing the following code.
```python
%load_ext autoreload
%autoreload 2
```

See [Open a notebook](https://cookiecutter-data-science.drivendata.org/using-the-template/#open-a-notebook) for more information and guidance on a useful notebook naming convention.
 
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

*If you do not expect to publish a Python package or share your code with others, this distinction is not very important and you can add all dependencies directly to the whole project using the steps above.*

#### Development environment dependencies with requirements.txt
If you use a `requirements.txt` file for your dependencies, you can create a second `requirements-dev.txt` file to manage development environment dependencies. A quick guide on how to do this can be found [here](https://www.packetcoders.io/pip-trick-for-splitting-dev-requirements/).

#### Development environment dependencies with Conda
In order to set up different environments and sets of dependencies, see [Managing Environments in Conda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

#### Development environment dependencies with Poetry
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

See [Add your data](https://cookiecutter-data-science.drivendata.org/using-the-template/#add-your-data) for more information on how to use the data syncing recipes provided with the `Makefile`.

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