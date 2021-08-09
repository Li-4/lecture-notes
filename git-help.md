git init 初始化本地库

git config user.name <username> 仓库级别用户名
git config user.email <email>   仓库级别邮箱
git config --global user.name <user.name> 系统用户级别用户名
git config --global user.email <email>    系统用户级别邮箱
级别优先级：就近原则：项目级别优先于系统用户级别，二者都有时采用项目级别的签名

git status 查看工作区、暂存区状态
git add <file> 将工作区的“新建/修改”添加到暂存区
git commit -m "commit massage" <file> 将暂存区的内容提交到本地库

git log 查看版本记录
git log --pretty=oneline 每条日志只显示一行
git log --oneline 	 显示一行，hash减少
*git reflog 		 在oneline的基础上显示HEDA@{移动到当前版本需要的步数}

版本的前进回退：
本质是HEAD指针的移动
基于索引值操作：git reset --hard <hash索引>
使用^符号：git reset --hard HEAD^
	只能后退,一个^表示一步
使用~符号：git reset --hard HEAD~n
	只能后退，后退n步
git reset 参数
	--soft
	    仅仅在本地库移动HEAD指针
	相当于add后没有commit
	--mixed
	    在本地库移动HEAD指针，重置暂存区
	相当于没有add没有commit
	--hard
	    在本地库移动HEAD指针，重置暂存区,重置工作区


删除文件并找回：
	前提：删除前，文件存在时的状态提交到了本地库
	操作：git reset --hard <指针位置>
		指针指向文件还未删除的记录即可

比较文件：
	git diff [文件名]
	    将工作区的文件和暂存区进行比较
	git diff [本地库历史版本][文件名]
	    将工作区的文件和本地库历史记录比较
	不带文件名可以比较多个文件

分支管理：
	分支：在版本控制过程中，使用多条线同时推进多个任务。
	分支的好处：
		同时并行推进多个功能的开发，提高才发效率
		各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任	何影响。失败的分支删除重新开始即可。
	分支操作：
		创建分支
		git branch [分支名]
		查看分支
		git branch -v
		切换分支
		git checkout [分支名]
		合并分支
			一：切换到接受修改的分支上
			git checkout [被合并的分支名]
			二：执行 merge 命令
			git merge [有新内容的分支名]
		解决冲突
			一：编辑文件删除特殊符号
			二：把文件修改到满意的程度，保存退出
			三：git add [文件名]
			四：git commit -m “message”
				此时不能带具体文件名

远程库地址添加本地别名
	git remote add [别名] [远程地址]
	查看
	git remote -v

推送到远程库
	git push [别名/地址] [分支名]

克隆
	命令
	git clone [远程地址]
	效果
	    完整的把克隆库下载到本地
	    创建远程地址别名
	    初始化本地库
拉取
	pull=fetch+merge
	git fetch [远程库地址别名] [远程分支名]
	git merge [远程库地址别名/远程分支名]
	git pull [远程库地址别名] [远程分支名]