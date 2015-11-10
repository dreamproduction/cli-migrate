# cli-migrate

This tool runs cli scripts. It is similar to database migrations tools, but it runs cli scripts. The ideea is that sometimes you need to run some scripts after a code deploy, like rebuilding the cache, or regenerate image derivatives. This tool keeps track of scripts that were run, and it doesn't run them again. This is helpfull if you need to automate the deploy.

# Installing

Prerequisites: you need to install PyYAML.

For Mac, run:
```
pip install pyyaml
```
If you don't have `pip` installed, run:
```
easy_install pip
```
If you don't want to install `pip`, you can instal PyYAML with `easy_install`:
```
easy_install pyyaml
```

For linux, use your package manager. Examples:
```
sudo apt-get install python-yaml
sudo yum install python-yaml
```

Then install the `cli-migrate` package. If you have `composer`:
```
composer require dreamproduction/cli-manager
```
Otherwise, just clone it.

Then, make sure that the executable (`bin/cli-migrate`) is in your path.

# Project setup

In the project root, you should have a YAML file, with the name  `.cli-migrate.config.yml`. This file should contain the following keys:
- scripts_folder: The path, from the project root, to the folder where you want the migrate scripts to be stored.
- state_file: The name (and path if you want) to the file where the migrations state is saved.

A dist config file is provided in the package (`.cli-migrate.config.dist.yml`), and it has good defaults for the options in most of the cases.

You should also configure your VCS to not include the state file (default `.cli-migrate.state.yml`). If you use git, add in the .gitignore:
```

# Ignore the state file for dreamproduction/cli-migrate
.cli-migrate.state.yml

```

# How to use it

First, you need to define your migration files. `cli-migrate` provides a command for generating empty executable migration files, prepended by the date in `year-month-day-hour:minute:second` format, to insure that the scripts are executed in the order they are created. The command is:
```
cli-migrate generate "Optional description of the migration. It is however a good practice to provide it. Only the first 6 words are used for the filename, but the whole description will be added to the migration file as a message displayed using echo"
```

Then you write your code in them, you commit them, and whenever you deploy the code, or some coleague pulls your code, the only thing that needs to be executed is:
```
cli-migrate run
```

The migrations scripts that are executed are recorded in the state file, and they will not execute again.
