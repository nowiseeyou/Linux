## 聊天室 ##

聊天室程序能让所有用户同时在线群聊，它分为客户端和服务器两个部分。

#### 客户端 ####

客户端程序有两个功能 ： 一是从标准输入终端读入用户数据，并将用户数据发送至服务器； 二是往标准输入终端打印服务器发送给他的数据。

#### 服务器 ####

服务器功能是接收客户数据，并把客户数据发送给每一个登录到该服务器上的客户端（数据发送者除外）。