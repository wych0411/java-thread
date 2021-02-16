# 继承Thread类 vs 实现Runnable接口

&emsp;&emsp;需要注意的是，继承Thread方式，target对象为null，重写了run()方法，导致Runnable中的线程原生的run()方法失效，因此并不会调用到target.run()的逻辑，而是直接调用子类重写的run()方法。

&emsp;&emsp;因为Java是单继承，此方式一般不常用。
