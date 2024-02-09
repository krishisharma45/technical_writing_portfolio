# NLP Text Summarization 

This repo contains code to implement natural language processing (NLP) models which will search archived documents and identify paragraphs concerning traffic regulations for different countries. The main output will be a summary of the identified paragraphs.  

[Python 3.8](https://www.python.org)

### Requirements
- [Docker](https://www.docker.com)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [NVIDIA Docker Container Runtime](https://github.com/NVIDIA/nvidia-container-runtime)

## Getting Started
Follow these instructions to set up your local environment using Docker. Docker ensures a consistent experience across development, testing, training, and even production. The self-contained Docker image automatically installs all required frameworks and libraries, saving you time and effort.

### First Time Users

If this is your first time using this application, please ensure that you have installed the
[requirements](#requirements) listed above before proceeding. If you are using MacOS or Linux, you
can run this command:

```sh
brew install git docker pre-commit shellcheck
```

On Windows you can run this commmand:

```sh
choco install git docker pre-commit shellcheck
```

We use pre-commit, a package manager for pre commit hooks, to run a list of hooks that checks the
following criteria before allowing a user to commit their changes:

- files parse as valid Python
- commit contains files less than 100MB in size
- commit does not contain any private key
- ensures that a file is either empty, or ends with one newline
- sorts entries in requirements.txt
- trims trailing whitespace
- runs black, a Python code formatter

To ensure that pre-commit is used, run

```sh
pre-commit install
```

after git, docker and pre-commit are installed from the previous step above. This will ensure that
pre-commit always runs the list of hooks defined in the .pre-commit-config.yaml file in the
project's root directory.

To get started, start playing with some of the [commands](#summary-of-commands) or [launch the
application locally](#launching-the-application).

### Launching the Application

To launch this application, you need to first build the Docker image using

```sh
bin/build.sh
```

and then bring up the containers for the application with

```sh
bin/up.sh
```

Once you're done working with your application, you can stop all containers and remove the
containers, volumes and images associated with the application by running:

```sh
bin/down.sh
```

Below are additional instruction on [training](#training) and [running tests](#testing) to verify
that everything is working.

## Additional Commands

### Paragraph Embedding
Before running the application, you have to generate embedded paragraphs using the raw data files provided. For embedding, include a list of countries that you ant to subet and set `embed` and `get_locations` in the main.py to `True`. To preprocess the data, run

```sh
bin/preprocess.sh
```

and this will save the preprocessed data to a local folder, as well as the generated embeddings.

### Paragraph Summarization
To summarize the identified embedded paragraphs, run

```sh
bin/summarize.sh
```

If you have trouble with this commmand, ensure that the filenames from the preprocessing step align with the naming conventions outlined in the config.json file.

### Model Experimentation
For exploratory analysis, consider using Jupyter Lab. Our notebooks are in the notebooks directory of this repository.

To launch Jupyter lab, run this command:

```sh
bin/notebook.sh
```

and navigate to http://localhost:8888/lab to access the lab instance.

(Note: Please include further instructions if GPU is required!)

### Unit Testing
Run unit tests using Docker by running this command: 

```sh
bin/test.sh
```

The unit tests run using [pytest](https://docs.pytest.org/en/latest/). To run a test on a specific file or directory, use the `-k` optino and list the path or file after. 

For example, to run just the test for the API, we can run:

```shell script
bin/test.sh -k test_api.py
```

### Summary of Commands
The `bin/` directory contains basic shell bin that allow us access to common commands on most
environments. We're not guaranteed much functionality on any generic machine, so keeping these
basic is important.

The most commonly used bin are:

- `bin/build.sh` - build docker container(s) defined in `Dockerfile` and `docker-compose.yml`
- `bin/test.sh` - run unit tests defined in `tests/`
- `bin/notebook.sh` - instantiate a new jupyter notebook server
- `bin/shell.sh` - instantiate a new bash terminal inside the container
- `bin/preprocess.sh` - run location identification, preprocessing and embedding on raw data
- `bin/summarize.sh` - compute similarity index and summarize paragraphs

Additional bin:

- `bin/lint.sh` - check code formatting for the project
- `bin/setup_environment.sh` - sets any build arguments or settings for all containers brought up
  with docker-compose
- `bin/up.sh` - bring up all containers defined in `docker-compose.yml`
- `bin/down.sh` - stops all containers defined in `docker-compose.yml` and removes associated
  volumes, networks and images


## Data Directory

Data organization philosophy from [cookiecutter data
science](https://github.com/drivendata/cookiecutter-data-science)

```
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
```