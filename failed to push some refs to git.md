###failed to push some refs to git
```javascript
error: failed to push some refs to 'https://git.sinacloud.com/wohuodongv1/'
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. Check out this branch and integrate the remote changes
hint: (e.g. 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
<br>本地库和git上的版本库有冲突，也就是可能两个版本不一样
<br>看了一下，好像在git版本库里上添加了一些文件但是本地没有
<br>
<br>基于这样的问题，如下是我Google之后解决的方法：
```javascript
git pull --rebase origin master
```
<br>再自动merge或手动merge冲突
<br>再次git push
<br>成功解决问题。


