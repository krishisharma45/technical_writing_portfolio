# Templating CLI

This command-line tool helps you generate template files commonly used in Python projects built with Docker. It leverages Click and PyInquirer for a user-friendly experience.

We aim to make this tool the go-to source for reusable Python project templates. While we encourage merging experimental or unfinished templates via pull requests as per our Gitflow guidelines (see below), ensure they're prefixed with "experimental-" until tested and proven successful in at least two different projects.

## Developer Guide
### Latest Release Installation

You can use pip installation method. First, ensure that you are on main and checkout the latest
version of main:

```sh
git checkout main && git pull origin main
```

Then, run:

```sh
pip install -e .
```

to get the latest version of this templating tool onto your local computer. To start using it, you can
following the below examples.

### Examples of How to Use Template Init

Then, you can initialize a project using:

```sh
template init -o ~/Documents
```

To define an output path, you can use
the -o flag. After you use this command, you'll encounter a few prompts that will ask about which
features you need for your project template.

If you want to skip all prompts, simply run:

```sh
template init -b
```

The -b signifies that the user only wants the default template.

### Development Branches Installation

If you are on a feature branch or develop and want to test out the changes that you've made by
generating a template, you can use the pip installation method directly. To do this, all you have
to do is make sure you're on the branch you want to test and run:

```sh
pip install -e .
```

You should see be able to find
the template directory in your virtual environment.

## Existing Templates

Prefer composition over a monolithic framework, so that you can mix and match different templates
into your project. Templates other than "project" are presented to users in a menu, and in the
future should be able to get added to existing projects with a new command. Templates should not
depend on each other, but should follow common conventions to enable their coexistence within
projects. New template folders should be prefixed by "experimental-" until they have appropriate
unit tests and have been used successfully in at least two different projects.

Templates live in the `templates/` folder. A few templates are included:

- `base/`: All projects are
  instantiated with this base code.
- `fastapi`: a template for getting started with FastAPI; includes an outline
  for a prediction endpoint.

## Beta Testing

If you have been selected by a peer to test out a feature branch, please follow the Development
Branches Installation guide above to get the template that needs to be tested. Then, run the
command:

```sh
template init -n beta_testing -o ~/Desktop
```

to generate the template. If the feature involves changing or adding options to the template init
command or a new command for template, make sure to test the related commands for that feature as
well. Once you have a copy of the template, run:

```sh
scripts/build.sh
```

to build the image and then

```sh
scripts/up.sh
```

to bring up containers for all the services in the project template you generated. If there are
other commands that were created in the feature branch, work with the developer to ensure that it
is properly tested and documented.

## Contribution

### Guidelines

Our guidelines for contributing to this CLI are the following:

- Template is a cookiecutter repo formatting generator - please focus on adding templates or auxiliary functionality to
  existing templates
- If your template has specific instructions or commands, add the complementary files to your
  template directory (e.g., enhanced README.md, bin/upload_data.sh, boilerplate test files in the
  tests/ directory)
- Ideally, test out any new ideas on other projects and discuss the pros and cons of having the
  template readily available for future projects before coding up template files
- Design templates around the 80/20 rule: our templates aim to solve problems that we face on 80%
  of our projects. We do not try to ensure that each template addresses every project's unique
  corner cases, but try to save time on problems that occur frequently and take a lot of time to
  solve

### Process

If you are ready to contribute, our process for contribution is:

1. Discuss your template idea through Github Issues
2. Gather feedback from projects that have implemented the template idea
3. Create a branch from `main` and title it with your initials and the feature/template 
4. Code your feature/template and request at least one engineer to peer review your branch
5. After at least one approval, merge the branch into `develop`
6. Schedule a release date
7. Prepare for the release by getting two different engineers to review the latest `develop` branch
8. Create a tag and draft a release in GitHub (follow the semantic versioning rules for assigning the tag name)
9. Upon tag creation and two or more approvals, merge `develop` into `main`

Should you have any questions, let us know on Github.

## Resources

[Illustrated guide](https://medium.com/fiverr-engineering/major-minor-patch-a5298e2e1798) on how
to use semantic versioning.
