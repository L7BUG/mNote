# 1. ArrayList 简介

---

`ArrayList`的底层是`Object[ ]` 相当与动态数组，长度会动态自增。*在添加大量元素前，应使用`ensureCapacity`来手动增加长度*

```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable{
}
```


- `RandomAccess` 是一个标志接口，表明实现这个这个接口的 List 集合是支持**快速随机访问**的。在 `ArrayList` 中，我们即可以通过元素的序号快速获取元素对象，这就是快速随机访问。
- `ArrayList` 实现了 **`Cloneable` 接口** ，即覆盖了函数`clone()`，能被克隆。
- `ArrayList` 实现了 `java.io.Serializable `接口，这意味着`ArrayList`支持序列化，能通过序列化去传输。

# 2. ArrayList扩容机制

## 2.1. 构造函数

- `ArrayList()`
无参构造默认为空 只有在第一次添加数据的时候初始化一个大小为10的空间
`private static final int DEFAULT_CAPACITY = 10;`

```java
private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
public ArrayList() {
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}
```

- `ArrayList(int initialCapacity)`

  自己指定容量

```java
public ArrayList(int initialCapacity) {
    if (initialCapacity > 0) {
        this.elementData = new Object[initialCapacity];
    } else if (initialCapacity == 0) {
        this.elementData = EMPTY_ELEMENTDATA;
    } else {
        throw new IllegalArgumentException("Illegal Capacity: " + initialCapacity);
    }
}
```

- `ArrayList(Collection<? extends E> c)`

  利用集合的迭代器返回给本集合

```java
public ArrayList(Collection<? extends E> c) {
    Object[] a = c.toArray();
    if ((size = a.length) != 0) {
        if (c.getClass() == ArrayList.class) {
            elementData = a;
        } else {
            elementData = Arrays.copyOf(a, size, Object[].class);
        }
    } else {
        // replace with empty array.
        elementData = EMPTY_ELEMENTDATA;
    }
}
```

## 2.2. 扩容机制

- [`add()`](#add)
- [`ensureCapacityInternal()`](#ensureCapacityInternal())
- [`ensureExplicitCapacity()`](#ensureExplicitCapacity())
- [`grow()`](#grow())
- [`hugeCapacity()`](#hugeCapacity())
- [`ensureCapacity()`](#ensureCapacity())

### **`add()`**

```java
public boolean add(E e) {
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    elementData[size++] = e;
    return true;
}
```

使用`System.arraycopy(elementData, index, elementData, index + 1, size - index);`实现自己复制自己，也就是往后挪了一位

```java
public void add(int index, E element) {
    rangeCheckForAdd(index);

    ensureCapacityInternal(size + 1);  // Increments modCount!!
    System.arraycopy(elementData, index, elementData, index + 1,
                     size - index);
    elementData[index] = element;
    size++;
}
```



### **`ensureCapacityInternal()`**

`add`之前，会调用该方法，用于得到最小扩容量

`calculateCapacity` 该方法会在第一次add的时候给他分配10

```java
private void ensureCapacityInternal(int minCapacity) {
    ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
}
private static int calculateCapacity(Object[] elementData, int minCapacity) {
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
        return Math.max(DEFAULT_CAPACITY, minCapacity);
    }
    return minCapacity;
}
```

### `ensureExplicitCapacity()`

调用`ensureCapacityInternal`后一定会执行这个方法，用于判断是否需要扩容

`minCapacity`最小所需空间

```java
private void ensureExplicitCapacity(int minCapacity) {
    modCount++;

    // overflow-conscious code
    if (minCapacity - elementData.length > 0)
        grow(minCapacity);
}
```

### `	grow()`

扩容方法

默认扩容1.5倍`newCapacity = oldCapacity + (oldCapacity >> 1);`

如果1.5倍还是小于最小所需容量，他会直接扩容到最所需容量

最后判断要扩容的是否比`MAX_ARRAY_SIZE`大，新容量会等于`Integer.MAX_VALUE`

然后利用`Arrays.copyOf`扩容

```java
private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;
private void grow(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    int newCapacity = oldCapacity + (oldCapacity >> 1);//往右移了一位相当于 / 2
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}
```

### `hugeCapacity()`

从上面的`grow()`可以知道， 如果`newCapacity`大于`MAX_ARRAY_SIZE`会进入该方法

```java
private static int hugeCapacity(int minCapacity) {
    if (minCapacity < 0) // overflow
        throw new OutOfMemoryError();
    return (minCapacity > MAX_ARRAY_SIZE) ?
        Integer.MAX_VALUE :
    MAX_ARRAY_SIZE;
}
```

### `ensureCapacity()`

用于给用户自己分配空间的方法，最好在add大量元素之前使用该方法减少重新分配的次数，

```java
public void ensureCapacity(int minCapacity) {
    int minExpand = (elementData != DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
        // any size if not default element table
        ? 0
        // larger than default for default empty table. It's already
        // supposed to be at default size.
        : DEFAULT_CAPACITY;

    if (minCapacity > minExpand) {
        ensureExplicitCapacity(minCapacity);
    }
}
```

