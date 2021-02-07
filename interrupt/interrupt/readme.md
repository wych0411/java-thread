# 如果一个线程有被中断的需求，那么就需要做如下的处理：
1. 在正常任务运行时，经常检查本线程的中断标志位，如果被设置了中断标志就自行停止线程。
2. 在调用阻塞方法时正确处理InterruptedException异常。（例如catch异常后就结束线程）

# Thread类interrupt相关的几个方法：

```java
//核心interrupt方法
public void interrupt() {
    if(this != Thread.currentThread()) //非本线程，需要检查权限。
        checkAccess();
        
    synchronized(blockerLock) {
        Interruptible b = blocker;
        if(b != null){
            interrupt0();     //仅仅设置interrupt标志位
            b.interrupt(this);//调用如I/O操作定义的中断方法
            return;
        }
    }
    
    interrupt0();
}
```
```
//静态方法，这个方法有点坑，该方法调用后会清除中断状态。
public static boolean interrupted() {
    return currentThread().isInterrupted(true);
}
```
```
//这个方法不会清除中断状态
public boolean isInterrupted() {
    return isInterrupted(false);
}
```
```
//上面两个方法会调用这个本地方法，参数代表是否清除中断状态
private native boolean isInterrupted(boolean clearInterrupted);
```
