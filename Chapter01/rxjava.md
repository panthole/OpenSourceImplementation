##一、RxJava简介
GitHub：https://github.com/ReactiveX/RxJava version1.X version2.X
RxJava 22440 Star  Retrofit 19719 Star  Okhttp 18335 Star

RxJava开始有Netflix开发和应用，后来也归属于由微软领导的ReactiveX这个社区

ReactiveX是Reactive Extensions的缩写，一般简写为Rx
Rx是一个使用可观察数据流进行异步编程的编程接口，ReactiveX结合了观察者模式、迭代器模式和函数式编程的精华
Rx是一个多语言实现，例如RxSwfit
ReactiveX不仅仅是一个编程接口，它是一种编程思想的突破，它影响了许多其它的程序库和框架以及编程语言

##二、RxJava介绍
Reactive Extensions for the JVM – a library for composing asynchronous and event-based programs using observable sequences for the Java VM.
一个在Java VM上使用可观测的序列来组成异步的、基于事件的程序库

##三、RxJava关键词
异步、响应式编程、基于事件，观察者模式

响应式编程是一种基于异步数据流概念的编程模式
同步：消费者从生产者那里以同步的方式得到值
异步：生产者以异步的方式把值推给观察者
##四、有无RxJava对比
当前代码
1.

2.

3.

4.

5.

使用RxJava的代码
1.

2.

3.


总结：
优点:
1.RxJava具有简洁的异步编程和线程切换
   避开繁琐的handler、asynctack、runOnUiThread、loader
2.链式写法、统一异常处理
   代码逻辑清晰、结构清晰
3.丰富强大的操作符
    减少和统一了业务逻辑处理，更少的BUG

缺点：


##五、RxJava初探
RxJava 有四个基本概念：Observable (可观察者，即被观察者)、 Observer (观察者)、 subscribe (订阅)、事件。Observable 和 Observer 通过 subscribe() 方法实现订阅关系，从而 Observable 可以在需要的时候发出事件来通知 Observer。




##六、RxJava实战场景
实战一、独立版图片剪切流程


实战二、去抖动

实战三、组合数据请求
组合数据请求   
1.  A和B可以并发进行，但需要数据都拿到后进行整合才能用

除了Zip， 还有Merge等，适用具体场景略有区别

2.  B请求依赖于A请求的数据结果


这里使用flatmap操作符，注意与map的区别

实战四、异常处理
1.unchecked Exception (避免这一类型的崩溃、避免了到处写异常处理)


2.checked Exception




3.RetryWhen和Flatmap合用实现Token获取
对于非一次性的 token (比如Cookie)，在获取 token 后将它保存起来反复使用，并通过 retryWhen() 实现 token 失效时的自动重新获取，将 token 获取的流程彻底透明化，简化开发流程。


实战五、基于RxJava的一系列开源项目（RxLifecycle、Rxbus、RxCache、RxBinding等）
1.内存泄露 RxLifecycle
在生命周期的某个时刻取消订阅。一个很常见的模式就是使用CompositeSubscription来持有所有的Subscriptions，然后在onDestroy()或者onDestroyView()里取消所有的订阅


2.事件总线 Rxbus

3.数据缓存 RxCache

网络请求的数据缓存

##七、RxJava核心概念
1.观察者模型 Observables
Observable.subscribe(Observer)



2.变换 Operator 
转换操作符、过滤操作符、组合操作
filter(Func1) 过滤事件，返回false的事件将被抛弃
map(Func) 事件参数类型映射变换器，可将输入的事件参数类型通过自定义函数解析变换为另一实体类型
flatMap(Func) 事件参数类型分解映射变换器，可将输入的单个事件类型解析、分解、变换为一个新的次级Observable对象（包含可发送不定量异步事件），直观上是把每个单一事件映射为每一组新的（异步）事件，用于事件分解或插入新的异步操作


http://reactivex.io/documentation/operators.html#alphabetical

3.线程调度控制 Scheduler
在RxJava 中，Scheduler ——调度器，相当于线程控制器，RxJava 通过它来指定每一段代码应该运行在什么样的线程。RxJava 已经内置了几个 Scheduler ，它们已经适合大多数的使用场景：
Schedulers.immediate() 默认调度器，在当前线程下执行
Schedulers.newThread() 无条件开启新线程执行
Schedulers.io() 使用IO线程池执行，线程池大小无上限
Schedulers.computation() 使用计算型线程池执行，线程池大小为CPU核心数量
AndroidSchedulers.mainThread() Android的主线程（UI线程）
有了这几个 Scheduler ，就可以使用 subscribeOn() 和 observeOn() 两个方法来对线程进行控制了。 * subscribeOn(): 指定 subscribe() 所发生的线程，即 Observable.OnSubscribe 被激活时所处的线程。或者叫做事件产生的线程。 * observeOn(): 指定 Subscriber 所运行在的线程。或者叫做事件消费的线程。





这里的scheduler3已经是subscribe.next的回调的时候，没有意义了

##八、RxJava原理分析
观察者模式



##代码

九、RxJava 和 RxJava2的区别
1.RxJava 1.x和RxJava 2.x相互独立，包名不同 
RxJava1.x 中的包名rx.
RxJava2.x 中的包名io.reactivex.
2.基于Reactive Stream规范,背压 Backpressure 生产者的速度大于消费者的速度
3.在RxJava2里，引入了Flowable这个类：Observable不包含Backpressure处理，而Flowable包含。

##十、目的
由于后续的架构希望引入响应式编程的思想，会使用基于RxJava的一系列Rx开源项目
本次分享的目的
1.普及RxJava的背景知识和基本使用
2.了解RxJava的基本原理
3.了解响应式编程的思想，应用在项目实践中

 

##参考
1. 给 Android 开发者的 RxJava 详解 https://gank.io/post/560e15be2dca930e00da1083
2. Reactive Streams http://www.reactive-streams.org/
3. What's different in 2.0 https://github.com/ReactiveX/RxJava/wiki/What's-different-in-2.0
4. Reactive-Streams API（一）：概览  https://blog.piasy.com/AdvancedRxJava/2016/09/10/the-reactive-streams-api-part-1/
5. ReactiveX文档中文翻译 https://www.gitbook.com/book/mcxiaoke/rxdocs
6. Operators http://reactivex.io/documentation/operators.html#alphabetical


