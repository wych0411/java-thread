# 原子性

# 原子类

Java SE5中引入了诸如AtomicInteger AtomicLong AtomicReference等特殊的原子性变量类，它们提供下面形式的原子性条件更新操作：
```java
boolean compareAndSet(expectedValue, updateValue);
```
