### netty的ByteBuf
#### java nio Buffer
- 在数据传输的过程中,会用到缓冲区(ByteBuffer),它有以下缺陷
  1. ByteBuffer大小固定,不能动态扩展和收缩,当需要编码的POJO对象大于ByteBuffer时,发生越界.(其实就是需要检查)
  2. 
- 从内存分配的角度看,ByteBuf可以分为两类
  1. 堆内存(HeapByteBuf)字节缓冲区:特点是内存的分配和回收速度快,可以被jvm自动回收;缺点就是如果进行socket的I/O读写,
  需要额外做一次内存复制.将堆内存对应的缓冲区复制到channel中,性能会有一定的下降.
  2. 直接内存(DirectByteBuf)字节缓存区:非堆内存,它在堆外进行内存分配,相对于堆内存,它的分配和
  回收速度会慢一些,但是将它写入或者从socket channel中读取时,由于少了一次内存复制,速度比堆内存快.
  