[Main](../README.md)

## [1. How to define and use module](../mds/api_module_design.md)
```sh
from ttcv.basic.basic_objects import BasObj
import cv2

# Define module
class ImProcessModule(BasObj):
    def rot90(self, im):
        return cv2.rotate(im, cv2.ROTATE_90_CLOCKWISE)

    def toGray(self, im):
        if len(im.shape)>2: return cv2.cvtColor(im,cv2.COLOR_BGR2GRAY)
        else: return im

# call module and execute method
im_processor = ImProcessModule()
im = cv2.imread(im_path)
im_rot = im_processor.rot90(im)
im_gray = im_processor.gray(im)
```
## [2. How define GUI module and run GUI](../mds/gui_design.md)
### Wrap it into GUI module
```sh
from ttcv.basic.basic_objects import DetGui
from ttcv.basic.basic_gui import GuiModule

class ImProcessGui(ImProcessModule,DetGui):
    def gui_process_single(self, rgbd, method_ind=0, filename='unnamed', disp_mode='rgb'):
        if method_ind==0: return self.rot90(im)
        if method_ind==1: return  self.toGray(im)
        
module = GuiModule(module=ImProcessModule,type='im_process', name='Image Process',
                   category='detector', num_method=2, run_thread=True)
```
### Run GUI with defined module
```sh
BasGUI(title='Image Processing Demo', modules=[module,], test_dirs=['data',])
```
## [3. Packaging](../mds/packaging_package.md) 
[Sample package](https://github.com/mtbui2010/testlib

## [4. Github](../mds/co_github_branch.md) 
### Clone code from master brach 
- For first time only
```sh
git clone $REPOSITORY_LINK
```
### Resume your work
- Set github link
```sh
git remote add $REPOSITORY_LINK
```
- Uupdate changes from master branch
```sh
git pull origin master
```
### Work on **your recomended workspace**. 
- If you work on other folders, make sure your filename are **distinguished** to other member.

### Push your temporaly complete work to git.  Recommend to push code every working day in order to backup codes.
- Set github link
```sh
git remote add $REPOSITORY_LINK
```
- Set member's branch
  + If branch not exist
  ```sh
  git checkout -b $MEMBER_BRANCH
  ```
  + If branch exist
  ```sh
  git chekcout $MEMBER_BRANCH
  ```
- Add code location to be pushed
  + If add a folder
  ```sh
  git add $DIR_PATH
  ```
  + If add current folder
  ```sh
  git add .
  ```
  + If add current folder with some ignorances
  ```sh
  git add . .gitignore
  ```
  **.gitignore** includes all filepaths which will not be push. It is helpful to neglect heavy data or checkpoints, for example data/\*, checkpoint/\*
- Edit commit message
```sh
git commit -m $MSG
```
**Commit message** descrbing who changed and what changed, e.x. [Cunho] Add HRC movej
- Push code to your brach
```sh
git push origin $MEMBER_BRANCH
```

## [5. Binarization](../mds/packaging_binarization.md) 
[Sample code](https://github.com/mtbui2010/manage_scripts/blob/master/make_binary_package.py)
### Generate .pyi files
```sh
pip install mypy
stubgen *.py -o .
```
### Generate binary files
```sh
cd $ROOT
python3 setup.py build_ext --incplace
```

## [6. pypi](../mds/packaging_pypi.md) 
### Distritrube package
1. Create an user ID in pypi.org

2. Install:
```sh
pip install  --upgrade setuptools wheel
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
[Sample code](https://github.com/mtbui2010/manage_scripts/blob/master/distribute_package.py)
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
