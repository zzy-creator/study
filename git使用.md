**初次使用：**

下载git

设置global user.name和user.email

[https://aliyuque.antfin.com/alicode/docs/agoow0?#afRjq](https://aliyuque.antfin.com/alicode/docs/agoow0?#afRjq) 生成ssh密钥

在工作文件夹内 git init

git clone (ssh)

**工作流程：**

+ （本地创建相应分支）在相应分支上开发，并commit到这个分支上
+ push到远程的相应分支上

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2023/png/88656377/1676972553395-64beab29-3b4f-4cad-99cf-dd44a4c10b91.png" width="842.4241937334353" title="" crop="0,0,1,1" id="uaa3c6953" class="ne-image">

```basic
//切换到想要的工作目录
git init //在工作目录下执行，初始化一个本地仓库，目录下会出现.git文件
git clone ssh的那个 //clone代码
//修改代码、本地测试
git pull origin 远程分支名B //同步
git status //查看修改文件
git add/rm 修改文件名字 //将修改文件上传到暂存区
git checkout 分支A //切换到想要的分支A，在本地仓库中，各个分支是独立的
git commit -m “注释” //提交到本地该分支
git push origin 本地分支名A:某个远程分支名 //将本地分支A代码更新到远程分支上，origin为默认的远程主机名字
```

+ review
+ push到真正要的分支B（一般是班车分支）上

```basic
git branch -a可以查看全部的分支（包括远程的）;git branch查看本地的
git checkout 远程分支名B //切换到本地的远程分支名B的分支（初次，则会在本地创建一个，并同步远程的）
git pull origin 远程分支名B //同步
git status 
git merge 分支A //（当前在分支B下，若不在，则git checkout B）将分支A合并到分支B
git push origin B //将本地B上的内容push到远程B上
```
