# Contributing to DOT

Hi! Thanks for your interest in contributing to DOT, we're really excited to see you! In this document we'll try to 
summarize everything that you need to know to do a good job.

Read our [Code of Conduct](./CODE_OF_CONDUCT.md) to keep our community approachable and respectable.

In this guide you will get an overview of the contribution workflow from opening an issue, creating a PR, reviewing, and 
merging the PR.

## New contributor guide

To get an overview of the project, read the [README](README.md). Here are some resources to help you get started with open source contributions:

- [Finding ways to contribute to open source on GitHub](https://docs.github.com/en/get-started/exploring-projects-on-github/finding-ways-to-contribute-to-open-source-on-github)
- [Set up Git](https://docs.github.com/en/get-started/quickstart/set-up-git)
- [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [Collaborating with pull requests](https://docs.github.com/en/github/collaborating-with-pull-requests)

## Getting started

### Creating Issues

If you spot a problem, [search if an issue already exists](<DOT REPO ISSUE Search>). If a related issue doesn't exist, 
you can open a new issue using a relevant [issue form](<DOT REPO NEW ISSUE>). 

As a general rule, we don’t assign issues to anyone. If you find an issue to work on, you are welcome to open a PR with a fix.

## Making Code changes

## Setting up a Development Environment

To set up your local development environment for contributing follow the steps
in the paragraphs below.

The easiest way to develop DOT is to use the provided Docker environment, see [README](./README.md) for more details. 
This comes with the user interface and Postgres database included. Self tests will also work there too, so we encourage
using this environment if you can. The Docker image will mount your filesystem, so changes to files 
will be reflected in the running instance of DOT and its user interface.

#### Running DOT without using Docker

If you wish to build locally, then ...

1. Install [miniconda](https://docs.conda.io/en/latest/miniconda.html) by selecting the installer that fits your OS version. Once it is installed you may have to restart your terminal (closing your terminal and opening again)
2. In this directory, open terminal
3. `conda env create -f environment.yml`
4. `conda activate dot_conda_env`
5. You will need a postgres database called 'dot_db'. To populate objects run the scripts in [./db/dot](./db/dot) sequentially.
6. Update your [./dot/config/dot_config.yml](./dot/config/dot_config.yml]) to point at your local database
7. Create a config file for the database connection details, located at the directory `dot/self_tests/data/base_self_test`.

#### Running unit tests

Run the following and hopefully you get a successful output.
```
pytest dot/self_tests/unit 
```

You can also run
```
git commit
```
since you have added the `Code Quality` tools referenced in the main README as a pre-commit hook,
together with the self-tests.

### GitHub Pull requests

As many other open source projects, we use the famous
[gitflow](https://nvie.com/posts/a-successful-git-branching-model/) to manage our
branches.

Summary of our git branching model:
- Go to the `dev` branch (`git checkout dev`);
- Get all the latest work from the upstream `datakind/Data-Observation-Toolkit` repository
  (`git pull upstream dev`);
- Create a new branch off of `dev` with a descriptive name (for example:
  `feature/new-test-macro`, `bugfix/bug-when-uploading-results`). You can
  do it by switching to the `dev` branch (`git checkout dev`) and then
  creating a new branch (`git checkout -b name-of-the-new-branch`);
- Do many small commits on that branch locally (`git add files-changed`,
  `git commit -m "Add some change"`); whenever you commit, the self-tests 
  and code quality will kick in; fix anything that gets broken
- Push to your fork on GitHub (with the name as your local branch:
  `git push origin branch-name`);
- Create a pull request using the GitHub Web interface (asking us to pull the
  changes from your new branch and add to them our `dev` branch);
- Wait for comments.


### Tips

- Write [helpful commit
  messages](https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message).
- Anything in the `dev` branch has to be deployable (no failing tests).
- Never use `git add .`: it can add unwanted files;
- Avoid using `git commit -a` unless you know what you're doing;
- Check every change with `git diff` before adding them to the index (stage
  area) and with `git diff --cached` before committing;
- If you have push access to the main repository, please do not commit directly
  to `dev`: your access should be used only to accept pull requests; if you
  want to make a new feature, you should use the same process as other
  developers so you code will be reviewed.


## Code Guidelines

- Use [PEP8](https://www.python.org/dev/peps/pep-0008/);
- Write tests for your new features (please see "Tests" topic below);
- Always remember that [commented code is dead
  code](https://www.codinghorror.com/blog/2008/07/coding-without-comments.html);
- Name identifiers (variables, classes, functions, module names) with readable
  names (`x` is always wrong);
- When manipulating strings, we prefer either [f-string
  formatting](https://docs.python.org/3/tutorial/inputoutput.html#formatted-string-literals)
  (f`'{a} = {b}'`) or [new-style
  formatting](https://docs.python.org/library/string.html#format-string-syntax)
  (`'{} = {}'.format(a, b)`), instead of the old-style formatting (`'%s = %s' % (a, b)`);
- You will know if any test breaks when you commit, and the tests will be run
  again in the continuous integration pipeline (see below);


## Tests

You should write tests for every feature you add or bug you solve in the code.
Having automated tests for every line of our code lets us make big changes
without worries: there will always be tests to verify if the changes introduced
bugs or lack of features. If we don't have tests we will be blind and every
change will come with some fear of possibly breaking something.

For a better design of your code, we recommend using a technique called
[test-driven development](https://en.wikipedia.org/wiki/Test-driven_development),
where you write your tests **before** writing the actual code that implements
the desired feature.

You can use `pytest` to run your tests, no matter which type of test it is.


## Continuous Integration

We use [GitHub Actions](https://github.com/datakind/Data-Observation-Toolkit/actions) 
for continuous integration. 
See [here](https://docs.github.com/en/actions) for GitHub's documentation.

The [`.github/workflows/lint.yml`](.github/workflows/ci.yml) file configures the CI.