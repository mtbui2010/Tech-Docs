[Main](../README.md)

## Base module
<img src="../images/1.PNG" width="50%">

## Use Base Module
<img src="../images/2.PNG" width="100%">

### Sample
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


## Base Detection Module
<img src="../images/3.PNG" width="70%">

## Base GUI Detection Module
<img src="../images/4.PNG" width="70%">

## Base Robot module
<img src="../images/5.PNG" width="60%">

## Combine modules
<img src="../images/6.PNG" width="100%">

[Main](../README.md)
