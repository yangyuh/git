1. 创建仓库 (respository)
```
$ git init
```
2. 查看当前状态
```
$ git status
```
3. 添加到暂存区
```
$ git add 文件
$ git add . //所有
```
4. 对比差异
```
$ git diff 文件
```

5. 文件重命名

	5.1 通过编辑器修改文件名称
	```
	$ git rm style.css
	$ git add theme.css
	$ git commit -m "把 style.css 重命名为 theme.css"
	```
	5.2 通过git mv重命名或者移动
	```
	$ git mv theme.css style.css
	```
	5.3 移动文件
	```
	//移动文件
	$ mkdir css
	$ git mv style.css css/
	$ git commit -m "将 style.css 移动到 css/style.css"
	//移动文件夹
	$ mkdir asset
	$ git mv css asset
	$ git commit -m "将 css 文件夹移动到 asset 目录下"
	```

6. 删除文件

```
$ git rm asset/css/style.css
```

7.恢复文件
```
$ git checkout HEAD -- index.html //恢复上一次提交
$ git checkout HEAD^ -- index.html //恢复上一次的上一次的提交
```
8.恢复文件的历史版本
```
$ git revert 3353c2e

```
9.控制头部指针
```
$ git reset --hard d2f7fc2
$ git reset --soft d2f7fc2
$ git reset --mixed d2f7fc2
```

10.工作进度
```
//保存工作进度
$ git stash save "修改 comment.json"
//查看工作进度
$ git stash list
//对比区别
$ git stash show -p stash@{0}
//使用工作进度
$ git stash apply stash@{0}
//删除工作进度
$ git stash drop stash@{0}

```

11.分支
```
//查看分支
$ git branch
//创建分支
$ git branch mobile-feature
//分支切换
$ git checkout mobile-feature
//对比两个分支的文件区别
$ git diff master..mobile-feature index.html
//合并分支
$ git merge mobile-feature
//重命名分支
$ git branch -m bugfix bugfix-1
//删除分支
$ git branch -d bugfix-1

```

12.远程
```
//远程连接
$ git remote add origin https://github.com/tangzhenhua/test.git
//推送分支
$ git push -u origin master
//clone
$ git clone https://github.com/tangzhenhua/test.git test-zhang

//fetch
$ git fetch //提取更新
$ git merge //合并

//fork
在github上先fork
$ git clone https://github.com/tangzhenh/test.git test-lisi //将项目clone到本地
$ git config user.name "李四"
$ git config user.email "102376640@qq.com"
$ git push origin master

//添加协作者共同开发

```