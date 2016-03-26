# Contributing

Contributions are welcome and are greatly appreciated! Every
little bit helps, and credit will always be given.

You can contribute in many ways:

## Types of Contributions

### Report Bugs

Report bugs through Github

If you are reporting a bug, please include:

-   Your operating system name and version.
-   Any details about your local setup that might be helpful in
    troubleshooting.
-   Detailed steps to reproduce the bug.

### Fix Bugs

Look through the GitHub issues for bugs. Anything tagged with "bug" is
open to whoever wants to implement it.

### Implement Features

Look through the GitHub issues for features. Anything tagged with
"feature" is open to whoever wants to implement it.

### Documentation

Dashed could always use better documentation,
whether as part of the official Dashed docs,
in docstrings, `docs/*.rst` or even on the web as blog posts or
articles.

### Submit Feedback

The best way to send feedback is to file an issue on Github.

If you are proposing a feature:

-   Explain in detail how it would work.
-   Keep the scope as narrow as possible, to make it easier to
    implement.
-   Remember that this is a volunteer-driven project, and that
    contributions are welcome :)

## Latest Documentation

[API Documentation](http://pythonhosted.com/dashed)

## Setting up a Python development environment

    # fork the repo on github and then clone it
    # alternatively you may want to clone the main repo but that won't work
    # so well if you are planning on sending PRs
    # git clone git@github.com:mistercrunch/dashed.git

    # [optional] setup a virtual env and activate it
    virtualenv env
    source env/bin/activate

    # install for development
    python setup.py develop

    # Create an admin user
    fabmanager create-admin --app dashed

    # Initialize the database
    dashed db upgrade

    # Create default roles and permissions
    dashed init

    # Load some data to play with
    dashed load_examples

    # start a dev web server
    dashed runserver -d


## Setting up the node / npm javascript environment

`dashed/assets` contains all npm-managed, front end assets.
Flask-Appbuilder itself comes bundled with jQuery and bootstrap.
While these may be phased out over time, these packages are currently not
managed with npm.


### Using npm to generate bundled files

#### npm
First, npm must be available in your environment. If it is not you can run the following commands
(taken from [this source](https://gist.github.com/DanHerbert/9520689))
```
brew install node --without-npm
echo prefix=~/.npm-packages >> ~/.npmrc
curl -L https://www.npmjs.com/install.sh | sh
```

The final step is to add
`~/.node/bin` to your `PATH` so commands you install globally are usable.
Add something like this to your `.bashrc` file.
```
export PATH="$HOME/.node/bin:$PATH"
```

#### npm packages
To install third party libraries defined in `package.json`, run the
following within this directory which will install them in a
new `node_modules/` folder within `assets/`.

```
npm install
```

To parse and generate bundled files for dashed, run either of the
following commands. The `dev` flag will keep the npm script running and
re-run it upon any changes within the assets directory.

```
# Compiles the production / optimized js & css
npm run prod

# Start a web server that manages and updates your assets as you modify them
npm run dev
```

For every development session you will have to start a flask dev server
as well as an npm watcher

```
dashed runserver -d -p 8081
npm run dev
```

## Testing

Tests can then be run with:

    ./run_unit_tests.sh

Lint the project with:

    # for python changes
    flake8 changes tests

    # for javascript
    npm run lint

## API documentation

Generate the documentation with:

    cd docs && ./build.sh

## CSS Themes
As part of the npm build process, CSS for Dashed is compiled from ```Less```, a dynamic stylesheet language.

It's possible to customize or add your own theme to Dashed, either by overriding CSS rules or preferably
by modifying the Less variables or files in ```assets/stylesheets/less/```.

The ```variables.less``` and ```bootswatch.less``` files that ship with Dashed are derived from
[Bootswatch](https://bootswatch.com) and thus extend Bootstrap. Modify variables in these files directly, or
swap them out entirely with the equivalent files from other Bootswatch (themes)[https://github.com/thomaspark/bootswatch.git]

## Pull Request Guidelines

Before you submit a pull request from your forked repo, check that it
meets these guidelines:

1.  The pull request should include tests, either as doctests,
    unit tests, or both.
2.  If the pull request adds functionality, the docs should be updated
    as part of the same PR. Doc string are often sufficient, make
    sure to follow the sphinx compatible standards.
3.  The pull request should work for Python 2.6, 2.7, and ideally python 3.3.
    `from __future__ import ` will be required in every `.py` file soon.
4.  Code will be reviewed by re running the unittests, flake8 and syntax
    should be as rigorous as the core Python project.
5.  Please rebase and resolve all conflicts before submitting.