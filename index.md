# **线程的生命周期**

### 在线程的生命周期中，线程要经历新建（new），就绪（runnable），运行（running），阻塞（blocked）和死亡（dead）五种状态
##### 1.新建：使用new关键词新建一个线程后，该线程即处于新建状态，JVM为其分配内存并初始化各变量值。 
##### 2.就绪：创建完成后，对于在新建状态的线程调用start()方法后线程进入就绪状态，就绪状态状态下的线程被视为活动状态，可用isAlive()方法检验线程是否处于就绪状态，处于该状态下的线程由JVM创建方法调用栈和程序计数器，等待调度运行。
##### 3.运行：当CPU调用就绪状态的线程后，线程状态称为运行状态，该线程开始执行run()方法的线程执行体。
##### 4.阻塞：处于运行状态的线程出于某些原因放弃对CPU的使用权时，该线程进入阻塞状态
```
阻塞状态分类：
1. 睡眠阻塞：调用sleep()方法使线程进入睡眠阻塞状态，调用该方法需捕获InterruptedExecption异常。
2. 同步阻塞：当线程尝试获取同步锁(synchronized)时，同步锁被其他线程占用时，该线程进入同步阻塞状态。
3. 等待阻塞：调用wait()方法使线程进入等待阻塞状态。
4. suspend()方法可以挂起线程使线程进入阻塞状态，但易造成死锁[JDK1.2后过时]
```
##### 5.死亡：当线程运行完run()方法，或遭遇未捕获的异常时，线程进入死亡状态。（调用stop()方法也可以让线程进入死亡状态，因容易造成死锁所以弃用。）

# **线程的创建方式**
### 1.继承Thread类并覆盖run()方法
```
public class myThread extends Thread{
    run(){
        System.out.println("Thread is ready now.");
    }
}

//通过start()方法调用线程
new MyThread().start();
```
### 2.实现Runnable接口并重写run()方法
```
public class myThread implements Runnable{
    run(){
        System.out.println("Thread is ready now.");
    }
}
new myThread().start();
```
# **线程几个状态的切换条件** #
### 1.就绪到运行：获取CPU；
### 2.
