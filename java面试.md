### Java基础

#### java特点

```
是一门面向对象的编程语言，简单，安全，摒弃了C++里难以理解的多继承和指针的概念，能够跨平台使用，支持网络编程且方便，支持多线程，具有强类型机制、异常处理、垃圾的自动收集
```

#### 什么是跨平台使用？原理是什么？

```
是指编写Java代码后，进行预编译，把.java文件转换为.class文件，.class文件是字节码文件，该文件是任何系统都可以识别的。并且Java程序是通过java虚拟机在系统平台上运行的，只要该系统可以安 装相应的java虚拟机，该系统就可以运行java程序。
```

#### 面向对象

```
面向对象是一种思想，是模型化的，但其底层还是面向过程，把面向过程抽象成类，然后封装，方便使用。使得可以设计出低耦合的系统，更便于去维护、复用、扩展。
```

##### 封装

抽象是封装的一种表现形式，将一个对象的属性私有化，同时提供一些可以被外界访问的属性的方法

##### 继承

1.子类拥有父类非 private 的属性和方法。

2.子类可以拥有自己属性和方法，即子类可以对父类进行扩展。

3.子类可以用自己的方式实现父类的方法。

##### 多态

指程序中定义的引用变量所指向的具体类型和通过该引用变量发出 的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量到 底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的 方法，必须在由程序运行期间才能决定。

在Java中有两种形式可以实现多态：继承（多个子类对同一方法的重写）和接口 （实现接口并覆盖接口中同一方法）。

#### GC(Garbage Collection)垃圾收集

```
jvm认为--没有指向，没有被引用的时候，该资源为垃圾就回收
```

#### JVM调优

##### 调试的原则

1.多数的java应用不需要在服务器上进行GC优化，虚拟机内部已经有很多优化来保证应用的稳定运行，所有不会为了调优而调优，不当的调优会适得其反

2.在应用上线之前，先考虑将机器的JVM参数设置到最优

3.在进行GC优化前，需要确认项目的架构和代码等已经没有优化空间。我们不能指望一个系统架构有缺陷或者代码层次优化没有穷尽的应用，通过GC优化令其性能达到一个质的飞跃

4.GC优化是一个系统而复杂的工作，没有万能的调优策略可以满足性能指标。GC优化必须建立在我们深入理解各种垃圾回收器的基础之上，才能有事半功倍的效果

5.处理吞吐量和延迟问题时，垃圾处理器能使用的内存越大，及Java堆空间越大垃圾收集效果越好，应用运行越流畅。这称为GC内存最大化原则

6.在(吞吐量、延迟、内存)中选择其中两个进行JVM调优，称之为GC调优三选二

##### 什么情况下需要调优

- Heap内存(老年代)持续上涨达到设置的内存值
- Full GC次数频繁
- GC停顿(Stop World)时间过长 (超过1秒，具体值按应用场景而定)
- 应用出现OutOfMemory等内存异常
- 应用出现OutOfDirectMemoryError等内存异常(failed to allocate 16777216byte(s) of direct memory (used:105696415,max:1073741824))
- 应用中有使本地缓存且占用大量内存空间
- 系统吞吐量与响应性能不高或下降
- 应用的CPU占用率过高不下或内存占用过高不下

#### JVM内存分布

#### 变量

存储数据的空间。命名规范：由字母，数字，_,组成，不能以数字开头。

#### 基本数据类型

| 类型   | 类型名称     | 关键字  | 占用内存 | 取值范围                                                  | 作为成员变量的默认值 |
| ------ | ------------ | :------ | -------- | --------------------------------------------------------- | -------------------- |
| 整型   | 字节型       | byte    | 1字节    | -128(-2^7) ~ 127(2^7-1)                                   | 0                    |
|        | 短整型       | short   | 2字节    | -32768(-2^15) ~ 32767(2^15-1)                             | 0                    |
|        | 整型         | int     | 4字节    | -2147483648(-2^31) ~ 2147483647(2^31-1)                   | 0                    |
|        | 长整型       | long    | 8字节    | -9223372036854775808(-2^63) ~ 9223372036854775807(2^63-1) | 0L                   |
|        | 单精度浮点型 | float   | 4字节    | -3.403E38 ~3.403E38                                       | 0.0F                 |
| 浮点型 | 双精度浮点型 | double  | 8字节    | -1.798E308 ~ 1.798E308                                    | 0.0D                 |
| 字符型 | 字符型       | char    | 2字节    | 0~65535                                                   | '\u0000'             |
| 布尔型 | 布尔型       | boolean | 1字节    | 只有false,true两个值                                      | false                |

#### 运算符

#### 数组

- ##### 复制


  ```java
  System.arraycopy(a,1,b,0,4)
      //参数1：源数组
      //参数2：源数组起始下标
      //参数3：目标数组
      //参数4：目标数组的起始下标
      //参数5:要复制的元素个数
  ```

  ```java
  int[] b = Arrays.copyOf(a,a.length+1);//数组的扩容
  	//a:源数组
  	//b:目标数组
  	//a.length+1：a的长度+1
  ```
- 排序

  - Arrays.sort(arr);

  ```java
  int[] arr = new int[10];
  for(int i=0;i<arr.length;i++){
      arr[i] = (int)(Math.random()*100);
      System.out.println(arr[i]);
  }
  Arrays.sort(arr); //对arr进行升序排列
  System.out.println("排序后:");
  for(int i=0;i<arr.length;i++){
      System.out.println(arr[i]);
  }
  System.out.println("倒序输出"); //只是倒着显示，但数组中数据没有改变
  for(int i=arr.length-1;i>=0;i--){
      System.out.println(arr[i]);
  }
  ```

#### 重载(行为多态)

发生在同一个类中，方法名相同参数列表不同（参数类型不同、个数不 同、顺序不同），与方法返回值和访问修饰符无关，即重载的方法不能根据返回 类型进行区分

#### 重写

发生在父子类中，方法名、参数列表必须相同。返回值小于等于父类,抛 出的异常小于等于父类，访问修饰符大于等于父类（里氏代换原则）；如果父类 方法访问修饰符为private则子类中就不是重写。(两同两小一大)

#### static(静态的)

属于类，存储在方法区中，(一次加载一直使用)，先于对象存在

- 被static修饰的变量或者方法是独立于该类的任何对象，这些变量不属于任何一个实例对象，而是被类的实例对象所共享
- 在该类被第一次加载的时候，就会加载被static修饰的部分，而且只在类第一次使用时加载并进行初始化，在后续可以根据需要再次复制
- static变量值在类加载的时候分配空间，以后创建类对象的时候不会重新分配。赋值的话，是可以任意赋值的。
- 被static修饰的变量或者方法是优先于对象存在的，也就是说当一个类加载完毕后，及时没有创建对象也可以访问

##### tips:

- 静态变量只能访问静态资源。
- 非静态既可以访问非静态的，也可以访问静态的。

#### 构造器

构造器不能被继承，因此不能被重写，可以重载。可以用来初始化对象，传值。采用类名.{}

#### this,super

- super: 它引用当前对象的直接父类中的成员（用来访问直接父类中被隐藏的父类中成员数据或函数，基类与派生类中有相同成员定义时如：super.变量名 super.成员函数据名（实参）
- this：它代表当前对象名（在程序中易产生二义性之处，应使用this来指明当前对象；如果函数的形参与类中的成员数据同名，这时需用this来指明成员变量名）
- super()和this()类似,区别是，super()在子类中调用父类的构造方法，this()在本类内调用本类的其它构造方法。
- super()和this()均需放在构造方法内第一行。
- 尽管可以用this调用一个构造器，但却不能调用两个。this和super不能同时出现在一个构造函数里面，因为this必然会调用其它的构造函数，其它的构造函数必然也会有super语句的存在，所以在同一个构造函数里面有相同的语句，就失去了语句的意义，编译器也不会通过。
- this()和super()都指的是对象，所以，均不可以在static环境中使用。包括：static变量,static方法，static语句块。
- 从本质上讲，this是一个指向本对象的指针, 然而super是一个Java关键字。

#### final(最终的最后的)

- final 修饰的类叫最终类，该类不能被继承。
- final 修饰的方法不能被重写。
- final 修饰变量：变量不可被改变，修饰方法：方法不可被重写，修饰类：类不能被继承，只能在声明时或构造方法初始化
- Static final 常量：1)常量必须声明同时初始化2)通过类名点来访问，不可被改变3)建议：常量名所有字母都大写，多个单词用_分隔

#### 抽象类和接口的对比

抽象类是用来捕捉子类的通用特性的。接口是抽象方法的集合。

从设计层面来说，抽象类是对类的抽象，是一种模板设计，接口是行为的抽象，是一种行为的规范。

##### 相同点

- 接口和抽象类都不能实例化
- 都位于继承的顶端，用于被其他实现或继承
- 都包含抽象方法，其子类都必须覆写这些抽象方法

##### 不同点

| 参数       | 抽象类                                                                                            | 接口                                                                       |
| ---------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| 声明       | 抽象类使用abstract关键字声明                                                                      | 接口使用interface关键字声明                                                |
| 实现       | 子类使用extends关键字来继承抽象类。如果子类不是抽象类的话，它需要提供抽象类中所有声明的方法的实现 | 子类使用implements关键字来实现接口。它需要提供接口中所有声明的方法的实现。 |
| 构造器     | 抽象类可以有构造器                                                                                | 接口不能有构造器                                                           |
| 访问修饰符 | 抽象类中的方法可以时任意访问修饰符                                                                | 接口方法默认修饰符时public.并且不允许定义为private或者protected            |
| 多继承     | 一个类最多只能继承一个抽象类                                                                      | 一个类可以实现多个接口                                                     |
| 字段声明   | 抽象类的字段声明可以时任意                                                                        | 抽象的字段默认都是static和final的                                          |

##### 普通类和抽象类的区别

普通类不能包含抽象方法，抽象类可以包含抽象方法。

抽象类不能直接实例化，普通类可以直接实例化。

遵循原则：

- 行为模型应该总是通过接口而不是抽向类来定义，所以通常是有限选用接口，尽量少用抽象类。
- 选择抽象类的时候通常时如下情况：需要定义子类的行为，又要为子类提供通用的功能。

#### 二进制

1.必须确定二进制的范围。

2.首位为符号位，1表示负数，0表示整数。

| 值 | 二进制 |
| -- | ------ |
| -8 | 1000   |
| -7 | 1001   |
| -6 | 1010   |
| -5 | 1011   |
| -4 | 1100   |
| -3 | 1101   |
| -2 | 1110   |
| -1 | 1111   |
| 0  | 0000   |
| 1  | 0001   |
| 2  | 0010   |
| 3  | 0011   |
| 4  | 0100   |
| 5  | 0101   |
| 6  | 0110   |
| 7  | 0111   |

#### String

##### 常用方法

- indexOf:返回指定字符的索引
- charAt():返回指定索引处的字符。
- replace():字符串替换
- trim():去除字符串的byte类型数组。
- split():分割字符串，返回一个分割后
- length():返回字符串长度。
- getBytes():返回字符串的byte类型数组
- toLowerCase():将字符串转成小写字母
- toUpperCase():将字符串转成大写字母
- substring():截取字符串
- equals():字符串比较

#### String和StringBuffer、stringaabuffer

String类中使用字符数组保存字符串，private final char value[]，所以 string对象是不可变的。

StringBuilder与StringBuffer都继承自AbstractStringBuilder类，在AbstractStringBuilder中也是使用字符数组保存字符串，char[] value，这两种对象都是可变的。线程安全性String中的对象是不可变的，也就可以理解为常量，线程安全。AbstractStringBuilder是StringBuilder与StringBuffer的公共父类，定义了一些字符串的基本操作，如expandCapacity、append、insert、indexOf等公共方法。StringBuffer对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。StringBuilder并没有对方法进行加同步锁，所以是非线程安全的。

##### 性能

每次对String 类型进行改变的时候，都会生成一个新的String对象，然后将指针指向新的String 对象。

StringBuffer每次都会对StringBuffer对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用StirngBuilder 相比使用StringBuffer 仅能获得10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

##### 对于三者使用的总结：

如果要操作少量的数据用 = String

单线程操作字符串缓冲区 下操作大量数据 = StringBuilder

多线程操作字符串缓冲区 下操作大量数据 = StringBuffer

#### IO

- InputStream/Reader:所有输入流的超类，前者是字节输入流，后者是字符输入流
- OutputStream/Write:所有输出流的超类，前者是字节输出流，后者是字符输出流

|              | 输入流input读取                                             |                                                                                            | 输出流output写出                                                                               |                                                                                                |
| ------------ | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 低级流节点流 | 字节输入流                                                  | 字符输入流                                                                                 | 字节输出流                                                                                     | 字符输出流                                                                                     |
|              | FileInputStream作用：从文件中读取字节数据                   |                                                                                            | FileOutputStream作用：将数据写入到文件按中                                                     |                                                                                                |
| 处理流高级流 | BufferedInputStream缓冲字节输入流，作用：块读取字节数据加速 | InpubtStreamReader转换输入流，作用：1、衔接字节输入流与字符输入流。2、读取的字节准换为字符 | BufferedOutputStream缓冲字节输出流，作用：块写字节加速的                                       | OutputStreamWriter转换输出流，作用：1、衔接字节输出流与字符输出流。2、将写出的字符转换为字节   |
|              | ObjectInputStream对象输入流，作用：进行对象的反序列化       | BufferedReader缓冲字符输入流，作用：1、块读写文本数据加速。2、按行读取字符串readLine       | ObjectOutputStream对象输出流，作用：进行对象序列化的将对象转换为一组字节的过程称为对此昂序列化 | PrintWriter具有自动行刷新的缓冲字符输出流。作用：1、块写文本数据加速。2、按行写出字符串println |

#### File的常见方法

- File.exists():检测文件路径是否存在
- File.createFile():创建文件
- File.createDirectory():创建文件夹
- File.delete():删除一个文件或目录
- File.copy():复制文件。
- File.move():移动文件。
- File.size():查看文件个数
- File.read():读取文件。
- File.write():写入文件。

File file = new File();    没有创建文件，创建的是文件的对象

#### 异常的结构

##### Throwable:是所有错误与异常的超类，用于指示发生了异常情况

- Exception（异常）：

  - IOException(IO异常)
    - EOFException
    - FileNotFountException(没找到指定文件)
  - ClassCastException(类型转换异常)
  - RuntimeException(运行时异常)
    - NullPointerException(空指针异常)
    - ArithmeticException(算数异常)
    - IndexOutOfBoundsException(下标越界异常)
- Error（错误）：程序中无法处理的错误，表示运行应用程序中出现了严重的错误。

  - VirtuMachineError(内存不足错误)
    - StackOverFlowError(栈溢出错误)
    - OutOfMemoryError(内存不足错误)
  - AWTError

通过 try-catch 对它进行捕获处理。

- try – 用于监听。将要被监听的代码(可能抛出异常的代码)放在try语句块之内，当try语句块内发生异常时，异常就被抛出。
- catch – 用于捕获异常。catch用来捕获try语句块中发生的异常。
- finally – finally语句块总是会被执行。它主要用于回收在try块里打开的物力资源(如数据库连接、网络连接和磁盘文件)。只有finally块，执行完成之后，才会回来执行try或者catch块中的return或者throw语句，如果finally中使用了 return或者throw等终止方法的语句，则就不会跳回执行，直接停止。
- throw – 用于抛出异常。
- throws – 用在方法签名中，用于声明该方法可能抛出的异常

#### Error和Exception区别

- Error 类型的错误通常为虚拟机相关错误，如系统崩溃，内存不足，堆栈溢出 等，编译器不会对这类错误进行检测，JAVA 应用程序也不应对这类错误进行捕 获，一旦这类错误发生，通常应用程序会被终止，仅靠应用程序本身无法恢复；
- Exception 类的错误是可以在应用程序中进行捕获并处理的，通常遇到这种错 误，应对其进行处理，使应用程序可以继续正常运行。

#### throw和throws的区别？

- throw 关键字用在方法内部，只能用于抛出一种异常，用来抛出方法或代码块中 的异常，受查异常和非受查异常都可以被抛出。
- throws 关键字用在方法声明上，可以抛出多个异常，用来标识该方法可能抛出 的异常列表。一个方法用 throws 标识了可能抛出的异常列表，调用该方法的方法中 必须包含可处理异常的代码，否则也要在方法签名中用 throws 关键字声明相应的异 常。

#### final、finally、finalize有什么区别

- final可以修饰类、变量、方法，修饰类表示该类不能被继承、修饰方法表示该方 法不能被重写、修饰变量表示该变量是一个常量不能被重新赋值。
- finally一般作用在try-catch代码块中，在处理异常的时候，通常我们将一定要执 行的代码方法finally代码块中，表示不管是否出现异常，该代码块都会执行，一般用 来存放一些关闭资源的代码。
- finalize是一个方法，属于Object类的一个方法，而Object类是所有类的父类， Java 中允许使用finalize()方法在垃圾收集器将对象从内存中清除出去之前做必要的 清理工作。

#### 线程

#####  线程的生命周期

| 状态名称     | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| NEW          | 初始状态，线程被构建，但是还没有调用start()方法              |
| RUNNABLE     | 运行状态，Java线程将操作系统中的就绪和运行两种状态称为“运行中” |
| BLOCKED      | 阻塞状态，表示线程阻塞于锁                                   |
| WAITING      | 等待状态，表示线程进入等待状态，进入该状态表示当前线程需要等待其他线程做出一些特定动作（通知或者中断） |
| TIME_WAITING | 超时等待状态，该状态不同于WAITING，他是可以在指定时间自行返回的 |
| TERMINATED   | 终止状态，表示当前线程已经执行完毕                           |

线程由两种实现方式：1、继承Thread类重写run方法。2、实现Runnable接口重写run方法

####  容器

#####  Collection

- set
  - SortedSet
    - TreeSet:基于红黑树实现，支持有序性操作，例如根据一个范围查找元素的操作。但是查找效率不如 HashSet，HashSet 查找的时间复杂度为 O(1)，TreeSet 则为 O(logN)。
  - HashSet:基于哈希表实现，支持快速查找，但不支持有序性操作。并且失去了元素的插入顺序信息，也就是说使用 Iterator 遍历 HashSet 得到的结果是不确定的。
  - LinkedHashSet:具有 HashSet 的查找效率，并且内部使用双向链表维护元素的插入顺序。
- List
  - ArrayList:基于动态数组实现，支持随机访问。	
  - vector:和 ArrayList 类似，但它是线程安全的。
  - LinkedList:基于双向链表实现，只能顺序访问，但是可以快速地在链表中间插入和删除元素。不仅如此，LinkedList 还可以用作栈、队列和双向队列。

- Queue
  - LinkedList:可以用它来实现双向队列。
  - PriorityQueue:基于堆结构实现，可以用它来实现优先队列。

#####  常用方法

boolean add(E e):向集合中添加一个元素，成功添加则返回true

int size():返回当前集合的元素个数

boolean isEmpty():判断当前集合是否为空集.当且仅当size=0时返回true.

void clear():清空集合

boolean contains(Object o):判断集合是否包含给定元素

boolean remove(Object o):从集合中删除给定元素，成功删除返回true.

boolean addAll(Collection c):将给定集合所有元素添加到当前集合中。

boolean removeAll(Collection c):删除当前集合中与给定集合的公有元素。

boolean containsAll(Collection c):判断当前集合是否包含给定集合中的所有元素。

Iterator iterator():获取用于遍历当前集合的迭代器

T[] toArray(T[] t):将当前集合转换为一个数组。参数为要转换的数组。

#####  集合的遍历

```java
public class IteratorDemo {
    public static void main(String[] args) {
        Collection c = new ArrayList();
        c.add("one");
        c.add("two");
        c.add("three");
        c.add("four");
        c.add("five");
        System.out.println(c);
        //获取迭代器
        Iterator it = c.iterator();
        /*
            迭代器提供的相关方法：
            boolean hasNext()
            判断集合是否还有元素可以遍历

            E next()
            获取集合下一个元素(第一次调用时就是获取第一个元素，以此类推)
         */
        while(it.hasNext()){
            String str = (String)it.next();
            System.out.println(str);         
        }
        System.out.println(c);
    }
}
 /*
                    迭代器要求遍历的过程中不得通过集合的方法增删元素
                    否则会抛出异常:ConcurrentModificationException
                 */
//                c.remove(str);
                /*
                    迭代器的remove方法可以将通过next方法获取的元素从集合
                    中删除。
                 */
```

##### 增强型for循环

```
for(元素类型 变量名 : 集合或数组){
    循环体
}
```

```java
public class NewForDemo {
    public static void main(String[] args) {
        String[] array = {"one","two","three","four","five"};
        for(int i=0;i<array.length;i++){
            String str = array[i];
            System.out.println(str);
        }

        for(String str : array){
            System.out.println(str);
        }
        Collection c = new ArrayList();
        c.add("one");
        c.add("two");
        c.add("three");
        c.add("four");
        c.add("five");
        //迭代器遍历
        Iterator it = c.iterator();
        while(it.hasNext()){
            String str = (String)it.next();
            System.out.println(str);
        }
        //新循环遍历
        for(Object o : c){
            String str = (String)o;
            System.out.println(str);
        }

    }
}
```

#####  泛型

泛型也称为参数化类型,允许我们在使用一个类时指定它当中属性,方法参数或返回值的类型.

- 泛型在集合中被广泛使用,用来指定集合中的元素类型.
- 有泛型支持的类在使用时若不指定泛型的具体类型则默认为原型Object

```java
/**
 * JDK5推出时，推出了一个新的特性:增强型for循环
 * 也称为新循环，它可以用相同的语法遍历集合或数组。
 *
 * 新循环是java编译器认可的，并非虚拟机。
 */
public class NewForDemo {
    public static void main(String[] args) {
        String[] array = {"one","two","three","four","five"};
        for(int i=0;i<array.length;i++){
            String str = array[i];
            System.out.println(str);
        }

        for(String str : array){
            System.out.println(str);
        }
        /*
         *  泛型 JDK5之后推出的另一个特性。
         * 泛型也称为参数化类型，允许我们在使用一个类时指定它里面属性的类型，
         * 方法参数或返回值的类型，使得我们使用一个类时可以更灵活。
         * 泛型被广泛应用于集合中，用来指定集合中的元素类型。
         * 支持泛型的类在使用时如果未指定泛型，那么默认就是原型Object
         *
         * Collection接口的定义
         * public interface Collection<E> ... {
         *
         * Collection<E> 这里的<E>就是泛型
         *
         * Collection中add方法的定义，参数为E
         * boolean add(E e)
         */
        Collection<String> c = new ArrayList<>();
        c.add("one");//编译器会检查add方法的实参是否为String类型
        c.add("two");
        c.add("three");
        c.add("four");
        c.add("five");
//        c.add(123);//编译不通过
        //迭代器遍历
        //迭代器也支持泛型，指定的与其遍历的集合指定的泛型一致即可
        Iterator<String> it = c.iterator();
        while(it.hasNext()){
            //编译器编译代码时会根据迭代器指定的泛型补充造型代码
            String str = it.next();//获取元素时无需在造型
            System.out.println(str);
        }
        //新循环遍历
        for(String str : c){
            System.out.println(str);
        }

    }
}
```

#####  List集合及常见方法

list集合有两个常用的实现类:

- java.util.ArrayList:内部使用数组实现，查询性能更好。

- java.util.LinkedList:内部使用链表实现，增删性能更好，首尾增删性能最佳。

  性能没有苛刻要求时，通常使用ArrayList。

E get(int index):获取指定下标index处对应的元素

E set(int index, E e):将给定元素设置到index指定的位置，返回值为该位置被替换的元素。

```java
package collection;

import java.util.ArrayList;
import java.util.List;

/**
 *  List集合
 *  List是Collection下面常见的一类集合。
 *  java.util.List接口是所有List的接口，它继承自Collection。
 *  常见的实现类:
 *  java.util.ArrayList:内部由数组实现，查询性能更好。
 *  java.util.LinkedList:内部由链表实现，增删性能更好。
 *
 *  List集合的特点是:可以存放重复元素，并且有序。其提供了一套可以通过下标
 *  操作元素的方法。
 */
public class ListDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
//        List<String> list = new LinkedList<>();

        list.add("one");
        list.add("two");
        list.add("three");
        list.add("four");
        list.add("five");

        /*
            E get(int index)
            获取指定下标对应的元素
         */
        //获取第三个元素
        String e = list.get(2);
        System.out.println(e);

        for(int i=0;i<list.size();i++){
            e = list.get(i);
            System.out.println(e);
        }

        /*
            E set(int index,E e)
            将给定元素设置到指定位置，返回值为该位置原有的元素。
            替换元素操作
         */
        //[one,six,three,four,five]
        String old = list.set(1,"six");
        System.out.println(list);
        System.out.println("被替换的元素是:"+old);
    }
}
```



void add(int index,E e):将给定元素插入到index指定的位置

E remove(int index):删除并返回下标index处对应的元素。

```java
/**
 * List集合提供了一对重载的add,remove方法
 */
public class ListDemo2 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("one");
        list.add("two");
        list.add("three");
        list.add("four");
        list.add("five");
        System.out.println(list);
        /*
            void add(int index,E e)
            将给定元素插入到指定位置
         */
        //[one,two,six,three,four,five]
        list.add(2,"six");
        System.out.println(list);

        /*
            E remove(int index)
            删除并返回指定位置上的元素
         */
        //[one,six,three,four,five]
        String e = list.remove(1);
        System.out.println(list);
        System.out.println("被删除的元素:"+e);
    }
}
```



List subList(int start,int end):获取当前集合中start到end之间的子集。(含头不含尾)

```java
/**
 *  List subList(int start,int end)
 *  获取当前集合中指定范围内的子集。两个参数为开始与结束的下标(含头不含尾)
 */
public class ListDemo3 {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        for(int i=0;i<10;i++){
            list.add(i);
        }
        System.out.println(list);
        //获取3-7这部分
        List<Integer> subList = list.subList(3,8);
        System.out.println(subList);
        //将子集每个元素扩大10倍
        for(int i=0;i<subList.size();i++){
            subList.set(i,subList.get(i) * 10);
        }
        //[30,40,50,60,70]
        System.out.println(subList);
        /*
            对子集元素的操作就是对原集合对应元素的操作
         */
        System.out.println(list);

        //删除list集合中的2-8
        list.subList(2,9).clear();
        System.out.println(list);

    }
}
```





#####  集合与数组的互转操作

集合转换为数组，使用集合的toArray方法即可。

```java
/**
 * 集合转换为数组
 * Collection提供了方法toArray可以将当前集合转换为一个数组
 */
public class CollectionToArrayDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("one");
        list.add("two");
        list.add("three");
        list.add("four");
        list.add("five");
        System.out.println(list);

//        Object[] array = list.toArray();
        /*
            重载的toArray方法要求传入一个数组，内部会将集合所有元素存入该数组
            后将其返回（前提是该数组长度>=集合的size）。如果给定的数组长度不足，
            则方法内部会自行根据给定数组类型创建一个与集合size一致长度的数组并
            将集合元素存入后返回。
         */
        String[] array = list.toArray(new String[list.size()]);
        System.out.println(array.length);
        System.out.println(Arrays.toString(array));
    }
}
```



数组转换为集合，只能转换为List集合，使用的是Arrays.asList()方法。

```java
public class ArrayToListDemo {
    public static void main(String[] args) {
        String[] array = {"one","two","three","four","five"};
        System.out.println(Arrays.toString(array));
        List<String> list = Arrays.asList(array);
        System.out.println(list);

        list.set(1,"six");
        System.out.println(list);
        //数组跟着改变了。注意:对数组转换的集合进行元素操作就是对原数组对应的操作
        System.out.println(Arrays.toString(array));

        /*
            由于数组是定长的，因此对该集合进行增删元素的操作是不支持的，会抛出
            异常:java.lang.UnsupportedOperationException
         */
//        list.add("seven");

        /*
            若希望对集合进行增删操作，则需要自行创建一个集合，然后将该集合元素
            导入。
         */
//        List<String> list2 = new ArrayList<>();
//        list2.addAll(list);
        /*
            所有的集合都支持一个参数为Collection的构造方法，作用是在创建当前
            集合的同时包含给定集合中的所有元素
         */
        List<String> list2 = new ArrayList<>(list);
        System.out.println("list2:"+list2);
        list2.add("seven");
        System.out.println("list2:"+list2);
    }
}
```

####  集合的排序

Collections是集合的工具类,里面定义了很多静态方法用于操作集合.

```java
/**
 * 集合的排序
 * 集合的工具类:java.util.Collections提供了一个静态方法sort,可以对List集合
 * 进行自然排序
 */
public class SortListDemo1 {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        Random random = new Random();
        for(int i=0;i<10;i++){
            list.add(random.nextInt(100));
        }
        System.out.println(list);
        Collections.sort(list);
        System.out.println(list);
    }
}
```

#####  排序自定义类型元素

```java
/**
 * 排序自定义类型元素
 */
public class SortListDemo2 {
    public static void main(String[] args) {
        List<Point> list = new ArrayList<>();
        list.add(new Point(1,2));
        list.add(new Point(97,88));
        list.add(new Point(7,6));
        list.add(new Point(9,9));
        list.add(new Point(5,4));
        list.add(new Point(2,3));
        System.out.println(list);
        /*
            编译不通过的原因:
            Collections.sort(List list)该方法要求集合中的元素类型必须实现接口:
            Comparable,该接口中有一个抽象方法compareTo,这个方法用来定义元素之间比较
            大小的规则.所以只有实现了该接口的元素才能利用这个方法比较出大小进而实现排序
            操作.
         */
        Collections.sort(list);//编译不通过 compare比较  comparable可以比较的
        System.out.println(list);
    }
}
```

实际开发中,我们并不会让我们自己定义的类(如果该类作为集合元素使用)去实现Comparable接口,因为这对我们的程序有**侵入性**.

侵入性:当我们调用某个API功能时,其要求我们为其修改其他额外的代码,这个现象就是侵入性.侵入性越强的API越不利于程序的后期可维护性.应当尽量避免.

#####  重载的Collections.sort(List list,Comparator c)方法

```java
/**
 * 排序自定义类型元素
 */
public class SortListDemo2 {
    public static void main(String[] args) {
        List<Point> list = new ArrayList<>();
        list.add(new Point(1,2));
        list.add(new Point(97,88));
        list.add(new Point(7,6));
        list.add(new Point(9,9));
        list.add(new Point(5,4));
        list.add(new Point(2,3));
        System.out.println(list);
        /*
            Collections.sort(List list)在排序List集合时要求集合元素必须实现了
            Comparable接口。实现了该接口的类必须重写一个方法compareTo用与定义比较
            大小的规则，从而进行元素间的比较后排序。否则编译不通过。

            侵入性:
            当我们调用某个API时，其反过来要求我们为其修改其他额外的代码，这种现象就
            成为侵入性。侵入性不利于程序后期的维护，尽可能避免。
            compare:比较
         */
//        Collections.sort(list);

         //匿名内部类的形式创建一个比较器
        Comparator<Point> com = new Comparator<Point>() {
            @Override
            /**
             * 实现比较器接口后必须重写方法compare.
             * 该方法用来定义参数o1与参数o2的比较大小规则
             * 返回值用来表示o1与o2的大小关系
             */
            public int compare(Point o1, Point o2) {
                int len1 = o1.getX() * o1.getX() + o1.getY() * o1.getY();
                int len2 = o2.getX() * o2.getX() + o2.getY() * o2.getY();
                return len1-len2;
            }
        };
        Collections.sort(list,com);//回调模式
        System.out.println(list);
    }
}
```

#####  最终没有侵入性的写法

```java
/**
 * 排序自定义类型元素
 */
public class SortListDemo2 {
    public static void main(String[] args) {
        List<Point> list = new ArrayList<>();
        list.add(new Point(1,2));
        list.add(new Point(97,88));
        list.add(new Point(7,6));
        list.add(new Point(9,9));
        list.add(new Point(5,4));
        list.add(new Point(2,3));

        System.out.println(list);
        /*
            Collections.sort(List list)在排序List集合时要求集合元素必须实现了
            Comparable接口。实现了该接口的类必须重写一个方法compareTo用与定义比较
            大小的规则，从而进行元素间的比较后排序。否则编译不通过。

            侵入性:
            当我们调用某个API时，其反过来要求我们为其修改其他额外的代码，这种现象就
            称为侵入性。侵入性不利于程序后期的维护，尽可能避免。
            compare:比较
         */
//        Collections.sort(list);

        //匿名内部类的形式创建一个比较器
//        Comparator<Point> com = new Comparator<Point>() {
//            @Override
//            /**
//             * 实现比较器接口后必须重写方法compare.
//             * 该方法用来定义参数o1与参数o2的比较大小规则
//             * 返回值用来表示o1与o2的大小关系
//             */
//            public int compare(Point o1, Point o2) {
//                int len1 = o1.getX() * o1.getX() + o1.getY() * o1.getY();
//                int len2 = o2.getX() * o2.getX() + o2.getY() * o2.getY();
//                return len1-len2;
//            }
//        };
//        Collections.sort(list,com);//回调模式

//        Collections.sort(list,new Comparator<Point>() {
//            public int compare(Point o1, Point o2) {
//                int len1 = o1.getX() * o1.getX() + o1.getY() * o1.getY();
//                int len2 = o2.getX() * o2.getX() + o2.getY() * o2.getY();
//                return len1-len2;
//            }
//        });

        Collections.sort(list,(o1,o2)->
                o1.getX() * o1.getX() + o1.getY() * o1.getY() -
                o2.getX() * o2.getX() - o2.getY() * o2.getY()
        );

        System.out.println(list);
    }
}
```

##### 排序字符串

```java
public class SortListDemo3 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
//        list.add("Tom");
//        list.add("jackson");
//        list.add("rose");
//        list.add("jill");
//        list.add("ada");
//        list.add("hanmeimei");
//        list.add("lilei");
//        list.add("hongtaoliu");
//        list.add("Jerry");

        list.add("传奇");
        list.add("小泽老师");
        list.add("苍老师");
        System.out.println(list);
        
        //按照字符多少排序
//        Collections.sort(list);
//        Collections.sort(list, new Comparator<String>() {
//            public int compare(String o1, String o2) {
////                return o1.length()-o2.length();
//                return o2.length()-o1.length();//反过来减就是降序
//            }
//        });

        Collections.sort(list,(o1,o2)->o2.length()-o1.length());
        System.out.println(list);
    }
}
```

####  ArrayList的优缺点

#####  优点：

- ArrayList 底层以数组实现，是一种随机访问模式。ArrayList 实现了 RandomAccess 接口，因此查
  找的时候非常快。
- ArrayList 在顺序添加一个元素的时候非常方便。

#####  缺点：

- 删除元素的时候，需要做一次元素复制操作。如果要复制的元素很多，那么就会比较耗费性能。
- 插入元素的时候，也需要做一次元素复制操作

#####  Map

- SortedMap
  - TreeMap:基于红黑树实现。
- HashTable:基于哈希表实现。
- LinkedHashMap:使用双向链表来维护元素的顺序，顺序为插入顺序或者最近最少使用（LRU）顺序。
- HashMap:和 HashMap 类似，但它是线程安全的，这意味着同一时刻多个线程同时写入 HashTable 不会导致数据不一致。它是遗留类，不应该去使用它，而是使用 ConcurrentHashMap 来支持线程安全，ConcurrentHashMap 的效率会更高，因为 ConcurrentHashMap 引入了分段锁。



Map体现的结构是一个多行两列的表格,其中左列称为key,右列称为value.

- Map总是成对保存数据,并且总是根据key获取对应的value.因此我们可以将查询的条件作为key查询对应的结果作为value保存到Map中.
- Map有一个要求:key不允许重复(equals比较的结果)

java.util.Map接口,是所有Map的顶级接口,规定了Map的相关功能.

常用实现类:

- java.util.HashMap:称为散列表,使用散列算法实现的Map,当今查询速度最快的数据结构.
- java.util.TreeMap:使用二叉树实现的Map

####  Map常用方法

V put(K k,V v):向Map中添加一组键值对,使用重复的key存入新的value时，那么就是替换value操作。此时put方法
						返回值为被替换的value。否则返回值为null。

V get(K k):根据给定的key获取对应的value。如果给定的key不存在则返回值为null

V remove(K k):根据给定key从Map中删除对应的键值对，返回值为该key对应的value。

int size():返回当前Map中的元素个数

void clear():清空Map

boolean containsKey(Object key):判断当前的Map是否包含给定的key

boolean containsValue(Object value):判断当前Map是否包含给定的value

Set keySet():遍历key使用的方法，将当前Map中所有的key以一个Set集合形式返回

Set entrySet():遍历每一组键值对的方法，将当前Map中每一组键值对(Entry实例)以一个Set集合形式返回

Collection values():遍历所有value使用的方法，将当前Map中所有的value以一个集合形式返回

forEach():基于lambda表达式遍历Map

```java
/**
 * java.util.Map接口  查找表
 * Map体现的结构像是一个多行两列的表格，其中左列称为key，右列称为value
 * Map总是成对儿(key-value键值对)保存数据，并且总是根据key获取其对应的value
 *
 * 常用实现类:
 * java.util.HashMap:称为散列表，使用散列算法实现的Map，当今查询速度最快的
 *                   数据结构。
 */
public class MapDemo {
    public static void main(String[] args) {
        Map<String,Integer> map = new HashMap<>();
        /*
            V put(K k,V v)
            将给定的键值对儿存入Map
            Map有一个要求，即：Key不允许重复(Key的equals比较)
            因此如果使用重复的key存入value，则是替换value操作，此时put方法
            的返回值就是被替换的value。否则返回值为null。
         */
        /*
            注意，如果value的类型是包装类，切记不要用基本类型接收返回值，
            避免因为自动拆箱导致的空指针
         */
        Integer value = map.put("语文",99);
        System.out.println(value);//null
        map.put("数学",98);
        map.put("英语",97);
        map.put("物理",96);
        map.put("化学",98);
        System.out.println(map);

        value = map.put("物理",66);
        System.out.println(value);//96,物理被替换的值
        System.out.println(map);
        /*
            V get(Object key)
            根据给定的key获取对应的value。若给定的key不存在则返回值为null
         */
        value = map.get("语文");
        System.out.println("语文:"+value);

        value = map.get("体育");
        System.out.println("体育:"+value);//null

        int size = map.size();
        System.out.println("size:"+size);
        /*
            V remove(Object key)
            删除给定的key所对应的键值对，返回值为这个key对应的value
         */
        value = map.remove("语文");
        System.out.println(map);
        System.out.println(value);

        /*
            boolean containsKey(Object key)
            判断当前Map是否包含给定的key
            boolean containsValue(Object value)
            判断当前Map是否包含给定的value
         */
        boolean ck = map.containsKey("英语");
        System.out.println("包含key:"+ck);
        boolean cv = map.containsValue(97);
        System.out.println("包含value:"+cv);
    }
}
```

#### Map的遍历

- 遍历所有的key
- 遍历所有的键值对
- 遍历所有的value(相对不常用)

```java
/**
 * Map的遍历
 * Map提供了三种遍历方式
 * 1:遍历所有的key
 * 2:遍历每一组键值对
 * 3:遍历所有的value(不常用)
 */
public class MapDemo2 {
    public static void main(String[] args) {
        Map<String,Integer> map = new HashMap<>();
        map.put("语文",99);
        map.put("数学",98);
        map.put("英语",97);
        map.put("物理",96);
        map.put("化学",98);
        System.out.println(map);
        /*
            遍历所有的key
            Set keySet()
            将当前Map中所有的key以一个Set集合形式返回。遍历该集合就等同于
            遍历了所有的key
         */
        Set<String> keySet = map.keySet();
        for(String key : keySet){
            System.out.println("key:"+key);
        }

        /*
            遍历每一组键值对
            Set<Entry> entrySet()
            将当前Map中每一组键值对以一个Entry实例形式存入Set集合后返回。
            java.util.Map.Entry
            Entry的每一个实例用于表示Map中的一组键值对，其中有两个常用方法:
            getKey()和getValue()
         */
        Set<Map.Entry<String,Integer>> entrySet = map.entrySet();
        for(Map.Entry<String,Integer> e : entrySet){
            String key = e.getKey();
            Integer value = e.getValue();
            System.out.println(key+":"+value);
        }
        /*
            JDK8之后集合框架支持了使用lambda表达式遍历。因此Map和Collection都
            提供了foreach方法，通过lambda表达式遍历元素。
         */
        map.forEach(
             (k,v)-> System.out.println(k+":"+v)
        );


        /*
            遍历所有的value
            Collection values()
            将当前Map中所有的value以一个集合形式返回
         */
        Collection<Integer> values = map.values();
//        for(Integer i : values){
//            System.out.println("value:"+i);
//        }
        /*
            集合在使用foreach遍历时并不要求过程中不能通过集合的方法增删元素。
            而之前的迭代器则有此要求，否则可能在遍历过程中抛出异常。
         */
        values.forEach(
                i -> System.out.println("value:"+i)
        );
    }
}
```

####  反射

在运行状态中，对于任意一个类都能够知道这个类所有的属性和方法；
并且对于任意一个对象，都能够调用它的任意一个方法；这种动态获取信息以及动态调用对象方
法的功能成为 Java 语言的反射机制

##### 反射API

1.Class 类：反射的核心类，可以获取类的属性，方法等信息。

2.
Field 类：Java.lang.reflec 包中的类，表示类的成员变量，可以用来获取和设置类之中的属性
值。

3.
Method 类： Java.lang.reflec 包中的类，表示类的方法，它可以用来获取类中的方法信息或
者执行方法。

4.
Constructor 类： Java.lang.reflec 包中的类，表示类的构造方法。

#####  获取Class对象的三种方式

###### 调用某个对象的 getClass()方法

```java
Person p=new Person();
Class cls=p.getClass();
```

######  调用某个类的 class 属性来获取该类对应的 Class 对象

```java
Class cls=Person.class;
```

######  使用 Class 类中的 forName()静态方法(最安全/性能最好)

```java
Class cls=Class.forName("类的全路径"); (最常用)
```

```java
//获取 Person 类的 Class 对象
Class clazz=Class.forName("reflection.Person");
//获取 Person 类的所有方法信息
Method[] method=clazz.getDeclaredMethods();
for(Method m:method){
System.out.println(m.toString());
}
//获取 Person 类的所有成员属性信息
Field[] field=clazz.getDeclaredFields();
for(Field f:field){
System.out.println(f.toString());
}
//获取 Person 类的所有构造方法信息
Constructor[] constructor=clazz.getDeclaredConstructors();
for(Constructor c:constructor){
System.out.println(c.toString());
}
```

#####  创建对象的两种方法

Class对象的newlnstance()

- 使用 Class 对象的 newInstance()方法来创建该 Class 对象对应类的实例，但是这种方法要求
  该 Class 对象对应的类有默认的空构造器

调用Constructor对象的newInstance()

- 先使用 Class 对象获取指定的 Constructor 对象，再调用 Constructor 对象的 newInstance()
  方法来创建 Class 对象对应类的实例,通过这种方法可以选定构造方法创建实例

```java
//获取 Person 类的 Class 对象
Class cls=Class.forName("reflection.Person");
//使用.newInstane 方法创建对象
Person p=(Person) cls.newInstance();
//获取构造方法并创建对象
Constructor c=cls.getDeclaredConstructor(String.class,String.class,int.class);
//创建对象并设置属性
Person p1=(Person) c.newInstance("李四","男",20);
```

####  注解

#####  4种元注解

@Retention：表示要在什么级别保存该注释信息

- RetentionPoicy参数
  - RetentionPolicy.CLASS    :   当前注解保留在编译后的字节码文件中，但是不可被反射机制操作。
  - RetentionPolicy.SOURCE   :   当前注解仅保留在源代码中。
  - RetentionPolicy.RUNTIME  :   当前注解保留在编译后的字节码文件中，可被反射机制操作。

@Target：该注解可以用在什么地方

- ElementType参数
  - ElementType.TYPE:在类上可以使用当前注解
  - ElementType.FIELD:在属性上可以使用当前注解
  - ElementType.CONSTRUCTOR:在构造方法上可以使用当前注解
  - ElementType.METHOD:在方法上可以使用当前注解
  - ElementType.PACKAGE:在包上可以使用当前注解

@Documented：将注解包含在javaDoc种

@Inhertied：允许子类继承父类种的注解
