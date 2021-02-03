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
     */
