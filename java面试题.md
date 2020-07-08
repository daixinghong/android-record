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
	* equals() length() indexOf() lastIndexOf() subString() replace()  replaceAll()

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
	            <td>有序的</td>
	            <td>无序的</td>
				<td>不继承Collection接口</td>
	        </tr>
	  <tr>
	            <td>可以存重复的元素</td>
	            <td>不可存重复的元素</td>
	        </tr>
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
	* 
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
	            <td>当Vector中的元素超过它的初始大小时,Vector会将它的容量翻倍</td>
	            <td>当Vector中的元素超过它的初始大小时,Vector会将它的容量增加百分之50</td>
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
	