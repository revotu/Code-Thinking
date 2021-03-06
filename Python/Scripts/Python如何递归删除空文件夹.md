# Python如何递归删除空文件夹 #
Python如何递归删除空文件夹，这个问题很常见。但大多数人的解决办法都是自己实现递归函数解决这个问题，其实根本不用那么麻烦。Python中的`os.walk`提供了一种从内到外的遍历目录树的方法（设置`topdown=False`），这样由内到外判断当前目录树下是否有文件和文件夹，如果都没有则意味着当前目录树为空文件夹，`os.rmdir`删除即可。
```python
#Recursively Remove Empty Directories

import os

for root, dirs, files in os.walk(path, topdown=False):
    if not files and not dirs:
        os.rmdir(root)
```
<!-- more -->
如果在遍历文件夹同时，先做了一些操作，比如删除文件操作`os.remove`，然后再判断此时文件夹是否为空，为空则删除。需要用`os.listdir`判断当前文件夹是否为空，因为`dirs`和`files`还是刚进入当前文件夹`root`时得到的。
```python
#Recursively Remove Empty Directories, During do something like os.remove(file)

import os

for root, dirs, files in os.walk(path, topdown=False):
    # do something like os.remove(file)
    if not os.listdir(root):
        os.rmdir(root)
```
原文链接：[Python如何递归删除空文件夹](http://www.revotu.com/recursively-delete-empty-directories-with-python.html)