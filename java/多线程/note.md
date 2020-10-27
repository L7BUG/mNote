# 多线程
## 几种方式
1. 继承Thread类
2. 实现Runnable接口（常用）
3. 实现Callable接口
    1. 实现Callable接口
    2. 重写call方法
    3. `Executors.newFixedThreadPool` 开启线程池
    4. 用线程池对象的`submit(Callable callable  )`方法 获取`Future<V>` 对象
    5. 调用 `Future` 对象的get方法
    6. 关闭线程池