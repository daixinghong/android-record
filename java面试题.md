# java基础
*  <h3>jdk和jre的区别</h3>
	* JDK是Java Development Kit的缩写，是Java的开发工具包，jdk中包含了jre
	* JRE是Java Runtime Environment的缩写，是Java程序的运行环境

* <h3>==和equals有什么区别？</h3>
	* ==是比较基本数据类型，因为基本数据存储的直接就是他们的值，所以就是直接比较的它们的值 引用数据类型使用==就是比较它们的堆内存地址值
	* equals比较的就是它们的堆内存地址值，不能用于基本数据类型的比较 对于String，Integer 这些类型，是因为它们重写了equals方法

* <h3>两个对象的 hashCode()相同，则 equals()也一定为 true，对吗？</h3>
	* 不一定 因为类的hashCode方法和equals方法都可以重写，返回的值完全在于自己定义。hashCode()返回该对象的哈希码值；equals()返回两个对象是否相等
	* 关于hashCode和equal是方法是有一些 常规协定 ：
	* 两个对象用equals()比较返回true，那么两个对象的hashCode()方法必须返回相同的结果。
	* 两个对象用equals()比较返回false，不要求hashCode()方法也一定返回不同的值，但是最好返回不同值，亿提搞哈希表性能。
	* 重写equals()方法，必须重写hashCode()方法，以保证equals方法相等时两个对象hashcode返回相同的值。

* <h3>final 在 java 中有什么作用？</h3>
	* final字面意思，最终的，不可变的
	* 在java中可以用于修饰变量，类，函数，被final修饰的变量为常量，必须定义的时候就赋值，不可以被修改，
	* 被final修饰的类不可以被继承，final修饰的类所有成员方法都将被隐式修饰为final方法，
	* 被final修饰的函数不可以被重写

* <h3>java 中的 Math.round(-1.5) 等于多少？</h3>
	* Math.round函数作用：四舍五入，负数返回较大整数，答案是-1

* <h3>String 属于基础的数据类型吗？</h3>
	* 不属于：8种基本数据类型分别是：int short long double float char byte Boolean

* <h3>java 中操作字符串都有哪些类？它们之间有什么区别？</h3>
	* String、StringBuffer、StringBuilder

	* String：final修饰，String的任何方法都是返回new String() String做任何操作都不会影响到原对象，对字符串的操作都会返回一个新的对象

	* StringBuffer : 对字符串的操作的方法都加了synchronized，保证线程安全

	* StringBuilder : 不保证线程安全，在方法体内需要进行字符串的修改操作，可以new StringBuilder对象，调用StringBuilder对象的append、replace、delete等方法修改字符串

* <h3>String str="i"与 String str=new String(“i”)一样吗？</h3>
	* 不一样 ，因为String str = "i" 相当于把"i"这个值在内存中的地址赋值给了str 如果再有String str3="i"；那么这句话的操作也是把“i”这个值在内存中的地址赋给str3,这两个引用的是同一个地址值，他们两个共享同一个内存。
	
	* 而String str2 = new String("i"); 则是将new String("i");的对象地址赋给str2，需要注意的是这句话是新创建了一个对象。如果再有String str4= new String("i");那么相当于又创建了一个新的对象，然后将对象的地址值赋给str4,虽然str2的值和str4的值是相同的，但是他们依然不是同一个对象了需要注意的是：String str="i"; 因为String 是final类型的，所以“i”应该是在常量池。而new String("i");则是新建对象放到堆内存中
	
* <h3>如何将字符串反转？</h3>
	* 使用Stringbuilder或者StringBuffer里面的reverse方法进行反转
	* 反向遍历进行字符串拼接
	
* <h3>String 类的常用方法都有那些？</h3>
	* equals()
	* length() 
	* indexOf() 
	* lastIndexOf() 
	* subString() 
	* replace()  
	* replaceAll()

* <h3>抽象类必须要有抽象方法吗？</h3>
	* 不一定

* <h3>抽象类和普通类有什么区别</h3>
	* 抽象类可以定义抽象方法，普通类不可以抽象方法
	* 抽象类不可以被实例化，普通类可以被实例化
	* 抽象方法不能被声明为静态
	* 抽象方法不能用 private 修饰
	* 抽象方法不能用 final 修饰

* <h3>Files的常用方法都有哪些</h3>
	* Files.exists() 检测文件路径是否存在
	* Files.createFile()创建文件
	* Files.createDirectory()创建文件夹
	* Files.delete() 删除文件或者目录
	* Files.copy() 复制文件
	* Files.move() 移动文件
	* Files.size（）查看文件个数
	* Files.read() 读取文件
	* Files.write()写入文件
# java容器 
* <h3>java 容器都有哪些？</h3>
	* List , ArrayList , LinkedList , Vector
	* Set  ,HashSet , LinkedHashSet , TreeSet
	* Map , HashMap , LinkedHashMap , HashTable , TreeMap
* <h3>Collection 和 Collections 有什么区别？</h3>
	* Collection是java容器的顶级父类，是一个接口，Collections是一个包装类，里面包含了很多静态方法，不能被实例化，是操作java容器的工具类	
* <h3>List、Set、Map 之间的区别是什么？</h3>
	   <table>
	       <tr>
	           <td>List(列表)</td>
	           <td>Set(集)</td>
  			   <td>Map(映射)</td>
	        </tr>
	        <tr>
		<td>继承Collection接口</td>
	       <td>继承Collection接口</td>
				<td>不继承Collection接口</td>
	        </tr>
	  <tr>
	            <td>可以存重复的元素</td>
	            <td>不可存重复的元素</td>
	        </tr>
		<tr>    <td>有序的</td>
	            <td>无序的</td></tr>
	 </table>




* <h3>HashMap 和 Hashtable 有什么区别？</h3>
	   <table>
	       <tr>
	           <td>hashMap</td>
	           <td>hashTable</td>
	        </tr>
	        <tr>
	            <td>允许有空键空值</td>
	            <td>不允许有空键空值</td>
	        </tr>
	  <tr>
	            <td>线程不安全</td>
	            <td>线程安全</td>
	        </tr>
	 </table>

* <h3>如何决定使用 HashMap 还是 TreeMap？</h3>
	* 首先TreeMap<Key,Value>的key是要求要实现java.lang.Comparable接口的，所以在遍历的时候，会按照自然排序或者是自定义的排序规则遍历键
	* HashMap<Key,Value> 是散列的，均匀的，不支持排序，是基于数组和链表结构实现的，适用于插入，删除和定位元素
	* 总结：如果你需要一个有顺序的Key列表，就使用TreeMap，HashMap不支持排序，但是性能更好，如果不需要排序key的时候，就使用HashMap
* <h3>说一下 HashMap 的实现原理？</h3>
	* HashMap的key是基于数组结构，value是基于链表结构
	* HashMap是拿到key的hash值,根据Hash值将value保存在bucket里
* <h3>说一下 HashSet的实现原理</h3>
	* HashSet是基于HashMap实现的，HashSet 底层使用HashMap来保存所有元素
	* HashSet是不允许存储重复值，并且他是无序的
* <h3>ArrayList 和 LinkedList 的区别是什么？</h3>
	   <table>
	       <tr>
	           <td>ArrayList</td>
	           <td>LinkedList</td>
	        </tr>
	        <tr>
	            <td>底层是基于动态数组</td>
	            <td>底层是基于链表结构</td>
	        </tr>
	  <tr>
	            <td>实现了randomaccess随机访问接口</td>
	            <td>实现了queue接口</td>
	        </tr>
	 </table>

* <h3>如何实现数组和 List 之间的转换</h3>
	* 数组转List
		* 可以通过遍历添加到另外一个容器中
		* 可以通过Arrays工具类 Arrays.asList(str) 转换
		* 使用使用Collections.addAll()全部添加到list中
		* 使用Stream中的Collector收集器 Stream.of(str).collect(Collectors.toList())
	* list转数组
		* 可以通过遍历添加到另外一个容器中
		* 可以使用toArray()方法 list.toArray(new String[list.size()]);

* <h3>ArrayList 和 Vector 的区别是什么？</h3>
	   <table>
	       <tr>
	           <td>ArrayList</td>
	           <td>vector</td>
	        </tr>
	        <tr>
	            <td>线程不安全</td>
	            <td>线程安全</td>
	        </tr>
	  <tr>
	            <td>当ArrayList中的元素超过它的初始大小时,ArrayList只会增加当前容量的百分之50</td>
	            <td>当Vector中的元素超过它的初始大小时,Vector会将它的容量翻倍</td>
	        </tr>
	 </table>
* <h3>Array 和 ArrayList 有何区别</h3>
	<table>
       <tr>
           <td>Array</td>
           <td>ArrayList</td>
        </tr>
        <tr>
            <td>长度是固定的</td>
            <td>长度不固定，可以动态扩容</td>
        </tr>
  <tr>
            <td>只能存储基本数据类型</td>
            <td>可以存储基本数据类型和引用数据类型</td>
        </tr>
 </table>

* <h3>在 Queue 中 poll()和 remove()有什么区别？</h3>
	* poll()和remove()都将移除并且返回队头，但是在poll()在队列为空时返回null，而remove()会抛出NoSuchElementException异常。

* <h3>哪些集合类是线程安全的？</h3>
	* HashTable
	* Vector
	* ConcurrentHashMap
	* Stack

* <h3>迭代器 Iterator 是什么？ 有什么特点</h3>
	* 迭代器是一种设计模式，用于顺序访问集合对象元素，无需知道集合对象的底层实现。
	* Iterator 是可以遍历集合的对象，为各种容器提供了公共的操作接口，隔离对容器的遍历操作和底层实现，从而解耦
	* 缺点是增加新的集合类需要对应增加新的迭代器类，迭代器类与集合类成对增加。

* <h3>Iterator 和 ListIterator 有什么区别？</h3>
	* ListIterator 继承 Iterator
	* Iterator
		* Iterator可以迭代所有集合 ListIterator 只能用于List及其子类
	* ListIterator
		* ListIterator 只能用于List及其子类
		* 有 add 方法，可以向 List 中添加对象 Iterator 不能
		* 有 hasPrevious() 和 previous() 方法，可以实现逆向遍历；Iterator不可以
		* 有 nextIndex() 和previousIndex() 方法，可定位当前索引的位置；Iterator不可以
		* 有 set()方法，可以实现对 List 的修改；Iterator 仅能遍历，不能修改
* <h3>怎么确保一个集合不能被修改？</h3>
	* 使用Collections包下的unmodifiableMap方法，通过这个方法返回的map,是不可以修改的
	* Collections.unmodifiableList(List)  
	* Collections.unmodifiableSet(Set)		

# java多线程
* <h3>并行和并发有什么区别？</h3>
	* 并发：指的是一个处理器在不同的时间段处理多个的请求
	* 并行：多个处理器在同时处理多个请求

* <h3>线程和进程的区别</h3>
	* 进程：是操作系统最基本的单元，一个应用只有一个进程
	* 线程：线程是运行在进程上的，一个进程可以有多个线程

* <h3>守护线程是什么？</h3>
	* 通常来说，守护线程经常被用来执行一些后台任务，但是呢，你又希望在程序退出时，或者说 JVM 退出时，线程能够自动关闭，此时，守护线程是你的首选

* <h3>创建线程有哪几种方式？</h3>
	* 4种
		* new Thread().start();
		* new Runable();
		* 线程池
		* Callable

* <h3>说一下 runnable 和 callable 有什么区别？</h3>
	* Runnable执行方法是run(),Callable是call()
	* 实现Runnable接口的任务线程无返回值；实现Callable接口的任务线程能返回执行结果
	* call方法可以抛出异常，run方法若有异常只能在内部消化

* <h3>线程有哪些状态？</h3>
	* 5种
		* 新建 （创建了Thread线程）
		* 就绪 （调用的start方法不代表就开始运行程序了，运行程序不是代码控制的，而是操作系统控制的）
		* 运行 （当cpu已经在运行这条程序的时候就是运行中了）
		* 阻塞 （当子线程遇到同步锁，sleep ，wait，就会进入阻塞状态）
		* 死亡 （当线程把代码执行完成之后就死亡了）

* <h3>sleep() 和 wait() 有什么区别？</h3>
	* sleep() 睡眠，不需要唤醒，到时间自动被唤醒，wait()则需要notify或者notifyAll方法
	* sleep() 不会释放锁，如果你在Synchronized同步代码块中执行sleep()方法，其他线程仍然无法获取到对象锁

* <h3>notify()和 notifyAll()有什么区别？</h3>
	* notify就是唤醒一条线程从等待池中进入锁池
	* notifyAll是唤醒所以在等待池中的线程进入锁池


* <h3>线程的 run()和 start()有什么区别？</h3>
	* start()是用来启动线程的，线程要开始运行的时候会自动调用run()方法，
	* 一个线程对start()方法只能调用一次，run()可以调用多次
* <h3>创建线程池有哪几种方式？</h3>
	* 4种
		* newCachedThreadPool 
		* newFixedThreadPool 
		* newScheduledThreadPoo
		* newSingleThreadExecutor 

* <h3>线程池都有哪些状态？</h3>
	* 5种状态
		* RUNNING  
			* 线程池处在RUNNING状态时，能够接收新任务，以及对已添加的任务进行处理。 
			* 线程池的初始化状态是RUNNING。换句话说，线程池被一旦被创建，就处于RUNNING状态，并且线程池中的任务数为0！
		* SHUTDOWN
			* 线程池处在SHUTDOWN状态时，不接收新任务，但能处理已添加的任务。
			* 调用线程池的shutdown()接口时，线程池由RUNNING -> SHUTDOWN。
		* STOP
			* 线程池处在STOP状态时，不接收新任务，不处理已添加的任务，并且会中断正在处理的任务
			* 调用线程池的shutdownNow()接口时，线程池由(RUNNING or SHUTDOWN ) -> STOP。
		* TIDYING
			* 当所有的任务已终止，ctl记录的”任务数量”为0，线程池会变为TIDYING状态。当线程池变为TIDYING状态时，会执行钩子函数terminated()。terminated()在ThreadPoolExecutor类中是空的，若用户想在线程池变为TIDYING时，进行相应的处理；可以通过重载terminated()函数来实现
			* 当线程池在SHUTDOWN状态下，阻塞队列为空并且线程池中执行的任务也为空时，就会由 SHUTDOWN -> TIDYING。 
		* TERMINATED
			* 线程池彻底终止，就变成TERMINATED状态
			* 线程池处在TIDYING状态时，执行完terminated()之后，就会由 TIDYING -> TERMINATED。

* <h3>线程池中 submit()和 execute()方法有什么区别？</h3>
	* submit和execute都是往线程池里面提交任务
	* submit没有返回值，execute有返回值
	* execute可以根据返回值查看任务执行结果，如果任务执行失败，可以获取到执行失败的异常

* <h3>在 java 程序中怎么保证多线程的运行安全？</h3>
	* 原子性：一个或者多个操作在 CPU 执行的过程中不被中断的特性
	* 可见性：一个线程对共享变量的修改，另外一个线程能够立刻看到
	* 有序性：程序执行的顺序按照代码的先后顺序执行
		* 导致原因：
			* 缓存导致的可见性问题
			* 线程切换带来的原子性问题
			* 编译优化带来的有序性问题
		* 解决办法：
			* JDK Atomic开头的原子类、synchronized、LOCK，可以解决原子性问题
			* synchronized、volatile、LOCK，可以解决可见性问题
			* Happens-Before 规则可以解决有序性问题
		
				
		
		
