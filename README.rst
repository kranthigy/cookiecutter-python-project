Cookiecutter Python Project
###########################

This project contains a Cookiecutter template to create new Python 3.6+
projects. This approach takes most of the boiler plate out of creating new
Python projects.

Cookiecutter is a command-line utility that creates projects from templates.
Cookiecutter lets you to easily and quickly bootstrap a new project from a
template which allows you to skip all manual setup and common mistakes when
starting a new project.

Cookiecutter takes a source directory tree and copies it into your new
project. It replaces all the names that it finds surrounded by templating
tags ``{{`` and ``}}`` with names that it finds in the file
``cookiecutter.json``.

The Python project structure produced by this Cookiecutter template
contains the following items:

- A minimal README.rst file.
- A Makefile that automates many common developer tasks, such as:

  - Running unit tests.
  - Checking code coverage.
  - Checking style compliance.
  - Checking type annotations.
  - Generating documentation.
  - Generating, testing and uploading a project release to PyPI.

- A ``setup.py`` file used to generate project install and releases.
- A ``CONTRIBUTING.rst`` guide. On Github this file is shown when sending
  a pull request or an issue. This file also gets included in the generated
  developer documentation.
- An empty ``CHANGELOG.rst`` file. This file gets included in the user
  documentation.
- A ``License`` file that defaults to the MIT License. Change this if
  you choose a license other than MIT.
- An ``examples`` directory with a minimal quickstart example script. This
  script imports the package and prints the package version. It is also
  called by the unit test suite to ensure it always works.
- A ``tests`` directory containing a basic unit test (using unittest) and
  a shell script that can be used to test a wheel distribution of the
  package.
- A ``.travis.yml`` file for continuous integration setup.
- A ``docs`` directory with a pre-configured Sphinx documentation setup. It
  contains:

  - A minimal ``index.rst`` page

  - A user focused page containing information such as installation
    instructions, API docs, a link to the change log and instructions
    about how to raise a bug.

  - A developer focused page containing information such as contributing,
    testing, code coverage, style compliance, type annotations and
    documentation.

It is assumed that the new Python package will eventually be:

- hosted on Github (or perhaps GitLab)
- published to PyPI (using bdist_wheel)
- linked to ReadTheDocs.

The generated docs have some references and links to those sites.


Getting Started
===============

One Time Setup Steps
--------------------

You need to prepare two locations to store content:

- A place where you store your projects (git repositories). You probably
  have a folder for that already (e.g. ``git-repos``). We will call this
  location $REPOS_DIR.

- A place to store Python virtual environments. Avoid putting your virtual
  environment in your project directory next to your code. This will avoid
  accidentally adding venv content to a git change set. We will call this
  location $VENVS_DIR.

Create a new virtual environment for cookiecutter and install cookiecutter
using ``pip``:

.. code-block:: console

    $ python -m venv $VENVS_DIR/ccenv
    $ source $VENVS_DIR/ccenv/bin/activate
    (ccenv) $
    (ccenv) $ pip install cookiecutter

You are now ready to create a new Python project from the Cookiecutter
template provided by this project.


Create a new project
--------------------

To create a new Python project based on a cookiecutter template simply
navigate to a directory where you want to create the new project (e.g
$REPOS_DIR) and run the ``cookiecutter`` command with this template as a
command line argument.

If you have cloned a local copy of this template you can use that:

.. code-block:: console

    (ccenv) $ cookiecutter path/to/cookiecutter-python-project

Alternatively you can create a new project by referencing this template
at Github (where gh is an abbreviated shortened form for Github):

.. code-block:: console

    (ccenv) $ cookiecutter gh:claws/cookiecutter-python-project

You will be prompted for input:

- Prompts are the keys in cookiecutter.json.
- Default responses are the values in cookiecutter.json.
- Prompts are shown in order.

You should now have a new Python project.

You can exit the cookiecutter virtual environment as it is no longer
required.

.. code-block:: console

    (ccenv) $ deactivate
    $


Manual Modifications
--------------------

Some aspects of generating a project in a generic approach are not practical
to completely automate so there may be a few steps remaining before you can
use the new project.

- If you specify a license other than MIT then you will need to update the
  ``LICENSE`` file to contain your license content. By default it contains
  a MIT License.

- If you do not plan to publish project artifacts at GitHub, PyPI or
  ReadTheDocs then remove any links to those sites. Affected files are:

  - README.rst
  - setup.py
  - docs/source/index.rst

- Update any additional useful classifiers in ``setup.py``. The list of
  available classifiers can be found `here <https://pypi.python.org/pypi?:action=list_classifiers>`_.


Example
=======

Below is an example showing exactly how to create a new Python project using
the template in this project. In this scenario the project is called
``abc 123`` and the Python package is called ``abc_123``.

At this point it is assumed that you have performed the actions outlined in
the One Time Setup Steps section above. This provides a virtual environment
that makes cookiecutter available.

Run cookiecutter and pass it a reference to the template. The first question
asks for the package display name. This human friendly label is used in docs
to refer to the project. It is then used to create a candidate package name so
it should not contain special characters that are invalid when used in a
Python attribute. It can have spaces and hyphens in it. The package display
name is first converted to lowercase text and then any spaces or hyphens are
converted to underscores to produce a Python package name.

.. code-block:: console

    (ccenv) $ cookiecutter ../cookiecutter-python-project/
    package_display_name [Package-Name]: abc 123
    package_name [abc_123]:
    package_short_description [A description of the package]: This is my abc 123 package.
    version [0.0.1]:
    full_name [Your Name]: First Last
    email []:
    github_user_name [GithubUserName]: flast
    github_repo_name [abc_123]:
    Select license:
    1 - MIT license
    2 - BSD license
    3 - Apache Software License 2.0
    4 - GNU General Public License v3
    5 - Not open source
    Choose from 1, 2, 3, 4, 5 [1]:
    year [2018]:

The project has been created in the ``abc_123`` directory.

.. code-block:: console

    $ cd abc_123

We can now kick the tires of this new project by performing some initial
project checks.

First, let's create a project specific virtual environment and activate it.
This will install all of the project's development dependencies as well as
the project itself. The project will be install as an editable package (by
using the ``-e`` flag to ``pip``).

.. code-block:: console

    $ make venv
    ...
    Enter virtual environment using:

      	source path/to/venvs/abc_123/bin/activate

    $ source path/to/venvs/abc_123/bin/activate
    (abc_123) $

Now that we have a virtual environment we can check the remaining convenience
functions provided by the Makefile.

.. code-block:: console

    (abc_123) $ make style
    (abc_123) $ make check-types
    (abc_123) $ make test
    (abc_123) $ make test-verbose
    (abc_123) $ make check-coverage
    (abc_123) $ make check-docs
    (abc_123) $ make docs
    (abc_123) $ make serve-docs  # in browser navigate to http://localhost:8000/html
    (abc_123) $ make dist
    (abc_123) $ make dist-test
