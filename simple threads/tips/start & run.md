# 为什么线程的实现逻辑在run()里，而启动线程要调用start() ?

    /**
     * Causes this thread to begin execution; the Java Virtual Machine calls the  run() method of this thread.
     * 1. start方法将导致this thread开始执行。由JVM调用this thread的run方法。
     * 
     * The result is that two threads are running concurrently: the current thread (which returns from the call to the start() method) and other thread (which executes its run() method).\
     * 2. 结果是：调用start方法的'当前线程'和执行run方法的'另一个线程'同时运行。
     *
     * It is never legal to start a thread more than once. In particular, a thread may not be restarted once it has completed execution.
     * 3. 多次启动线程永远不合法。特别是，线程一旦完成执行就不会重新启动。
     * @exception IllegalThreadStateException if the thread was already started.
     * 如果线程已启动，则抛出异常。
     * @see #run()
     * @see #stop()
     */
```java
 /**
  * This method is not invoked for the main method thread or "system" group threads created/set up by the VM. Any new functionality added to this method in the future may have to also be added to the VM.
  * 4. 对于由VM创建/设置的main方法线程或"system"组线程，不会调用此方法。未来添加到此方法的任何新功能可能也必须添加到VM中。
  *
  * A zero status value corresponds to state "NEW".
  * 5. status=0代表是“NEW”。
  */
 public synchronized void start() {
     if(threadStatus != 0)
         throw new IllegalThreadStateException();
         
     /**
      * Notify the group that this thread is about to be started so that it can be added to the group's list of threads and the group's unstarted count can be decremented.
      * 6. 通知组该线程即将启动，以便将其添加到线程组的列表中，并且减少线程组的未启动线程数递减。
      */
     group.add(this);
     boolean started = false;
     
     try{
         // 7. 调用native方法，底层开启异步线程，并调用run()方法。
         start0();
         started = true;
     }finally{
         try{
             if(!started){
                 group.threadStartFailed(this);
             }
         }catch(Throwable ignore){
             /**
              * do nothing. If start0 threw a Throwable then it will be passed up the call stack.
              * 8. 忽略异常。如果start0抛出一个Throwable，它将被传递给调用堆栈。
              */
         }
     }
 }
 
 private native void start0();
 ```

&emsp;&emsp;start()方法用synchronized修饰，是同步方法；<br>
&emsp;&emsp;虽然是同步方法，但不能避免'多次调用'问题。针对此问题，Thread中设计了用threadStatus来记录线程状态，如果线程被多次start就会抛出异常，而threadStatus的状态是由JVM控制的。<br>
&emsp;&emsp;start()方法中线程的启动逻辑比较清晰，如果要探究更底层的原理，就要研究native方法start0了。

> 使用runnable时，主线程无法捕获子线程中的异常状态。线程的异常，应在线程内部解决。
