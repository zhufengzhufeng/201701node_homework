``````## pwd
print working directory 打印当前工作目录
``````
## 告诉git当前我是谁``
- 用git第一次需要配置 以后都不需要,如果不配置则不能提交代码
```
git config --global user.name <github名字>
git config --global user.email <github邮箱>
git config --list 查看配置列表
```

## 初始化文件夹（告诉git哪个文件夹归git所管理）
```
git init
```
## cd 
- change directory

## mkdir 
- make directory

## 不能仓库套仓库
不能再初始化后的仓库下，在新建文件夹初始化仓库

## 查看文件中的内容
```
ls -a
```
## 删除文件夹
```
rm -rf .git
```

## 创建文件
```
touch index.txt
```

## 查看文件内容
```
cat index.txt
```

## vi编辑
```
vi index.txt
i 插入模式
ESC :wq保存并退出
q! 强制退出
```