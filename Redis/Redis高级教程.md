# Redis 高级教程 #


## Redis数据备份与恢复 ##

Redis SAVE 命令用于创建当前数据库的备份。

**语法 ：**

    redis 127.0.0.1:6397> SAVE

**实例 ：**

    redis 127.0.0.1:6397> SAVE
	OK

该命令将在redis 安装目录中创建 dump.rdb文件。

**恢复数据**

如果需要恢复数据，只需要将备份文件（dump.rdb） 移动到redis 安装目录并启动服务即可。获取 redis 目录可以使用 CONFIG 命令，如下所示 ： 

    redis 127.0.0.1:6397>CONFIG GET dir
	1) "dir"
	2) "/usr/local/redis/bin"

以上命令 CONFIG GET dir 输出的 redis 安装目录为 /user/local/redis/bin。

**Bgsave**

创建redis 备份文件也可以使用命令 BGSAVE ,该命令在后台执行。

**实例**

    redis 127.0.0.1:6397> BGSAVE

	Background saving started
	




