---
title: You take THE photos
date: 2017-10-10 13:46:34
categories: Tech
tags:
- python
- image processing
---
### Samples
input | mask |  output
:---:|:---:|:---:
<img src="http://oxlfstmvz.bkt.clouddn.com/test.jpg" width="300"/> | <img src="http://oxlfstmvz.bkt.clouddn.com/python_generate_ngzk.png" width="300"/> | <img src="http://oxlfstmvz.bkt.clouddn.com/python_generate_output.jpg" width="300"/>


### Merge two picutres
This code will help you to merge two pictures.    
One image is in PNG form, and the other is in JPEG form. The PNG image has 4 channels, rgba, and the JPEG image only has 3 channels, rgb. By merging them together and you can get the final result, which seems to be taken by you.

**requirements**
* python

#### workflow
1. read the PNG image `Im` and get rgba data;
2. read the JPEG image as `I` and get rgb data;
3. resize `I` to `I'`, which is the smaller one as shown above;
4. blur the image `I` using gaussian kernel;
5. merge those images together according to the alpha channel data of `Im`

#### code
```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import pdb
from PIL import Image, ImageFilter
import numpy as np

im = Image.open('ngzk.png') # r,g,b,a
height = im.size[0]
width = im.size[1]
r,g,b,a = im.split()
pic = Image.open('test.jpg')

pic_b = pic.resize((height,width))
pic_b = pic_b.filter(ImageFilter.GaussianBlur(radius=7))
pic_s = pic.resize((268,465))
pic_b.paste(pic_s,(196,673))
# pic_b.show()

im = np.array(im)
pic_b = np.array(pic_b)
max_a = 0
for i in range(width):
  for j in range(height):
    p = 1.0*im[i,j][3]/255
    q = 1-p
    pic_b[i,j][0] =im[i,j][0] * p + pic_b[i,j][0] * q
    pic_b[i,j][1] =im[i,j][1] * p + pic_b[i,j][1] * q
    pic_b[i,j][2] =im[i,j][2] * p + pic_b[i,j][2] * q
outim = Image.fromarray(pic_b)
#outim.show()
outim.save('out.jpg')
```
Notice that this is **the simplest version**. You can modify this code so that the parameters can be read from the command console or package them to a execuate file.
