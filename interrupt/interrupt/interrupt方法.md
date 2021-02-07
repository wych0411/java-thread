1. interrupt中断操作时，非自身打断需要先检测是否有中断权限，这由JVM的安全机制配置；
2. 如果线程处于sleep、wait、join等状态，那么线程将立即退出被阻塞状态，并抛出一个InterruptedException异常；
3. 如果线程处于I/O阻塞状态，将会抛出ClosedByInterruptException（IOException的子类）异常；
4. 如果线程在Selector上被阻塞，select方法将立即返回；
5. 如果非以上情况，将直接标记interrupt状态。

> 注意：interrupt操作不会打断所有阻塞，只有上述三类阻塞情况才在JVM的打断范围内，如果处于锁阻塞的线程，不会受interrupt中断。

> 阻塞情况下中断，抛出InterruptedException后线程状态将恢复成非中断状态，即interrupted=false

```java
public class ThreadTest {
    
    public static void main(String[] args) {
    
        Thread t = new Thread(new Task("1"));
        t.start();
        t.interrupt();
    }
    
    static class Task implements Runnable {
        String name;
        
        public Task(String name) {
            this.name = name;
        }
        
        @Override
        public void run() {
            try{
                Thread.sleep(1000); // 处于阻塞状态的线程被中断时，将立即退出被阻塞状态，并抛出InterruptedException
            } catch(InterruptedException e) {
                System.out.println("thread has been interrupt!");
            }
            
            System.out.println("isInterrupted: " + Thread.currentThread().isInterrupted());
            System.out.println("task " + name + " is over");
        }
    }
}
```
输出
```
thread has been interrupt!
isInterrupted: false
task 1 is over
```

<br>
> 调用Thread.interrupted()方法后线程将恢复非中断状态：

```java
public class threadTest {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(new Task("1"));
        t.start();
        t.interrupt();
    }
}

static class Task implements Runnable {
    String name;
    
    public Task(String name) {
        this.name = name;
    }
    
    @Override
    public void run() {
        System.out.println("first: " + Thread.interrupted());
        System.out.println("second: " + Thread.interrupted());
        System.out.println("task " + name + " is over");
    }
}
```
输出结果：
```
first: true
second: false
task 1 is over
```
