### 5 集合
#### 5.4.1.序列
```scala
//可变的序列 import scala.collection.mutable._
import scala.collection.mutable.ListBuffer

object MutListDemo extends App{
  //构建一个可变列表，初始有3个元素1,2,3
  val lst0 = ListBuffer[Int](1,2,3)
  //创建一个空的可变列表
  val lst1 = new ListBuffer[Int]
  //向lst1中追加元素，注意：没有生成新的集合
  lst1 += 4
  lst1.append(5)

  //将lst1中的元素最近到lst0中， 注意：没有生成新的集合
  lst0 ++= lst1

  //将lst0和lst1合并成一个新的ListBuffer 注意：生成了一个集合
  val lst2= lst0 ++ lst1

  //将元素追加到lst0的后面生成一个新的集合
  val lst3 = lst0 :+ 5
}
```

### 6.类、对象、继承、特质
#### 6.1.类
##### 6.1.2.构造器
```scala
//注意：主构造器会执行类定义中的所有语句
/**
  *每个类都有主构造器，主构造器的参数直接放置类名后面，与类交织在一起
  */
class Student(val name: String, val age: Int){
  //主构造器会执行类定义中的所有语句
  println("执行主构造器")

  try {
    println("读取文件")
    throw new IOException("io exception")
  } catch {
    case e: NullPointerException => println("打印异常Exception : " + e)
    case e: IOException => println("打印异常Exception : " + e)
  } finally {
    println("执行finally部分")
  }

  private var gender = "male"

  //用this关键字定义辅助构造器
  def this(name: String, age: Int, gender: String){
    //每个辅助构造器必须以主构造器或其他的辅助构造器的调用开始
    this(name, age)
    println("执行辅助构造器")
    this.gender = gender
  }
}



/**
  *构造器参数可以不带val或var，如果不带val或var的参数至少被一个方法所使用，
  *那么它将会被提升为字段
  */
//在类名后面加private就变成了私有的
class Queen private(val name: String, prop: Array[String], private var age: Int = 18){
  
  println(prop.size)

  //prop被下面的方法使用后，prop就变成了不可变得对象私有字段，等同于private[this] val prop
  //如果没有被方法使用该参数将不被保存为字段，仅仅是一个可以被主构造器中的代码访问的普通参数
  def description = name + " is " + age + " years old with " + prop.toBuffer
}

object Queen{
  def main(args: Array[String]) {
    //私有的构造器，只有在其伴生对象中使用
    val q = new Queen("hatano", Array("蜡烛", "皮鞭"), 20)
    println(q.description())
  }
}

```