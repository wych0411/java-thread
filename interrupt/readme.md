# 暴力中断线程

## Thread.stop Thread.suspend Thread.resume都已经被废弃了，因为它们太暴力了，是不安全的。

> 初始的Java版本中定义了一个stop方法来终止一个线程，还定义了一个suspend方法来阻塞一个线程，直到另一个线程调用resume方法。stop和suspend方法在Java SE 1.2之后就被弃用了，因为这两种方法都不安全。
