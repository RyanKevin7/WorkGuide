### git相关命令

```
git pull         ## 拉取
git add --all    ## 添加所有文件  （新文件需要先add）
git commit			 ## 提交
git push         ## 推送
git status 			 ## 查看状态

git reflog                         ## 查看本地提交记录
git reset -r-hard FETCH_HEAD        ## 回退
git reset --hard HEAD@{2}          ## 回退到本地最新代码

git merge master		        ## 合并 master 分支到当前分支

git branch dev   		      ## 创建 dev 分支
git checkout dev			    ## 切换到 dev 分支
```



### 上传工程至github

#### 创建github 

- URL：https://github.com
- 新建github账户
- new repositories     # 新建信息库



#### 安装git

- URL： https://git-scm.com/downloads



#### 上传工程

```
cd csccnn  ## 路径切换到该工程下
git init   ## 初始化仓库
git add    ## 项目下的文件添加到仓库
git commit  ## 提交到本地仓库 会提示要求输入 user.name && user.email 
		
git commit -m '备注'   ## 提交时加上备注
git remote add origin https://github.com/zhengkai7/ccnn.git  ## 本地仓库关联到GitHub
git push -u origin master   ## 代码上传到GitHub上
```



#### 更新项目

- 当以后需要更新项目的时候有四步需要走
  - 第一步：执行   `git pull `   命令将GitHub上的代码当下来合并代码，防止提交新代码的时候起冲突
  - 第二步：执行   `git add`     命令将代码添加到仓库
  - 第三步：执行   `git commit `    命令将代码提交到仓库
  - 第四步：执行   `git push `      命令将代码提交到GitHub 







