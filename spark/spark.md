## 学习spark源码(标注那些工具可以用在自己的项目中)
### 监听器
### 日志收集
### spark rpc
### spark rdd
#### rdd记录的是一个dag图,是一个转换关系
```scala
//rdd的map方法
  /**
   * Return a new RDD by applying a function to all elements of this RDD.
   * 通过应用一个函数到这个rdd的所有元素 返回一个新的rdd
   */
  def map[U: ClassTag](f: T => U): RDD[U] = withScope {
    val cleanF = sc.clean(f)
    new MapPartitionsRDD[U, T](this, (context, pid, iter) => iter.map(cleanF))
  }
  
//MapPartitionsRDD的构造函数
  private[spark] class MapPartitionsRDD[U: ClassTag, T: ClassTag](
      var prev: RDD[T],
      f: (TaskContext, Int, Iterator[T]) => Iterator[U],  // (TaskContext, partition index, iterator)
      preservesPartitioning: Boolean = false,
      isFromBarrier: Boolean = false,
      isOrderSensitive: Boolean = false)
    extends RDD[U](prev) {}

//调用了 rdd的构造函数    
    /** Construct an RDD with just a one-to-one dependency on one parent */
    def this(@transient oneParent: RDD[_]) =
      this(oneParent.context, List(new OneToOneDependency(oneParent)))
//rdd 构造函数
abstract class RDD[T: ClassTag](
    @transient private var _sc: SparkContext,
    @transient private var deps: Seq[Dependency[_]]
  ) extends Serializable with Logging {      
//从上面可以得知 map方法得到了一个rdd,它的 deps: Seq[Dependency[_]] 是一个 List(new OneToOneDependency(oneParent))
```