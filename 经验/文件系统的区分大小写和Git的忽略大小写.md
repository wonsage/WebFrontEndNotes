## 背景简述
文件系统有区分大小写的配置，Windows的NTFS和macOS的APFS是默认不区分大小写，而Linux的EXT4默认区分大小写。
由于有以上的区别，Git也有相应的区分。git config core.ignorecase选项控制了是否忽略大小写，true时不区分，false时区分。此项会根据系统的文件系统进行默认配置。
## 可能出现的问题
文件系统和Git在大小写配置上不相宜时可能出现一些问题。
比如，Git仓库区分，文件系统不区分，则pull后，会出现大小写不同的同名文件夹或文件合并的情况。
区分大小写的系统可以兼容不区分的，而不区分的则无法兼容区分的。不区分大小写是区分大小写的子集。（此段待考证）
使用大小写系统开发时遇到
#### git中的文件无法改名
在不区分大小写的系统中，文件名可以修改大小写，但忽略大小写的Git无法记录这类大小写改动，不会产生log。
解决办法有：
- 使用两次`git mv`命令：先`git mv dir-name tmp-name`，后`git mv tmp-name dir-name`。
  注：在core.ignorecase为true时，使用`git mv a.js A.js`会有问题。
- 两次提交：改一个中间名后提交一次，改为目标名后再次提交。
不建议修改git config core.ignorecase为false，因为改名后提交，仓库中会有大小写不同的两个文件，需要再手动删除。
假如修改了core.ignorecase，解决后记得使用`git config --unset core.ignorecase`改回。

#### 文件改名后报错
文件引入其他文件后，又修改了文件或文件夹名的大小写，此时可能会有如下的类似报错：
```
File name '/Volumes/Dev/case/Stat.vue' differs from already included file name '/Volumes/Dev/CASE/Stat.vue' only in casing.  
The file is in the program because:  
Root file specified for compilation  
Imported via "./Stat.vue" from file '/Volumes/Dev/CASE/index.vue'Vetur(1149)
```
造成此报错的原因是，文件夹原名`CASE`，后修改为`case`。在不区分大小写的系统中，二者视为同一文件，文件索引记录的仍为原名`CASE`。
解决办法是，将case文件夹复制一份，删除原有文件夹后再改名。
## 个人推荐配置
根据开发中的情况，来决定是否在工作电脑上开启区分大小写。使用Mac/Win作为开发电脑时，如果团队不是全Linux开发，则使用默认的即可。只在确实需要的时候，在硬盘中新建一个区分大小写的分区作为专用即可。

## 参考
[区分大小写 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/case-sensitivity#differences-between-windows-and-linux-case-sensitivity)