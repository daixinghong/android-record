
*  <h3>synchronized与Lock的区别</h3>
	* 首先synchronized是java内置关键字，在jvm层面，Lock是个java类
	* synchronized无法判断是否获取锁的状态，Lock可以判断是否获取到锁<br></br>
	* synchronized会自动释放锁(a 线程执行完同步代码会释放锁 ；b 线程执行过程中发生异常会释放锁)，Lock需在finally中手工释放锁（unlock()方法释放锁），否则容易造成线程死锁 
	* 用synchronized关键字的两个线程1和线程2，如果当前线程1获得锁，线程2线程等待。如果线程1阻塞，线程2则会一直等待下去，而Lock锁就不一定会等待下去，如果尝试获取不到锁，线程可以不用一直等待就结束了；<br></br>
	* synchronized的锁可重入、不可中断、非公平，而Lock锁可重入、可判断、可公平（两者皆可）
	* Lock锁适合大量同步的代码的同步问题，synchronized锁适合代码少量的同步问题。<br></br>

* <h3>Handler机制如何保证消息不错乱？</h3>
	* 1.handler机制中多个handler共有一个looper不会错乱是因为在handler 发送消息的时候，会将当前的handler对象绑定到message的target属性上，然后在Looper取到消息后通过msg.target拿到之前的handler对象，然后调用handler的handleMessage方法。<br></br>
* <h3>Handler消息延迟是如何实现的</h3>
	* handler发送延迟消息，会将当前的延迟时间绑定到msg的when属性上，然后在循环MessageQUeue获取msg时判断如果当前有延迟就进行阻塞，通过计时器计算时间，时间通过系统启动计算时间，然后等待阻塞时间结束之后将其唤醒，在阻塞过程中会将之后的消息放在消息队列的头部去处理

* <h3>Handler、Looper、MessageQueue三者对应关系？</h3>
	* 同一个线程中可以有多个Handler，只有一个Looper，而MessageQueue在looper中初始化的，所以也只有一个MessageQueue。因此对应关系是：Handler：Looper = 多对一，Looper：MeesageQueue = 一对一，Handler：MessageQueue = 多对一。<br></br>
* <h3>内存泄漏如何避免？</h3>
	* Handler的内存泄漏是由于Handler持有外部类的引用，使其无法释放。
解决办法：(1)定义成静态内部类，使其不持有外部类的引用；(2)可以使用弱引用；
还需要在外部类销毁的时候，移除所有的消息。<br></br>
* <h3>Looper中的死循环为什么不会引器主线程ANR？</h3>
	* 可以说整个应用的生命周期都是在looper.loop()控制之下的（在应用启动的入口main函数中初始化ActivityThread，Handler，Looper，然后通过handler和looper去控制初始化应用）。而looper.loop采用的是Linux的管道机制，在没有消息的时候会进入阻塞状态，释放CPU执行权，等待被唤醒。真正会卡死主线程的操作是在回调方法onCreate/onStart/onResume等操作时间过长，会导致掉帧，甚至发生ANR，looper.loop本身不会导致应用卡死。<br></br>
* <h3>IO与NIO的区别？</h3>
	  <table>
       <tr>
           <td>IO</td>
           <td>NIO</td>
        </tr>
        <tr>
            <td>面向stream</td>
            <td>面向buffer</td>
        </tr>
  <tr>
            <td>阻塞</td>
            <td>非阻塞</td>
        </tr>
 </table>	
	*	第一点：IO是面向流的，NIO是面向缓冲区的。
IO面向流意味着每次从流中读一个或多个字节，直至读取所有字节，它们没有被缓存在任何地方。此外，它不能前后移动流中的数据
	* NIO是面向缓存的。数据读取到一个缓冲区，需要时可在缓冲区中前后移动。这就增加了处理过程中的灵活性。但是，还需要检查是否该缓冲区中包含所有您需要处理的数据。而且要确保当更多的数据读入缓冲区时，不要覆盖缓冲区中未处理的数据<br></br>
	* 第二点：IO的各种流是阻塞的。这意味着，当一个线程调用read() 或 write()时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情
	* NIO的非阻塞模式，使一个线程从某通道发送请求读取数据，但是它仅能得到目前可用的数据，如果目前没有数据可用时，就什么都不会获取，而不是保持线程阻塞，在数据可读之前，该线程可以继续做其他的事情。 非阻塞写也是如此
	* 一个线程请求写入一些数据到某通道，但不需要等待它完全写入，这个线程同时可以去做别的事情。 线程通常将非阻塞IO的空闲时间用于在其它通道上执行IO操作，所以一个单独的线程现在可以管理多个输入和输出通道<br></br>
	
* <h3>单例模式有几种写法以及各自的优劣？</h3>
	* 饿汉式：
<pre class="prettyprint lang-javascript">
	public class SingleInstance {
    
    private static SingleInstance mInstance = new SingleInstance();
    
    private SingleInstance(){}
    
    public static SingleInstance getInstance(){
        return mInstance;
    }
	}

</pre> 
		* 缺点：存在内存损耗问题，如果当前类没有用到也会被实例化
* 懒汉式：
<pre class="prettyprint lang-javascript">
	public class SingleInstance {

    private static SingleInstance mInstance = null;

    private SingleInstance(){}

    public static SingleInstance getInstance(){
        if(mInstance==null){
            synchronized (SingleInstance.class){
                if(mInstance==null){
                    mInstance = new SingleInstance();
                }
            }
        }
        return mInstance;
    }
	}

</pre>
		* 缺点:加了synchronized锁会影响性能
	* 为什么做两次非空判断
		* 有次被问到为什么要有两次空判断？
		第一次空判断和好理解，可以很大程度上减少锁机制的次数；
		第二次判空是因为，如果a，b两个线程都到了synchronized处，而假设a拿到了锁，进入到代码块中创建了对象，然后释放了锁，由于b线程在等待锁，所以a释放后，会被b拿到，因此此时判空就保证了实例的唯一性。<br></br>

*静态内部类：
<pre class="prettyprint lang-javascript">
	public class SingleInstance {

    private SingleInstance(){}

    public static SingleInstance getInstance(){
        return Builder.mInstance;
    }
    
    private static class Builder{
        
        private static SingleInstance mInstance = new SingleInstance();
    }
	}
</pre>
	*优点：解决了内存浪费问题，同时也避免了加锁性能问题
	*为什么这种写法是线程安全的？因为类加载过程是安全的，而静态变量是随着类的加载进行初始化的。

* 4.枚举形式：
<pre class="prettyprint lang-javascript">
	public enum SingleInstance {
    
        INSTANCE;
    
	}

</pre>
		* 优点:不存在反射和反序列化的问题
		* 缺点:通过查看枚举类生成的class文件发现，有多少变量，就会在静态代码块中创建多少对象，所以不建议使用。

	
* 	<h3>ArrayList 和LinketList区别？</h3>
	  <table>
       <tr>
           <td>arrayList</td>
           <td>LinketList</td>
        </tr>
        <tr>
            <td>实现了randomaccess随机访问接口</td>
            <td>实现了queue接口</td>
        </tr>
  <tr>
            <td>基于动态数组实现</td>
            <td>基于链表实现</td>
        </tr>
 </table>
	* ArrayList基于数组实现，所以get，set操作效率较高；
	* LinketList基于链表实现（双向链表），所以add，remove操作效率较高；<br></br>
* <h3>如何实现高效率的查询和插入结构？</h3>
	* 二叉树或者散列表<br></br>
*	<h3>hashmap的实现原理？hashmap与hashtable的区别？</h3>
	* hashmap是由数组+链表结构现实的。获取到key的hashcode，然后对数组长度取余，找到对应的数组位置index，然后在对应的链表中判断是否有当前key，从而进行查询/添加/替换等操作。
	* hashMap和hashTable的区别
		* <table>
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
* 	<h3>gson序列化数据时如何排除某个字段？</h3>
	* 	方式一:给字段加上 transient 修饰符
	* 	方式二:排除Modifier指定类型的字段。这个方法需要用GsonBuilder定制一个GSON实例。
	* 	方式三:使用@expose注解。没有被 @expose 标注的字段会被排除<br></br>
* 	<h3>ButterKnife与Xutils注解的区别？</h3>
	* 	ButterKnife采用的是编译时注解，在编译时生成辅助类，在运行时通过辅助类完成操作。编译时注解运行效率较高，不需要反射操作。
	* 	XUtils采用的是运行时注解，在运行时通过反射进行操作。运行时注解相对效率较低<br></br>
	
* 	<h3>Retrofit中的注解是如何处理的</h3>
	* 	Retrofit与EventBus采用的都是运行时注解，也就是通过反射技术处理的。<br></br>

* 	<h3>AsyncTask的原理以及弊端？AsyncTask为什么要求在主线程加载，对象为什么要在主线程创建？</h3>
	* 	AsyncTask内部封装了两个线程池和一个Handler。两个线程池作用分别是：用于任务队列的线程池和用于执行的线程池。执行线程池的核心线程数是2-4之间，也取决于cpu核数，最大线程数是2*cup核数，线程队列定义的是128。而Handler的作用主要是进行线程间通信。
一个AsyncTask对象只能被执行一次，也就是只能调用一次execute，否则会抛异常。
而AsyncTask的任务队列通过synchronized关键字实现的是串行执行。而且由于AsyncTask内部线程池定义成了静态变量，所以整个进程的所有asyncTask全部都在这个串行线程池中排队执行，而且执行都使用同一个线程池，因此，在任务量较多时，效率不高，不建议使用。<br></br>
	*	AsyncTask中的Handler是静态全局变量，而且还在handleMessage方法中获取了主线程的Looper为了能够进行线程间切换，所以就要求Handler对象在主线程中创建，execute方法必须在主线程执行。由于静态成员变量，会随着类的加载而加载，因此就需要AsyncTask在主线程中加载。（Android4.1及以上已有系统完成主线程加载，是在ActivityThread的main方法中调用了AsyncTask的init方法，就满足了类在主线程中加载。）<br></br>
	
* 	<h3>Android开发中的屏幕适配方案？</h3>
	* 	第一种就是宽高限定符适配 (**在资源文件下生成不同分辨率的资源文件，然后在布局文件中引用对应的 dimens**)
	* 	第二种就是 鸿神 的 AndroidAutoLayout <br></br>
* 	<h3>多线程中sleep和wait的区别？</h3>
	* sleep是thread类里面的，而wait是object类的
	* 使用sleep休眠的线程，让cpu执行其他的线程，但是sleep不会释放锁，其他的线程是不能进来的，而wait是会释放锁的
	* sleep是休眠指定时间，到了时候之后cpu会自动继续执行该线程，而调用了wait方法，需要调用notify方法来唤醒<br></br>
* 	<h3>ThreadLocal作用？</h3>
	* ThreadLocal是一个线程内的数据存储类，可以通过它在指定线程中存储数据，并且只有在当前线程可以获取到存储的数据。通常当某些数据以线程为作用域并且不同线程具有不同的数据副本时使用。
通过查看源码可以知道，set方法会通过values()方法拿到当前线程的ThreadLocal数据（Thread类中有个成员变量专门存储ThreadLocal数据：ThreadLocal.Values localValues），在localValues内部有个数组Object[] table，用于存储ThreadLocal的值，而位置存储在ThreadLocal的reference的下一个位置。
而get方法就是通过当前线程的reference拿到localValues中table的位置，然后index+1获取数据<br></br>
* 	<h3>深复制（深拷贝）与浅复制（浅拷贝）的区别？</h3>
	* 	
* 	<h3>Activity中的context与Application中的context区别？</h3>
	* 	
* 	<h3>在使用git管理时，commit到本地库后，发现漏了文件，如何处理？（rebase命令合并两次commit的数据）</h3>
	* 
* <h3>关于协程的概念</h3>	
	* 简单的介绍：协程又称微线程，是一个线程执行。协程看上去也是子程序，但是不同的是可以在子程序内部中  断转而去执行其他子程序，然后在合适的时候再返回中断位置继续执行。
	* 协程特点：
执行效率高：没有多线程的线程间切换的开销；
不需要多线程的锁机制：因为只有一个线程，所以不需要锁机制。<br></br>
*	<h3>开发过程中如果想替换第三方jar中的某个class文件，或者在开发时你的class文件与jar中的重名，但是你想使用自己的应该如何解决？如果你替换掉某个方法又该怎么解决？</h3>
	*	方式一：可以获取到jar的源码或者将jar反编译获取到java项目，然后替换掉自己想要的.java文件或者方法；
	*	方式二：可以通过类加载器将目标class替换成自己的class；<br></br>
* <h3>Android开发过程中的版本适配问题？</h3>
	* - Android4.4适配：uri转path需要适配
	* - Android5.0适配：分包适配 -〉在5.0及以上在app的gradle文件中配置multiDexEnabled true即可，但是5.0以下需要倒入jar，然后在Application的attch方法中进行初始化
	* - Android6.0：权限适配 -〉敏感权限动态申请；
	* - Android7.0：Uri.fromFile()适配 -〉使用FileProvider进行适配；Android出于安全考虑关闭了网络/拍照/录像系统广播；
	* - Android8.0:Service启动方式适配 -〉需要使用startForegroundService()启动服务；Notification适配 -〉添加了渠道和组的概念；
	* 软件安装适配 -〉Android8.0去掉了“允许未知来源”选项，需要用户手动确定，所以安装程序需要在AndroidManifest.xml文件中添加REQUEST_INSTALL_PACKAGES权限；广播适配 -〉AndroidManifest.xml中注册的广播不能使用隐式，需要明确指定。权限适配-〉读写权限分离
	* 8.0 如小米 华为 oppo vivo 根据官网来适配刘海屏(凹凸屏)，9.0根据google来的规则适配刘海屏(凹凸屏)
	* Android9.0 如果网络请求url不是https的需要做适配