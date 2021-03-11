#### git添加文件到缓存区
```
git add . // 添加所有修改的文件
git add filepath // 添加指定文件到缓存区
```
#### 撤销文件修改
当本地文件只是修改没有被添加到缓存区，`git checkout -- <file>`。

当文件已经`add`进缓存区了，可以使用`git restore --staged <file>`丢弃。

当文件已经`commit`，可以使用`git reset HEAD^`将最近的提交撤销。