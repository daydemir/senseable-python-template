# [DRAFT] A Senseable Python Template

[View on GitHub](https://github.com/daydemir/senseable-python-template)

This guide provides recommendations for how to structure our Python projects developed within the MIT Senseable City Lab. The goal of this structure is to make it easy to make the work you do easier to review and reproduce, and the code you write easier to share and publish.

This guide strongly recommends that the [cookiecutter-data-science](https://cookiecutter-data-science.drivendata.org) template be used to create the skeleton for your project. Using this template will create an initial project structure that can be shared among projects in the lab, but can also be modified if needed.

This template is implemented using [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/README.html), a command line utility to quickly build out your project structure. There are [many different cookiecutter templates](https://github.com/search?q=cookiecutter&amp%3Btype=Repositories&type=repositories&s=stars&o=desc) that can be used for different project setups with different focuses and strengths. We specifically recommend the template *cookiecutter-data-science* because it is widely adopted for use in research environments and presents an easy-to-share and flexible starting off point. As stated in their documentation:
> *A logical, flexible, and reasonably standardized project structure for doing and sharing data science work.*

It is recommended that you read about [the opinions reflected in the template](https://cookiecutter-data-science.drivendata.org/opinions/), and use them to guide your own work and to inform any choice to deviate from the recommended structure.

### Resulting Directory Structure
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


