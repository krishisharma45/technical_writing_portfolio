# The Celer Project

## About the Project
Addressing engineers' need for both structure and freedom, this tool leverages project data visualization to shape a standardized yet flexible engineering workflow driven by Git metrics pulled from Git repos.

### Built With

[Python 3.8](https://www.python.org)

### Requirements

- [Docker](https://www.docker.com)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Terraform](https://www.terraform.io/)
- [AWS](https://aws.amazon.com)

## Getting Started

This project leverages Docker to guarantee a consistent environment across development, testing, training, and even production. Use these intstructions to help you get started.

### First Time Users
If this is your first time using this application, please ensure that you have installed the[requirements](#requirements) listed above before proceeding. If you are using MacOS or Linux, you can run this command:

```shell script
brew install git docker
```

And if you are on Windows, you can run this command:
```shell script
choco install git docker
```

To get started, start playing with some of the <a href="#command-summary">commands</a> or <a href="#launching-the-app">launch the application locally</a>.

<h3 id="launching-the-app"> Launching the Application </h3>
To launch this application, you need to first build the Docker image using

```shell script
bin/build.sh
```
and then bring up the containers for the application with

```shell script
bin/up.sh
```

Once you're done working with your application, you can stop all containers and remove the containers, volumes and images associated with the application by running
```shell script
bin/down.sh
```

Below are additional instruction on <a href="#training">training</a> and <a href="#testing">running tests</a> to verify that everything is working.

<h2 id="additional-commands"> Additional Commands </h2>

<h3 id="training"> Testing the Application </h3>
Once the Docker image is built we can run the project's unit tests to verify everything is
working. The below command will start a Docker container and execute all unit tests using
the [pytest framework](https://docs.pytest.org/en/latest/).

```shell script
bin/test.sh
```

If you want to run a test on a specific file or directory (rather than running all the tests in the tests/ directory), you can use the `-k` flag and list the file path afterwards.

For example, if we specifically wanted to run a test called "test_api", and its file path is as "tests/test_api.py", we can run:

```shell script
bin/test.sh -k test_api.py
```

<h3 id="command-summary"> Summary of Commands </h3>

The `bin/` directory contains basic shell scripts that allow us access to common commands on most environments. We're not guaranteed much functionality on any generic machine, so keeping these basic is important.

The most commonly scripts are:

- `bin/build.sh` - build docker container(s) defined in `Dockerfile` and `docker-compose.yml`
- `bin/test.sh` - run unit tests defined in `tests/`
- `bin/shell.sh` - instantiate a new bash terminal inside the container

Additional scripts:

- `bin/coverage.sh` - run a coverage report based on a pytest run of `tests/`
- `bin/setup_environment.sh` - sets any build arguments or settings for all containers brought up with docker-compose
- `bin/up.sh` - bring up all containers defined in `docker-compose.yml`
- `bin/down.sh` - stops all containers defined in `docker-compose.yml` and removes associated volumes, networks and images

<h4 id="command-details">Example of How to Use the Commands</h4>
If you want to use the shell script for a specific service listed in your Docker Compose, then you can do that by listing the name of the service after the shell script.

For example, if we wanted to specifically use the shell script to inspect the Grafana container of an application, we can run:
```shell
bin/shell.sh grafana
```

Note that this assumes that there is a service in the Docker Compose called "grafana".