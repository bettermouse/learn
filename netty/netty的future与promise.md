a | b | c
:--- | ---:|:---:
ddddddddddd1 | 2|xxx
3 |dddddddddddddddddddd 4|xxxxxxxxx

-  netty写消息后会有一个future.这个future可以用来监听消息的成功和失败.
这个东西的实现,肯定是在调用channel.write(),把对应的字节写出去后,来设置的.

