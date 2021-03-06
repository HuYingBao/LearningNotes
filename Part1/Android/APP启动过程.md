# APP启动过程
---

![](http://7xntdm.com1.z0.glb.clouddn.com/activity_start_flow.png)

* 上图就可以很好的说明App启动的过程
* ActivityManagerService组织回退栈时以ActivityRecord为基本单位，所有的ActivityRecord放在同一个ArrayList里，可以将mHistory看作一个栈对象，索引0所指的对象位于栈底，索引mHistory.size()-1所指的对象位于栈顶
* Zygote进程孵化出新的应用进程后，会执行ActivityThread类的main方法.在该方法里会先准备好Looper和消息队列，然后调用attach方法将应用进程绑定到ActivityManagerService，然后进入loop循环，不断地读取消息队列里的消息，并分发消息。
* ActivityThread的main方法执行后,应用进程接下来通知ActivityManagerService应用进程已启动，ActivityManagerService保存应用进程的一个代理对象，这样ActivityManagerService可以通过这个代理对象控制应用进程，然后ActivityManagerService通知**应用进程**创建入口Activity的实例，并执行它的生命周期方法