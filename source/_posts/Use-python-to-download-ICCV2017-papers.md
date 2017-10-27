---
title: Use python to download ICCV2017 papers
date: 2017-10-27 17:46:15
categories: Tech
tags:
- python
---
### Enviroment
- [x] python 2.7

### Usage
Before run this code, please make sure you have installed necessary libraries.
1. modify the `localDir` in the code
2. run the code, and all papers will be downloaded in the path， the name of the file is just the title of the paper.

### Something to say
The code will replace some  punctuations which is not legal in the file name.   
If you replace ICCV2017 with CVPR2017, you can download all papers in CVPR2017. That is a **bonus**.

### Code
```python
# coding:utf-8
import re
import requests
import urllib
import os
# get web context
r = requests.get('http://openaccess.thecvf.com/ICCV2017.py')
data = r.text
# find all pdf links
link_list =re.findall(r"(?<=href=\").+?pdf\">pdf|(?<=href=\').+?pdf\">pdf" ,data)
name_list =re.findall(r"(?<=href=\").+?2017_paper.html\">.+?</a>" ,data)
cnt = 0
totalnum = len(link_list)
# your local path to download pdf files
localDir = 'E:\study\papers\ICCV2017\\'
if not os.path.exists(localDir):
    os.makedirs(localDir)
# for url in link_list:
while cnt < totalnum:
    url = link_list[cnt]
    url = url[0:-5]
    #seperate file name from url links
    file_name = name_list[cnt].split('<')[0].split('>')[1]
    #import pdb
    #pdb.set_trace()
    file_name = file_name.replace(':','_')
    file_name = file_name.replace('\"','_')
    file_name = file_name.replace('?','_')
    file_name = file_name.replace('/','_')
    file_path = localDir + file_name + '.pdf'
    print file_name
    # download pdf files
    try:
        urllib.urlretrieve('http://openaccess.thecvf.com/'+url,file_path)
        # os.symtem('wget '+url+' -O '+file_path)
        print "downloading:"+url+" -> "+file_path  
        print "Downloading %s/%s" % (cnt, totalnum)
    except Exception,e:
        continue
    cnt = cnt + 1
print "all download finished"  
```