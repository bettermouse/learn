### case class
```scala
case class Student(name:String)
```
- 在idea中编译后,生成``Student.class``文件,用javap可以查看java编译器生成的字节码.
``javap Student.class ``
```字节码
public class Student implements scala.Product,scala.Serializable {
  public static scala.Option<java.lang.String> unapply(Student);
  public static Student apply(java.lang.String);
  public static <A> scala.Function1<java.lang.String, A> andThen(scala.Function1<Student, A>);
  public static <A> scala.Function1<A, Student> compose(scala.Function1<A, java.lang.String>);
  public java.lang.String name();
  public Student copy(java.lang.String);
  public java.lang.String copy$default$1();
  public java.lang.String productPrefix();
  public int productArity();
  public java.lang.Object productElement(int);
  public scala.collection.Iterator<java.lang.Object> productIterator();
  public boolean canEqual(java.lang.Object);
  public int hashCode();
  public java.lang.String toString();
  public boolean equals(java.lang.Object);
  public Student(java.lang.String);
}

```