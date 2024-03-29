# r-rintaros

r-rintaros is an Anaconda package which provides RIntaros package.
RIntaros is an R package which provides high level geostatistical functions relying on RGeostats package for the INTAROS project context. More information for the RGeostats package are available here: http://cg.ensmp.fr/rgeostats

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
sudo conda update -y conda 
```

* Install the R package:

```
sudo conda install r-rintaros
```

### <a name="testing">Testing 

* Type:

```
LD_LIBRARY_PATH=/opt/glibc-2.14/lib:${LD_LIBRARY_PATH} /opt/anaconda/bin/R -e "library('RIntaros')"
```

### <a name="upgrade">Upgrade

To upgrade this package to newer version of RIntaros proceed as follows:

* Login on a Ellip Workflows VM,
* Install the required dependencies:

```
sudo yum install -y glibc-2.14 miniconda
sudo conda update -y conda
sudo conda install -y conda-build
```

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
 
* Build the package with:

```
sudo conda build . --no-test
```

#### Local Test

* Perform a local test:

```
sudo conda install -y --use-local r-rintaros
LD_LIBRARY_PATH=/opt/glibc-2.14/lib:${LD_LIBRARY_PATH} /opt/anaconda/bin/R -e "library('RIntaros')"
```

#### Release and deployment to production

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
