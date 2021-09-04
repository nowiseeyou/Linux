## 解决git 发访问问题 ##

# IP1
	
	https://github.com.ipaddress.com/	

# IP2

	https://fastly.net.ipaddress.com/github.global.ssl.fastly.net#ipinfo 

#IP3(一组)
		
	https://github.com.ipaddress.com/assets-cdn.github.com 

# hosts
		140.82.113.4(IP1 Address) github.com 
		199.232.69.194(IP2 Address) github.global.ssl.fastly.net
		185.199.108.153(IP3 Address)  assets-cdn.github.com
		185.199.109.153(IP3 Address)  assets-cdn.github.com
		185.199.110.153(IP3 Address)  assets-cdn.github.com
		185.199.111.153(IP3 Address)  assets-cdn.github.com
	

## git 相关命令 ##
	
    git rm -r --cache a/2.txt	//删除a目录下的2.txt文件
	git reset --hard HEAD		//回退版本 HEADE^(上一个)，HEADE^^(上两个版本)
	git reset HEAD				//清除 add 缓存区
	git revert HEAD				//撤销前一次 commit
	git checkout -b berry001		//创建并切换到该分支

	# 删除文件
	git rm web/z1.php 			
	git commit -m "修改的内容"
	git push -u origin berry001
	git stash && git checkout master && git branch | grep -v "master" | xargs git branch -D  //删除除了master外的所有分支
	git stash : 备份分支修改
	
	# 创建远程仓库地址
	git remote add origin https://github.com/nowiseeyou/golang.git	
	git remote -v	//查看远程仓库地址
	git remote remove origin //删除远程仓库地址

	# 删除本地文件，如何恢复
	git checkout master
	git reset --hard

	# 拉取分支
	git fetch  origin xx
	git pull   origin xx

### Git Config ###

- 进入git bash终端， 输入如下命令：
	git config --global credential.helper store


- 执行完后查看%HOME%目录下的.gitconfig文件，会多了一项：
	[credential] helper = store



- 重新开启git bash会发现git push时不用再输入用户名和密码


	
	# git push 免输入 用户名 密码
	touch .git-credentials
	vim .git-credentials
			https://{username}:{password}@github.com

	# Linux ： git 命令行的颜色配置
	git config --global color.status auto	
	git config --global color.diff auto
	git config --global color.branch auto
	git config --global color.interactive auto


- 获取当前登陆用户：

	git config user.name   //获取当前登录的用户
	git config user.email  //获取当前登录用户的邮箱


- 修改登陆用户：

	git config --global user.name 'userName'    // 修改登陆账号，userName为你的git账号
	git config --global user.email 'email'      // 修改登陆邮箱，email为你的git邮箱
	git config --global user.password 'password'  // 修改登陆密码，password为你的git密码



- 配置用户名和邮箱：

	git config --global user.name "username"
	git config --global user.email "useremail@qq.com"



- 清除配置中纪录的用户名和密码，下次提交代码时会让重新输入账号密码：

	git config --system --unset credential.helper


- 查看git配置信息

	git config --list



- 执行命令之后，再次pull或push时会缓存输入的用户名和密码：

	git config --global credential.helper store




- 清除git缓存中的用户名的密码

	git credential-manager uninstall