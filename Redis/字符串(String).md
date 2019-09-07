## 字符串(String) ##

**语法**

    redis 127.0.0.1:6397> COMMAND KEY_NAME

实例

    redsi 127.0.0.1:6397> SET runoobeky redis
	OK
	redis 127.0.0.1:6397> GET runoobkey
	"redis"

**Redis字符串命令**

- SET key value : 设置指定 key 的值。
- GET key : 获取指定key的值。
- GETRANGE key start end : 返回 key 中字符串值的子字符。
- GETSET key value : 将给的的 key 的值设为 value ，并返回 key 的旧值（old value）。
- GETBIT key offset : 对 key 所储存的的字符串值，获取指定偏移量上的位（bit）。
- MGET key1[key2..] : 获取所有（一个或多个）给定 key 值。
- SETBIT key offset value : 对 key 所储存的字符串值，设置或清除指定偏移量的位（bit）。
- SETTNX key value : 只有在 key 不存在时设置 key 的值。
- STRLEN key : 返回 key 储存的字符串值的长度。
- MSET key value [key value...] : 同时设置一个或多个key-value 对，当且仅当所有给定的key都不存在。
- 