#### git配置用户信息
```
// 配置本地用户信息
git config --local user.name 'user'
git config --local user.email 'user.email'

// 配置全局用户信息
git config --global user.name 'user'
git config --global user.email ''user.email
```
#### git查询当前配置
```
git config --list
```

#### git添加文件到缓存区
```
git add . // 添加所有修改的文件
git add <file> // 添加指定文件到缓存区
```
#### 撤销文件修改
当本地文件只是修改没有被添加到缓存区，`git checkout -- <file>`。

当文件已经`add`进缓存区了，可以使用`git restore --staged <file>`丢弃。

当文件已经`commit`，可以使用`git reset HEAD^`将最近的提交撤销。