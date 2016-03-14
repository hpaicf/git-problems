# git-problems
###git创建多个远程仓库

<br>git使用多个远程仓库还是挺简单的，只要在原有的仓库中再添加一个远程仓库链接就可以了，只是有几点注意的地方。 非常建议使用ssh的传输方式，可以在推送和拉去分支的时候免账户和密码登录。 还是拿我这个应用举例，我早先在coding.net上创建了一个远程仓库，名为bookmark，打开文件.git/config，有下面一段话
<br>
```javascript
  [remote "sae"]
	url = https://git.sinacloud.com/wohuodongv1/
	fetch = +refs/heads/*:refs/remotes/sae/*
```
<br>这段代码即是远程仓库的链接，如果想再添加一个远程仓库，只要在其下面再添加一个远程仓库的链接即可。我在github上创建了一个名字为bookmark-online的裸仓库，注意一定要是裸仓库，不然两个仓库就出现分裂了，比较难同步。 创建完成后，就可以上面的文件了，添加代码：
<br>
```javascript
 [remote "all"]
	url = https://git.sinacloud.com/wohuodongv1/
	url = https://github.com/hpaicf/wohuodong.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[gui]
```
<br>这样改动的文件就能使用“git push all”命令同时推送到这两个仓库中了。 其实，我们完全可以使用命令来完成此事，只是我比较喜欢研究命令的背后实现，才整出上面这么罗嗦的东东。使用如下命令添加远程代码库
<br>
```javascript
 git remote set-url --add 你的新仓库
[gui]
```
<br>这样做的一个好处是，不用指定分支名字，使用“git push”即可推送到两个仓库中，这是因为,git/config有如下代码的限制：
<br>
```javascript
 [branch "master"]
remote = origin
merge = refs/heads/master
[gui]
```
<br>这样，我们就能正常的推送代码到两个仓库中了。
