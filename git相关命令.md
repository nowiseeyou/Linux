## git 相关命令 ##

    git rm -r --cache a/2.txt	//删除a目录下的2.txt文件
	git reset --hard HEAD		//回退版本 HEADE^(上一个)，HEADE^^(上两个版本)
	git reset HEAD				//清除 add 缓存区
	git revert HEAD				//撤销前一次 commit
	git checkout -b berry001		//创建并切换到该分支

	/*删除文件*/
	git rm web/z1.php 			
	git commit -m "修改的内容"
	git push -u origin berry001

	git remote add origin https://github.com/nowiseeyou/golang.git	//创建远程仓库地址
	git remote -v	//查看远程仓库地址
	git remote remove origin //删除远程仓库地址

	/*删除本地文件，如何恢复*/
	git checkout master
	git reset --hard

添加Git Config 内容
进入git bash终端， 输入如下命令：
git config --global credential.helper store
执行完后查看%HOME%目录下的.gitconfig文件，会多了一项：
[credential] helper = store
重新开启git bash会发现git push时不用再输入用户名和密码


	
	/*git push 免输入用户名 密码*/
	touch .git-credentials
	vim .git-credentials
			https://{username}:{password}@github.com