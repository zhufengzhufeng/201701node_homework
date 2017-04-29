
## 添加内容到文件中

```
echo '# hello' > README.md  //创建并追加
echo '# hello' >> README.md // 追加内容
```

```
echo "# git-homework" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/liangjingtao2016/git-homework.git
git push -u origin master
```

## 关联仓库

```
git remote add origin https://github.com/liangjingtao2016/git-homework.git
```
## 删除链接

```
git remote rm origin  //删除链接
```
## 推送到远程仓库

```
 -u 后置下次再推送只需要 git push就行啦！
git push origin master -u
git push
```

## 忽略文件
- .gitignore
 - 要忽略的文件需要在 .gitignore 建立之后再 add.

> git 不能提交空文件夹

## 在github上发布静态网站
- 必须当前项目下建立一个 gh-pages 的分支
- 将我们需要发布的内容推送到 gh-pages这个分支上
- 推送到远程仓库上即可
- github 会给你一个地址地址

```
git checkout -b gh-pages
touch index.html
git add index.html
git commit -m"index.html"
git push origin gh-pages
在setting中可以查找到网址+ 文件名即可 （默认会展示 index.html)
```

## git push origin
-

## 将文章发送给老师 (通过 github)
- 老师
- 组长fork (叉子) 老师代码，你的代码和我的一样，

## clone 自己的创库

```
git clone https://github.com/liangjingtao2016/201701node_homework.git leader-jmty
```
## 组长
- 添加

## 2.
- 组长克隆自己的代码
- 组员也克隆自己的代码
## 3.
- 组长建立自己组的文件夹，里面放入组员信息
- 组长提交到自己的创库
## 4.组员和组长建立联系

```
git remote add leader 组长的地址
```
- 组员拉取组长最新代码
```
git pull leader master
```
- 将自己写的内容放到文件夹中
- 组员将内容提交到自己的创库上
- 提交后发送pull request

## 5.
- 组长合并代码


