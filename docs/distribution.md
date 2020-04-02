### Distributing
The maintainers of the package keep the recent version of the ```pyviz3d``` package available on [PyPy](https://packaging.python.org/tutorials/packaging-projects/) and Anaconda.
The anaconda package is created from the pypi package.

##### PyPi

Loosely following the instructions from [[1](https://medium.com/@joel.barmettler/how-to-upload-your-python-package-to-pypi-65edc5fe9c56)]

```
$ pip install twine
```

In your home folder, set up `~/.pypirc`:

```
[distutils]
index-servers=
    pypi
    testpypi
[testpypi]
repository: https://test.pypi.org/legacy/
username: your username
```

To test the release without messing around with the public PyPi release.
First, this creates `dist` and `pyviz3d.egg-info` folders which can then be uploaded to the pypi test repository given the correct credentials.
```
$ python setup.py sdist bdist_wheel
$ twine upload --repository-url https://test.pypi.org/legacy/ dist/*
$ pip install -i https://test.pypi.org/simple/ pyviz3d
```


When happy, prepare a new release on github:
```
https://github.com/francisengelmann/pyviz3d/releases
```

When done, we can upload the release to the public PyPi repository:
```
$ python setup.py sdist bdist_wheel
$ twine upload dist/*
```

##### Anaconda

We rely on Anaconda Cloud to host the pyviz3d package
[[2]]( https://docs.anaconda.com/anaconda-cloud/user-guide/tasks/work-with-packages/)
```
$ conda install anaconda-client conda-build conda-verify
$ conda config --set anaconda_upload no
$ conda skeleton pypi pyviz3d
$ conda build pyviz3d
```