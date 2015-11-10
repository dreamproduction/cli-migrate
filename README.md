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

Then install the `cli-migrate` package:
comming soon

# How it works

comming soon
