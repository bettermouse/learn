# nio与netty 
## 现状
如今,在java写的框架中,远程通信,大部分都使用了nio/netty.kafka使用了nio,在spark中
,2.0以前的的版本节点之间的通信用了akka,从2.0开始,使用netty.
* kafka为什么要用nio
### nio
```java

```
## 为什么要用netty?
- netty 简化了nio的开发.
[Java NIO开发需要注意的陷阱](http://www.cnblogs.com/pingh/p/3224990.html ) 
1. 处理事件忘记移除key
2. 正确处理OP_WRITE,OP_WRITE处理不当很容易导致CPU 100% 
- nio的主要逻辑是``selector.selectedKeys();``检测到准备好的Channel,进行相应的数据处理.
```java
                selector.select(1000);
                //	int select = selector.select();
                Set<SelectionKey> selectedKeys = selector.selectedKeys();
                Iterator<SelectionKey> it = selectedKeys.iterator();
                SelectionKey key = null;
                while (it.hasNext()) {
                    key = it.next();
                    //移除key
                    it.remove();
                    try {
                        handleInput(key);
                
```
- netty的主体思想也应该是一个死循环,不断检测已经就绪的事件,然后进行处理.
- 下面的部分主要参考 netty权威指南2
### 