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
[image](<mxfile host="app.diagrams.net" modified="2021-04-11T03:19:38.393Z" agent="5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36" etag="hZutEXfjtrrEeYsnCkO7" version="14.5.10" type="github"><diagram id="Bxwihh6jPsrpgNfdOrA-" name="Page-1">7Vtdk5s2FP01mkkf2kHiS3oEGzeT6WbSbpp2H1mjtUkwcrEc2/31kUCYL63tZtbAupnxA7pIAu7RufdcgYE5We1/zcL18o5FNAHIiPbAnAKEoIUQkD8jOhQW13AKwyKLI9WpMtzH/1JlNJR1G0d00+jIGUt4vG4a5yxN6Zw3bGGWsV2z2xNLmlddhwvaMdzPw6Rr/SuO+LKwYuRW9rc0XizLK0OHFGdWYdlZPclmGUZsVzOZATAnGWO8OFrtJzSRziv9UoybPXP2eGMZTfklA7aPu0e8/30bv78L3z7s3tFP/3z8Gat744fygWkknl81WcaXbMHSMAkqq5+xbRpROashWlWf3xhbCyMUxs+U84MCM9xyJkxLvkrUWbqP+d9y+C+2aj3Uzkz3aua8cSgbKc8OtUGy+VA/Vw3LW+W44vnkQz3rNmXasG02pyd8VS6/MFtQfqIfOoIrWEHZior7EeMymoQ8/tq8j1Atz8WxX4WgOFAg/gdA1bxfw2SrrgQCG2AMiC8PfB/4HghcgD3gOyBwADYAhiCYAX8iur2nu/KYdJZGE/jdMub0fh3mPtsJ9jdBVvdBM073p13fdVU5wFDUOZTkUu1dxUSiTMsaCR3jSs7tuqRHtsAaVyrmnGNLgysVda7PFnQhW8wh2YK0bPEN4ENJEsEW7xRb/timafgoYB4tZY5cOEMZ+1qUKSn7gzMXcMa8kDPWoBnGGY9mMC5EtKkZ4PgQtQdF1B0PoqNXgZciCoeF9IewvwKkg8ZdZA8LKfouTN2xR95BqzVToz8x8GdAaDRx4EGAJ2f0Z5wuxiM/Teu8/DxK1F70p6XxsAO8qdT2gSWLYQ+e8PCUhtF43Os4Lffa9kXq/moFMRpU3Ru1gHSxuoeNJKOiWj8hyX4NIcnWEIYAgnPC2JItJDhBGD9h8y90RJwxLdTgjKspiJ0eA5LT9W+HQmnkya1r0Zon4WYTz1vr/+qS6bwU0vu85lT7RJS/eCWrK3xgsbjBapPDshuQWi2sCiKqQfUd8dY8VitbmbA1UeGGzkQ57sen/v6l4HaWQkp3wvBxmYm08+anzsIQLODNpbDhGftCJyxhmbCkLJUB9ilOkpYpTOJFKteTQJoKuy85Fc/DxFMnVnEU5dFZx8gmZ1+AlLDleQ0ptTIBXS2RWYMmsheol3qU1tB6DYkM6qSfyGRWnq5EJgsA8TS5beiEZeEmNyxTQw7Uq8obdH/ole3hwktV3rC7CVCn81xZGAnNJt+BBADbI2QHJGNjByQaT2L5Egmb0qUi4Hh4k1C6Fhld6mUMiPNZaIqiKcSnT+SBbwLS3eK5mZRvEqsBHNRsDVi9pnz9q3KxvuSeS75H4Nm1jKEKnM0hnS8zloqwdaLKuRnYbLOlkYmGb06vuKEObtlWTybJNgI8t7GXJqIZMfPOU0BmR0ZKpAXMAvXiALt5n0n+Blj0meYTYoAD4Ls5rz2ArTxUihVQvDfG8ldNaAM8AwSqICCvlS8mQvL7mcmfvJYhf7KzK7ejbnYlWXZr88rSrKRe302j7vbrLoz5LRdex+/qTtC53yjc3Q/ZCOl00yDANhOMoUHAWgmjQl0RxhwVq0j+QYwIZjI5qpyYMh4/Hf4H2dB0zqvPfpHris9SaqJZKTI7Oe9m8UGt2hnigfEp10cNn3ef7tQnmbjglC3FhbQ4ecllSw0iqq46AUU1RtzJhz9vF7l2XYd0OrNf6Lr1wSGmyU3vy6L2jvjQ8c3sin1dZnq2bHtTL9duGbhW4LM1n0pD92WQE83qXwvFu5Dqvx9m8A0=</diagram></mxfile>)
