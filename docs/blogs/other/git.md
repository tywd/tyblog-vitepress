# git操作
## git操作——撤回修改
### 1.修改了代码，但是还没使用git add进行缓存，这时候想放弃修改
#### 1.1 放弃修改某个文件
```
git checkout -- filename
```
#### 1.2放弃修改所有文件
```
git checkout .
```
这个命令不会删除新建的文件，因为新建的文件还没有被add到仓库，不能被git操控，只能通过手动删除

### 2.已经使用git add缓存代码，但还没有用git commit提交，这时候想放弃修改
#### 2.1放弃修改某个文件
```
git reset HEAD filename
```
#### 2.2放弃所有文件的修改
```
git reset HEAD
```

这个时候还没有完全撤回所有的修改，这个命令是清除了所有的缓存，也就是回到了上面的第一步，目前本地的修改还是在的。如果要彻底清除代码的修改，还需要按照上面第一步的操作再来一次

### 3.已经使用git commit提交代码了，这时候想放弃修改
#### 3.1撤回本次修改，退回到上一次修改的时候
```
git reset --hard HEAD^
```

#### 3.2退回到任意版本的时候
先通过git log查看提交历史的commit id
```
git log
```
然后退回到指定版本
```
git reset --hard commit id
```