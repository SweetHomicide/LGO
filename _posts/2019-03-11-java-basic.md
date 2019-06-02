### java基础


## Session & cookie


##  网络

>1.TCP/IP

## 1.内存模型

> 1.堆内存Heap与栈内存Stack的区别   
	
	堆内存：主要用于存储实例化的对象、数组、有JVM动态分配内存空间，一个JVM中只有一个堆内存，线程是可以共享数据的。
	栈内存：主要用于存储局部变量和对象的引用变量，每个线程都会有一个独立的栈空间，所以线程之间是不共享数据的。
	


## 2.数据类型
>1.数据类型的概念是什么?

	数据类型是对计算机内存位置的一个抽象表达方式,是对固定大小内存起了一个别名
	
>2.java中有几种数据类型?  

	两种:基本类型和引用类型
>3.基本数据类型和引用数据类型的区别是什么?
	
	主要区别在于存储方式上
	一:基本类型被创建时是在栈内存Stack上为其划分一块内存,将数值直接存在栈内存中。
	二:引用内存在被创建时首先在栈内存中为其引用分配一块内存,而对象的具体信息都存在堆内存中,然后由栈上面的引用指向堆内存中的对象地址

	例如:
		User user = new User("张三");//name
	1.首先在栈内存中为其user分配一块空间
	2.然后在堆内存中为User这个对象分配一块空间,其属性name初始值为空
	3.调用构造方法给堆内存中的User对象属性name赋值"张三"
	4.将堆内存中的User对象的地址赋值给栈内存中的user引用
	最后可以通过user这个引用找到堆内存中User()对象的具体信息

>4.基本数据类型有几种?

	八种基本类型
	byte：Java中最小的数据类型，在内存中占8位(bit)，即1个字节，取值范围-128~127，默认值0
	short：短整型，在内存中占16位，即2个字节，取值范围-32768~32717，默认值0
	int：整型，用于存储整数，在内在中占32位，即4个字节，取值范围-2147483648~2147483647，默认值0
	long：长整型，在内存中占64位，即8个字节-2^63~2^63-1，默认值0L
	float：浮点型，在内存中占32位，即4个字节，用于存储带小数点的数字（与double的区别在于float类型有效小数点只有6~7位），默认值0
	double：双精度浮点型，用于存储带有小数点的数字，在内存中占64位，即8个字节，默认值0
	char：字符型，用于存储单个字符，占16位，即2个字节，取值范围0~65535，默认值为空
	boolean：布尔类型，占1个字节，用于判断真或假（仅有两个值，即true、false），默认值false
>5.引用数据类型有是什么?

	引用类型包括类、接口、枚举和数组类型、null类型。
 	注意:
	（1）null类型只能被转换成引用类型,不能转换成基本类型，所以不能给基本类型赋值为null
		int i = null;//编译不通过
		Error:(14, 17) java: 不兼容的类型: <nulltype>无法转换为int
	（2）字符串类型是一个类，即引用类型
>6.值传递和引用传递的区别？

	区别在于值传递不会影响原始数据的值，引用传递可能会影响原始数据的值
	值传递传的是数据的拷贝,所以方法中对值传递的数据操作不会影响原始数据
	引用传递给方法的是对象的地址,与原始数据指向的是同一块地址,所以操作会改变原始数据

>7.什么是装箱和拆箱?
	
	装箱就是  自动将基本数据类型转换为包装器类型；
	拆箱就是  自动将包装器类型转换为基本数据类型。
	Integer i = 10;  //装箱
	int n = i;   	 //拆箱	 
>8.Integer和int的区别?

	1.int是基本类型的原始类型 Integer是int的包装器类型
	2.int默认值是0;Integer默认值是null
	3.int没有toString()方法;Integer具有 

>9.switch语句能否作用在byte上，能否作用在long上，能否作用在string上？

	byte的存储范围小于int，可以向int类型进行隐式转换，所以switch可以作用在byte上
	long的存储范围大于int，不能向int进行隐式转换，只能强制转换，所以switch不可以作用在long上
	string在1.7版本之前不可以，1.7版本之后switch就可以作用在string上了。
>10.java 中 3*0.1 == 0.3 将会返回什么？true 还是 false？

	false，因为浮点数不能完全精确的表示出来，一般都会损失精度。
>11.java 中 float f = 3.4; 是否正确？

	不正确，3.4 是双精度数，将双精度型（double）赋值给浮点型（float）属于向下转型（down-casting，也称为窄化）会造成精度损失，因此需要强制类型转换 float f = (float)3.4; 或者写成 float f = 3.4F; 才可以。
	
>12.char类型变量能不能储存一个中文的汉字，为什么？

	char ch = '能';
	因为char类型变量是用来存储Unicode编码的字符，而Unicode编码字符集中包含了大量的常用汉字,所以可以存储中文汉字;
	另外又因为Unicode编码占用两个字节，一个中文汉字也是两个字节长度所以可以存储一个中文汉字
	
>13.short s1 = 1; s1 = s1 + 1;有什么错? short s1 = 1; s1 +=1;有什么错?
	
	java规范：
		a.高位转低位需要强制转换
		b.低位转高位自动转.
	1.前者编译错误,因为short在运算时自动提升表达式的类型为int;所以运算后赋值给s1的时候需要强制转换。
	2.+=是java语言规定的运算符，java编译器会对它进行特殊处理，因此可以正确编译

>14.能不能继承String类

	不能，因为String是个final类所以String类是不可以被继承的。同样，String对象的值是不可以被改变的；
>15.为什么说Strng对象的值不能被改变?
	
	String s = "张三"; s = "李四";
	System.out.println(s); //输出的结果是"李四"
	因为是final修饰的类，所以不能改变；
	这种情况只是改变了s引用指向堆内存中的地址;s="李四"是在堆内存中重新创建了一个String对象并将地址赋值给了s，  
	s="张三"这个对象依然在堆内存中存在，但是不能再访问张三这个String对象,因为s引用已经指向了堆内存中"李四"这个String对象了，  
	所以在编程的时候若有要经常修改的内容情况,建议使用StringBuilder、StringBuffer	
	
>15.String 、 StringBuffer 、StringBuilder三者的区别？你在编程中如何使用	

	他们都是可以操作字符串的数据类型,区别在于
	1.String和StringBuilder非线程安全，StringBuffer是线程安全
	2.String追加字符串都会创建新的对象，消耗的时间长，性能差，不适合动态构建字符串
	3.StringBuffer因为实现了线程安全，所以性能差，适合多线程环境使用
	4.StringBuilder相比StringBuffer性能高，适合单线程环境使用
 



## 2.集合
>1.Java中集合框架的有几个？

	有两个分别是Collection框架 和 Map框架,它们有各自的实现框架
	1.Collection框架包含了List、Queue、Set
	2.Map框架包含了AbstractMap和Hashtable

>2.List 、 Set 、Queue的区别？

	1.List是有序集合,集合内元素可以重复，元素可为null
	2.Set是无序集合,集合内元素不能重复，会自动去重，元素可为null
	3.Queue是模拟队列这种数据结构，遵循先进先出(FIFO);队列的头部保存着队列中存放时间最长的元素，队列的尾部保存着队列中存放时间最短的元素 
		常用的方法有:
		1. queue.offer("新元素")//插入元素到队列的尾部
		2. queue.poll() //返回第一个元素，并在队列中删除
		3. queue.element()//返回第一个元素 不从队列中删除

	
>3.ArrayList 、 LinkedList 、Vector的区别
	
	1.ArrayList 和 LinkedList 非线程安全
	2.ArrayList基于动态数组实现,LinkedList基于双向链表实现;
	3.ArrayList随机访问get、set方法时效率比LinkedList高;
	4.LinkedList对数据进行增加和删除的操作时(add和remove操作)效率比ArrayList高
	5.Vector 和 ArrayList都是基于动态数组实现，Vector是线程安全

>4.什么是双向链表？
	
	双向链表中数据节点的结构分为3部分：prev 、data 、next，节点与节点之间通过prev和next指针相连

>5.HashSet 、 TreeSet 、LinkedHashSet的区别?

	1.HashSet非线程安全,元素允许有null，但只能放一个null,迭代时不能保证元素迭代顺序是按照插入时的顺序。
	2.TreeSet是SortedSet接口的唯一实现类、元素中不能有null，且同一个treeSet对象中存的数据类型必须相同；默认自然排序支持定制排序;
	3.LinkedHashSet是HashSet的子类,非线程安全,迭代时可以保证元素迭代顺序是按照插入时的顺序。迭代访问数据时比HashSet性能好,插入数据性能差

>6.HashMap、TreeMap和HashTable的区别
	
	1.父类不同：Hashtable的父类是Dictionary，HashMap的父类是AbstractMap
	2.HashMap基于数组方式存储,非线程安全,key和value均可为null,最多只能有一个key为null,迭代时不能保证元素迭代顺序是按照插入时的顺序。
	3.TreeMap  非线程安全,key不能为null,迭代时可以保证元素迭代顺序是按照插入时的顺序。
	4.Hashtable是线程安全,key和value均不能为null,因为Hashtable是线程安全的所以效率会比HashMap低

>7.List、Set、Map的区别
	
	1.List是有序集合,允许多个元素为null,可以存储重复对象
	2.Set是无序集合,但是子类SortedSet的实现类TreeSet是有序的且支持定制排序；
		HashSet元素允许有null，但只能放一个null
		TreeSet中元素不允许存在null值.
	3.Map是以key、Value存储元素
		HashMap可以存储null最多只能有一个key为null
		TreeMap的key不能为null，
		Hashtable的key、value均不能为null

>8
	
	
	
## 多线程	
	
>1.线程和进程的区别是什么？

	它们的共同点都是系统中程序运行的基本单元，进程是操作系统资源分配的基本单元,通常指的是一个程序运
	行状态的实例,程序运行时系统就会创建一个进程，并为它分配资源，然后把该进程放入进程就绪队列，进程
	调度器选中它的时候就会为它分配CPU时间，程序开始真正运行。
	而线程是进程运行时的最小单元,一个进程可以由很多个线程组成，线程间共享进程的所有资源，每个线程有
	自己的堆栈和局部变量。
>2.线程同步的方法有那些?

	1.使用synchronized关键字
	2.使用wait和notify等待唤醒线程
	3.使用volatile实现线程同步
	4.使用ReentrantLock重入锁实现线程同步
	5.使用ThreadLocal局部变量来实现线程同步

>3.start()方法和run()方法简介和区别？

	start是启动线程的方法，当线程调用了start方法则会使线程处于就绪状态(Runnable),一旦得到cpu资源分配就
	自动开始执行run方法里面的代码实现;主要作用就是启动线程达到就绪状态。
	run方法是实现线程需要重写的方法,用来执行线程任务;如果直接调用线程的run方法,相当于调用了一个普通方法体。

>4.volatile关键字的作用是什么？  


	volatile保证了内存的可见性,就是保证了多线程环境中线程间操作的变量是最新变量;如线程1中对变量v的
	最新修改，对线程2是可见的。  

>5.ThreadLocal关键字的作用是什么？

	ThreadLocal修饰的全局变量,可以为每个线程保存一个变量副本,这个副本变量不会受到其他线程的干扰,只作用于当前持有的线程内。

	它的实现原理是内部有个ThreadLocalMap类型的成员变量threadLocals用来存储实际变量的副本,Key为当前的 
	ThreadLocal变量,Value是要存储的变量副本(即T类型的变量);初始时，在Thread里面，threadLocals为空，当
	通过ThreadLocal变量调用get()方法或者set()方法，就会对Thread类中的threadLocals进行初始化，并且以当
	前ThreadLocal变量为键值，以ThreadLocal要保存的副本变量为value，存到threadLocals。然后在当前线程里
	面，如果要使用副本变量，就可以通过get方法在threadLocals里面查找。
	
	实现方法：
    get()方法用于获取当前线程的副本变量值。
    set()方法用于保存当前线程的副本变量值。
    initialValue()为当前线程初始副本变量值。
    remove()方法移除当前前程的副本变量值。

>6.ReentrantLock 和 synchronized的区别?
	
 	1.Synchronized是依赖于JVM实现的，而ReenTrantLock是JDK实现的
	2.Synchronized的使用比较方便,由编译器去保证加锁和释放；
	3.而ReenTrantLock需要手工声明来加锁和释放锁,为了避免忘记手工释放锁造成死锁,所以最好在finally中声明释放锁。
	4.ReenTrantLock提供了一个Condition（条件）类,用来实现分组唤醒需要唤醒的线程们,synchronized要么随机唤醒一个线程要么唤醒全部线程。
	5.Synchronized线程等待不可中断,除非抛出异常(释放锁方式：1.代码执行完，正常释放锁；2.抛出异常，由JVM退出等待)
	6.ReentrantLock持有锁的线程长期不释放的时候，正在等待的线程可以选择放弃等待
	方法：
     	1.设置超时方法 tryLock(long timeout, TimeUnit unit)，时间过了就放弃等待；
      	2.lockInterruptibly()放代码块中，调用interrupt()方法可中断，而synchronized不行)
 

>7.阻塞线程的方法有几种?

	sleep:可以指定线程等待的时间,当时间到了线程自动恢复运行状态,不会释放锁;
	wait:需要通过notify或者notifyAll方法唤醒线程,会释放锁
	yield:它能让当前线程由“运行状态”进入到“就绪状态”;
	join:可以使得一个线程在另一个线程结束后再执行;使线程运行排序

>8.怎么保证多线程顺序执行而不是通过cpu随机调度?
 
	1.使用join方法可以阻塞线程,join的作用是一个线程在另一个线程结束之后再执行.从而可以达到线程顺序执行。
	2.通过共享对象锁加上可见变量(volatile )来实现。
	3.创建一个单线程的线程池ExecutorService executor = Executors.newSingleThreadExecutor();

>9.




## io流

>1.Java的io流分为哪两种？

	按功能来分：输入流(input)，输出流(output)
	按类型来分：字符流与字节流

>2.字节流与字符流的区别？

	字节流以字节为单位输入输出数据，字节流按照8位传输
		输入使用Reader类来操作
		输出使用Writer类来操作
	
	字符流以字符为单位输入输出数据，字符流按照16位传输
		输入使用InputStream类来操作
		输出使用OutputStream类来操作

	处理对象不同：字节流能处理所有类型的数据（如图片、avi等），而字符流只能处理字符类型的数据。

>3.常用io类有那些？

    File
    FileInputSteam，FileOutputStream
    BufferInputStream，BufferedOutputSream
    PrintWrite
    FileReader，FileWriter
    BufferReader，BufferedWriter
    ObjectInputStream，ObjectOutputSream





## 自定义注解

>1.自定义注解怎么实现?

	java中有四种元注解：@Retention、@Inherited、@Documented、@Target

	@Retention ：用来说明该注解类的生命周期。它有以下三个参数：
		RetentionPolicy.SOURCE   : 注解只保留在源文件中
		RetentionPolicy.CLASS    : 注解保留在class文件中，在加载到JVM虚拟机时丢弃
		RetentionPolicy.RUNTIME  : 注解保留在程序运行期间，此时可以通过反射获得定义在某个类上的所有注解。

	@Target :  用来说明该注解可以被声明在那些元素之前。
		ElementType.TYPE：说明该注解只能被声明在一个类前。
		ElementType.FIELD：说明该注解只能被声明在一个类的字段前。
		ElementType.METHOD：说明该注解只能被声明在一个类的方法前。
		ElementType.PARAMETER：说明该注解只能被声明在一个方法参数前。
		ElementType.CONSTRUCTOR：说明该注解只能声明在一个类的构造方法前。
		ElementType.LOCAL_VARIABLE：说明该注解只能声明在一个局部变量前。
		ElementType.ANNOTATION_TYPE：说明该注解只能声明在一个注解类型前。
		ElementType.PACKAGE：说明该注解只能声明在一个包名前。
	过程：通过@interface创建一个自定义注解类,通过是@Retention注解标注该类的生命周期,通过@Target标注可以被声明在那些元素之前。

>2.自定义注解使用场景 ? 项目中怎么使用
	
	登陆、权限拦截、日志处理
	自定义注解是通过运行时靠反射机制获取注解，实际开发中我们要获取某个方法的调用日志，可以通过 AOP（动态代理机制）给方法添加切面，通过反射来获取方法包含的注解，如果包含日志注解，就进行日志记录。
 

## 动态代理

>1.什么是代理?

	代理就是给某一个对象提供一个代理对象，由代理对象控制对原对象的引用。	
	
>2.什么是动态代理？

	动态代理就是实现阶段不用关心代理谁,而是在运行阶段才指定代理那个对象,如果是自己写代理类的方法
	就是静态代理(确定性),确定了需要代理的对象.
	
	组成要素:
	
	(动态)代理模式主要涉及三个要素:
	
	#1:抽象类接口
	
	#2:被代理类(具体实现抽象接口的类)
	
	#3:动态代理类:实际调用被代理类的方法和属性的类

>3.代理有那些实现方法?

	CGLIB和JDK动态代理
	JDK提供了动态代理接口InvocationHandler来实现动态代理类.

>4.动态代理的原理?

	JDK动态代理:基于java反射机制实现,必须要实现了接口InvocationHandler才能用这种办法生成代理对象. 
	
	cglib动态代理:基于ASM机制实现,通过生成业务类的子类作为代理类.

>5.静态代理和动态代理的区别?

	静态代理:事先写好代码类,可以手工编写,也可以用工具生成.缺点是每个业务类都要有一个对应代理类,非常不灵活.
	动态代理:运行时自动生成代理对象.缺点是生成代理对象和调用代理对象都要额外花费时间,

# 数据库
## mysql

> 数据库三大范式是什么?

	1.确保表中的每一列都是原子性不可再分割
	2.有主键，其他非主键字段依赖主键。确保一个表只说明一个事物
	3.非主键字段不能相互依赖。 每列都与主键有直接关系，不存在传递的依赖

	第一范式：不符合第一范式的例子：

        表：字段1、 字段2(字段2.1、字段2.2)、字段3 ......
	第二范式：不符合第二范式的例子:

        表：学号、课程号、姓名、学分;

        这个表明显说明了两个事务:学生信息, 课程信息;由于非主键字段必须依赖主键，这里学分依赖课程号，姓名依赖与学号，所以不符合二范式。

	第三范式：不符合第三范式的例子:

         表：学号、姓名、 年龄、 所在学院、学院联系电话、学院联系电话

          存在依赖传递: (学号) → (所在学院) → (学院地点, 学院电话)
 

>1. JDBC操作的步骤

    加载数据库驱动类
    打开数据库连接
    执行sql语句
    处理返回结果
    关闭资源
>2. 在使用jdbc的时候，如何防止出现sql注入的问题。

	使用PreparedStatement类，而不是使用Statement类

>3.怎么在JDBC内调用一个存储过程

	使用CallableStatement

 
>4.是否了解连接池，使用连接池有什么好处？

	数据库连接是非常消耗资源的，影响到程序的性能指标。连接池是用来分配、管理、释放数据库连接的，可以使应用程序重复使用同一个数据库连接，而不是每次都创建一个新的数据库连接。通过释放空闲时间较长的数据库连接避免数据库因为创建太多的连接而造成的连接遗漏问题，提高了程序性能。
>5.你所了解的数据源技术有那些？使用数据源有什么好处？

	Dbcp,c3p0等; druid 阿里产品
	好处:通过配置文件的形式来维护数据库信息，而不是通过硬编码。当连接的数据库信息发生改变时，不需要再更改程序代码就实现了数据库信息的更新。
>6.drop,delete与truncate的区别

	drop直接删掉表 truncate删除表中数据，再插入时自增长id又从1开始 delete删除表中数据，可以加where字句

>7.索引的工作原理及其种类？

	1.普通索引 index 
	2.唯一索引 unique 
	3.主键索引 primary key
	4.组合索引 index 
	5.全文索引 fulltext
	索引使用b+ 树的数据结构

>8.数据库优化的思路?

	1.选择合适的存储引擎
	2.SQL语句优化
	3.索引优化
	4.数据库结构优化
		1）范式优化： 比如消除冗余（节省空间。。） 
		2）反范式优化：比如适当加冗余等（减少join） 
		3）拆分表
	5.服务器硬件优化

>9.连接查询的种类?
	
	左连接 left join： 返回包括左表中的所有记录和右表中连接字段相等的记录
	右连接 right join：返回包括右表中所有记录和左表中连接字段相等的记录
	内连接 inner join :返回与连接条件相匹配的数据行
	交叉连接 cross join:

>10.MySQL中myisam与innodb的区别，至少5点
	
	1.InnoDB支持事物，而MyISAM不支持事物
	2.InnoDB支持行级锁，而MyISAM支持表级锁
	3.InnoDB支持MVCC, 而MyISAM不支持
	4.InnoDB支持外键，而MyISAM不支持
	5.InnoDB老版本不支持全文索引，而MyISAM支持。
	6.InnoDB不能通过直接拷贝表文件的方法拷贝表到另外一台机器， myisam 支持
	7.InnoDB表支持多种行格式， myisam 不支持
	8.InnoDB是索引组织表， myisam 是堆表

>11.MySQL中varchar与char的区别以及varchar(50)中的50代表的涵义?

	char    最多能存放的字符个数 255 
	varchar 最多能存放 65532 个字符

	(2)、varchar(50)中50的涵义
		最多存放50个字符，varchar(50)和(200)存储hello所占空间一样，但后者在排序时会消耗更多内存，因为
		order by col采用fixed_length计算col长度(memory引擎也一样)。在早期 MySQL 版本中， 50 代表字节
		数，现在代表字符数。
	
>12.存储过程与触发器的区别

	触发器与存储过程非常相似，触发器也是SQL语句集，两者唯一的区别是触发器不能用EXECUTE语句调用，而是
	在用户执行Transact-SQL语句时自动触发（激活）执行

>13.MySQL中InnoDB引擎的行锁是通过加在什么上完成(或称实现)的？

	InnoDB是基于索引来完成行锁
	
	例: select * from tab_with_index where id = 1 for update;
	
	for update 可以根据条件来完成行锁锁定,并且 id 是有索引键的列,
	
	如果 id 不是索引键那么InnoDB将完成表锁,并发将无从谈起。

>14.having和where的区别?
 
	1.where无法使用统计函数，having能够使用统计函数
	1.having筛选必须对查询的结果集进行筛选 
	2.having子句中可以使用字段别名，而where不能使用
 

>15.distinct和group by的区别？

 	两者都可以实现去重的作用,group by  

	

>16.面试查询题


	https://segmentfault.com/a/1190000015570878?utm_source=tag-newest

## redis
>1.redis有多少种数据类型?

	五种数据类型:String,List,Hash,Set,sorted set:
>2.程序中怎么使用redis的?

	会话缓存
>3.Redis主要消耗什么物理资源？

	内存。
>4.Redis相比memcached有哪些优势？

	(1) memcached所有的值均是简单的字符串，redis作为其替代者，支持更为丰富的数据类型
	(2) redis的速度比memcached快很多
	(3) redis可以持久化其数据
>5.Redis有哪几种数据淘汰策略？

	noeviction:返回错误当内存限制达到并且客户端尝试执行会让更多内存被使用的命令（大部分的写入指令，但DEL和几个例外）
	allkeys-lru: 尝试回收最少使用的键（LRU），使得新添加的数据有空间存放。
	volatile-lru: 尝试回收最少使用的键（LRU），但仅限于在过期集合的键,使得新添加的数据有空间存放。
	allkeys-random: 回收随机的键使得新添加的数据有空间存放。
	volatile-random: 回收随机的键使得新添加的数据有空间存放，但仅限于在过期集合的键。
	volatile-ttl: 回收在过期集合的键，并且优先回收存活时间（TTL）较短的键,使得新添加的数据有空间存放。
>6.一个字符串类型的值能存储最大容量是多少？
	
	512M

>7.Redis集群都有哪些方案？

	方案一：
		主从复制方案：
			主从复制不会阻塞master,在同步数据时，master可以继续处理client请求.	
			a)主从复制，若主节点出现问题，则不能提供服务，需要人工修改配置将从变主
			b)主从复制主节点的写能力单机，能力有限
			c)单机节点的存储能力也有限
		提供哨兵模式:(高可用)
			当用Redis做Master-slave的高可用方案时，如果master宕机，Redis自身并不能实现
			自动进行主备切换，sentinel可以监控复制节点的状态，当主节点宕机后，它能根据选
			举方式选出后端的一个从节点作为新的master，sentinel还能监控多个master-slave
			集群，发现master宕机后能进行自动切换。同时，sentinel本身也存在单点问题，通常
			sentinel也是一个集群，因此，redis的复制集群通常是下面的结构
	方案二：
		cluster:
			是一种服务器分片技术，3.0版本开始正式提供。分片采用slot(槽)的概念。
	方案三：
		codis:
			Codis是一个豌豆荚团队开源的使用Go语言编写的Redis Proxy使用方法和普通的redis没
		有任何区别，设置好下属的多个redis实例后就可以了，使用时在本需要连接redis的地方改为连
		接codis，它会以一个代理的身份接收请求 并使用一致性hash算法，将请求转接到具体redis	
	方案四：
		twemproxy:
			twitter开源的方案


>8.Redis集群方案应该怎么做？

	场景一：单机(高并发)
		如果你的数据量很少,主要是承载高并发高性能的场景，比如你的缓存一般就几个G,单机足够了

	场景二：主从复制(高并发+高可用)
	  	如果要实现高可用可以使用主从复制一个mater，多个slave，要几个slave跟你的要求的读吞吐量有关
		系，然后自己搭建一个sentinal集群，去保证redis主从架构的高可用性，就可以了

	场景三：cluster(海量数据+高并发+高可用)
 		cluster主要是针对海量数据+高并发+高可用的场景，海量数据，如果你的数据量很大，那么建议就用redis cluster
	
>9.Redis如何设置密码及验证密码？

	设置密码：config set requirepass 123456

	验证密码：auth 123456

>10.Redis集群之间是如何复制的？

	异步复制

>11.Redis集群最大节点个数是多少？

	16384个。
>12.Redis集群如何选择数据库？

	Redis集群目前无法做数据库选择，默认在0数据库。
>13.Redis中的管道有什么用？

	可以一次性发送多条命令并在执行完后一次性将结果返回，pipeline通过减少客户端与redis的通信次数
	来实现降低往返延时时间，而且Pipeline 实现的原理是队列

>14.怎么理解Redis事务？

	Redis事务允许在一次单独的步骤中执行一组命令，并且可以保证如下两个重要事项：
		事务中的所有命令都会序列化、按顺序地执行。
		事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。

>15.Redis事务相关的命令有哪几个？

	multi	：开始一个事务， 然后将多个命令入队到事务中
	exec 	：触发事务， 一并执行事务中的所有命令
	discard : 取消事务，放弃执行事务块内的所有命令
	watch	: 监视一个(或多个) key ，如果在事务执行之前这个(或这些) key 被其他命令所改动，那么事务将被打断。
	unwatch : 取消监视

>16.Redis事务的用法

	使用MULTI命令便可以进入一个Redis事务。这个命令的返回值总是OK。此时，用户可以发出多个Redis命令。Redis
	会将这些命令放入队列，而不是执行这些命令。一旦调用EXEC命令，那么Redis就会执行事务中的所有命令。
	相反，调用DISCARD命令将会清除事务队列，然后退出事务。

>17.Redis如何做内存优化？

	尽量使用Hash来存储；比如需要存储用户信息:
		1)如果根据用户id存储,把其他信息封装成一个对象以序列化的方式存储因为序列化需要io操作,所以开销比较大
		2)通过用户id+属性名作为Key,其值作为value虽然省去了序列化操作,但是如果用户信息较多则会耗费大量的内存
		3)hash是一个string类型的map映射表,使用用户id做为key,属性和值存储到map映射中,属性名作为key,值为value
		即可以减少序列化开销又能节省内存资源

>18.Redis如何持久化?

	RDB持久化是指在指定的时间间隔内将内存中的数据集快照写入磁盘 

		RDB又存在哪些劣势呢？

		1). 如果你想保证数据的高可用性，即最大限度的避免数据丢失，那么RDB将不是一个很好的选择。因为系统
			一旦在定时持久化之前出现宕机现象，此前没有来得及写入磁盘的数据都将丢失。
		
		2). 由于RDB是通过fork子进程来协助完成数据持久化工作的，因此，如果当数据集较大时，可能会导致整个
			服务器停止服务几百毫秒，甚至是1秒钟。

	 AOF：以独立日志的方式记录每次写命令，重启时在重新执行AOF文件中的命令达到恢复数据的目的。
	 主要作用：解决了数据持久化的实时性。

		appendfsync always      #每次有数据修改发生时都会写入AOF文件。

		appendfsync everysec    #每秒钟同步一次，该策略为AOF的缺省策略。
		
		appendfsync no          #从不同步。高效但是数据不会被持久化。

	

## mongodb

## elasticsearch


# 框架
## Spring
 

## SpringMvc



## SpringBoot



## mybatis

 

## hibernate



## SpringDataJpa



## shiro



# 服务器
## Tomcat

## Nginx
	

## Linux
>1.查看内存/cpu使用情况的命令?

	使用top命令
>2.修改目录和文件的访问权限命令?

	chmod用法：
	用来修改某个目录或文件的访问权限。
	
	语法：chmod [-cfvR] [--help] [--version] [who] [+ | - | =] [mode] 文件名
	
	例子：chmod -R 777 /home/linux

3.更改某个目录或文件的用户名和用户组的命令?

	chown用法：
	
	用来更改某个目录或文件的用户名和用户组。
	
	chown 用户名:组名 文件路径（可以是绝对路径也可以是相对路径）
	
	例1：chown root:root /tmp/tmp1
	
	就是把tmp下的tmp1的用户名和用户组改成root和root（只修改了tmp1的属组）。
	
	例2：chown -R root:root /tmp/tmp1
	
	就是把tmp下的tmp1下的所有文件的属组都改成root和root。
	


# 分布式

## SpringCloud

## dubbo

## 单点登录
	
>1.什么是单点登录

	单点登录就是一处登录多处使用;多用于分布式系统中。
	它的实现过程：

## 分布式缓存
>1.redis主从复制如何实现的？其作用是什么?
	
	选择一台主服务器Master用来写数据,其余的从节点slave用来读数据,slave节点通过配置redis.conf文
	件中的slaveof主节点master的ip地址;主节点密码masterauth 等属性实现主从复制。

	主从模式通常需要配置哨兵机制,从而实现redis集群的高可用性.
	
	主从复制的作用：数据备份、读写分离、分布式集群、实现高可用、宕机容错机制等。

>2.Redis 实现主从复制的原理是什么？

    slave 启动成功之后连接到 master 后会发送一个 sync 命令。

    master 接收到这个同步命令之后启动后台的存盘进程，即将内存的数据持久化到 rdb 或 aof。

    持久化完毕之后，master 将整个数据文件传送给 slave。

	slave会将接收到的 master 发来的整个数据库文件存盘并加载到内存。


>3.redis哨兵模式如何配置?

	通过配置sentinel.conf文件
	1.sentinel monitor来监控节点 
	2.sentinel auth-pass 验证监控节点的密码 
	3.通过配置sentinel down-after-milliseconds参数修改心跳检测【默认为30秒】
	4.通过./redis-server sentinel.conf --sentinel &

>4.redis的key是如何寻址的？

	hash 算法
	一致性 hash 算法
	redis cluster 的 hash slot 算法	

>5.
	

## 分布式事物

 

## 分布式锁

## rabbitmq

>1.	如何保证消息的可靠性传输（如何处理消息丢失的问题）？

	1.生产者丢失消息(事物+confirm模式)
		方案一：
		rabbitmq提供的事务功能，生产者发送数据之前开启rabbitmq事务（channel.txSelect），然
		后发送消息，如果消息没有成功被rabbitmq接收到，那么生产者会收到异常报错，此时就可以回滚事（channel.txRollback)然后重试发送消息；如果收到了消息，那么可以提交事务

		方案二：
		在生产者开启confirm模式写消息的时候会分配一个唯一的id,然后将消息写入rabbitqm中，rabbitqm会回传一个ack消息通知生产者消息接收成功,否则会回调nack接口通知消息接收失败，生产者端可以维护这个唯一id，如果超过一定的时间没有接收到rabbitqm的回调通知,则可以重新发送消息。

	2.rabbitmq (持久化)
		①、将queue的持久化标识durable设置为true,则代表是一个持久的队列
		②、发送消息的时候将deliveryMode=2
	3.消费端弄丢了数据
		手动确认模式,关闭rabbitmq自动ack可以通过一个api来调用就行，然后每次你自己代码里确保处理完的时候，再程序里ack一把。

>2.消息队列满了怎么办?

	1.消息队列满了的情况下,就会丢失数据，此时可以在生产端重试发送,等消费端消费确认。
	2.如果还是不行，可以将消息记录到数据库，后期做补偿。（不太推荐，不方便）
	
# 前端

## bootstrap
