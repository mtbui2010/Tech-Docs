[Main](../README.md)

### Distritrube package
1. Create an user ID in pypi.org

2. Install:
```sh
pip install  --upgrade setuptools whee
pip install  --upgrade twine
```

3. Make wheel and upload pypi
Change version of package in setup.py
New version > old version
```sh
cd $ROOT
sudo rm -rf build
sudo rm -rf dist
python3 setup.py sdist bdist_wheel
python3 -m twine upload dist/*
```

4. Install uploaded package:
```sh 
pip install $PACKAGE_NAME
```

### Distritrube binary package
- Pypi does not allow system-specified binary package
-> Trick:  change dist/[package-name]-[system]-linux.whl -> change dist/[package-name]-[system]-manylinux2-14.whl 

```sh
cd $ROOT
sudo rm -rf build
sudo rm -rf dist
python3 setup.py build_ext –inplace
python3 setup.py sdist bdist_wheel
```
Rename .whl file
```sh
 python3 -m twine upload dist/*
```


[Main](../README.md)
