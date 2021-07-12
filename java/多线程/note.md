## 线程组

> 每个Thread必然存在于一个`ThreadGroup`中
>
> 如果在new Thread时没有显式指定，那么默认将父线程（当前执行new Thread的线程）线程组设置为自己的线程组。