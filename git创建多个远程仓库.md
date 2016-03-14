# git-problems
###git创建多个远程仓库
####源于
<br>我在做wohuodong这个项目的时候，之前因为把wohuodong放在新浪云上面的，方便，便于和后台接接口成功后，外网的他们访问看效果（因为新康园的云豆每个月也有免费的访问次数)，所以就用的新浪云，但是新浪云git代码管理，既是一个服务器，也是一个git仓库，然后我之后也想把这个项目放在自己的github上，方面以后自己的管理，所以就有了两个仓库，当我自己提交的时候，因为是新手，总是提示我如下错误：
```javascript
error: failed to push some refs to 'https://git.sinacloud.com/wohuodongv1/'
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. Check out this branch and integrate the remote changes
hint: (e.g. 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
<br>
<br>查了很久，感觉可能是因为我本地项目远程了两个仓库，但是配置并没有设置同步两个，所以可能有错误，然后我就查询git远程两个仓库
<br>就解决了
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
