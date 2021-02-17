# 定时器

TimerTask实现了Runnable接口，Timer内部有个TimerThread继承自Thread，因此绕回来还是Thread + Runnable。
```java
public class DemoTimeTask {
  public static void main(String[] args) {
     Timer timer = new Timer();
     timer.scheduleAtFixdRate((new TimerTask() {
       @Override
       public void run() {
         System.out.println("定时任务1执行了....");
       }
     }), 2000, 1000);
  }
}
```
