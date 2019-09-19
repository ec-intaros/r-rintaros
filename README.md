# r-rintaros

r-rintaros is an Anaconda package which provides RIntaros.
RIntaros is an interface between RGeostats and Intaros. 

## License

* GPL v3


### Quick link

* [Installation](#installation)
* [Testing](#testing)
* [Upgrade](#upgrade)

### <a name="installation">Installation 

* Login on a [Ellip Workflows VM](https://docs.terradue.com/ellip/solutions/workflows/index.html),
* Install the dependencies:

```
sudo yum install -y glibc-2.14 miniconda
```

* Install the R package:

```
sudo conda update conda 
sudo conda install r-rintaros
```

### <a name="testing">Testing 

* Type:

```
LD_LIBRARY_PATH=/opt/glibc-2.14/lib:${LD_LIBRARY_PATH} /opt/anaconda/bin/R -e "library('RIntaros')"
```

### <a name="upgrade">Upgrade

To upgrade this package to newer version of Rgeostats proceed as follows:

* Login on a Ellip Workflows VM,
* Clone the repo:

```
git clone https://github.com/ec-intaros/r-rintaros.git
cd r-rintaros/conda.recipe
git checkout develop
```

* Edit the `meta.yaml` file to update the following information:

``` 
version (first line)
sha256
```

* Install `conda-build` with:

```
sudo conda install conda-build
```
 
* Build the package with:

```
sudo conda build .
```
 
* Commit and push the local changes to the remote repository:

```
git commit -am "Set new version"
```

* Initialise [git flow](https://danielkummer.github.io/git-flow-cheatsheet/):

```
git flow init -d
export GIT_MERGE_AUTOEDIT=no
``` 

* Perform the release:

```
version=<your version number>
git flow release start ${version}
git flow release finish -m "${version}" ${version}
```

* Push the changes on the remote repository

```
git config --global push.default matching
git push && git push --tags
```

The command *git push* triggers a build process on https://build.terradue.com, which produces an Anaconda package for the new version and stores it under https://anaconda.org/Terradue/r-rintaros.
