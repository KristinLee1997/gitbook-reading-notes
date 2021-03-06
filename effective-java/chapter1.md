# Chapter1

## 第1条:考虑用静态工厂方法代替构造器

注意:这里的静态工厂方法并不是与设计模式中的静态工厂方法对应

**静态工厂方法优点:**

1. 静态工厂方法有名称,例如判断是否为素数:BigInteger.probablePrime比    BigInteger\(int,int,Random\)更明确方法的目的.   
2. 不必再每次调用时都创建一个新对象.对于实例受控的类,静态工厂方法可以将构建好的实例缓存起来重复利用,避免创建不必要的对象.例如 Boolean.valueOf\(boolean\)就使用了这个方法.
3. 可以返回原返回类型的任何子类型对象例如 Book通过price判断分为ExpensiveBook和cheapBook.如果使用工厂方法,传入price就可返回对应的子对象.如果传入构造器,不加业务逻辑的情况下只会返回父类.
4. 在创建参数化类型实例的对象时,可以是代码变得等简洁

**静态工厂方法缺点**

1. 类如果不含有公有的或者受保护的构造器,就不能被子类化.
2. 它们与其他的静态方法实际上没有任何不同.

## 第2条 遇到多个构造器参数时要考虑用构造器

遇到大量可选参数时:

1. 使用重叠构造器,参数少的构造器调用参数多的构造器.\(构造器中存在好多不想设置的参数\)
2. 使用JavaBean,\(当调用bean和设置bean并发时,导致构造过程处于不一致状态\).
3. 使用Builder模式\(不足:为了创建对象必须创建构造器\)

   总结:当遇到多个可选参数时,使用builder模式是个不错的选择

## 第3条 用私有构造器或者枚举类型强化Singleton属性

实现Singleton的方法:

1. 使用私有构造器
2. 使用静态工厂方法
3. 使用enum类

## 第4条 通过私有构造器强化不可实例化的能力

通过加强私有构造器达到类不可实例化的

## 第5条 避免创建不必要的对象

当你重用现有对象时,不要创建新的对象,这样消耗性能的 

```text
public void getSum(){
    Long sum = 0;
    for (long i = 0; i < Integer.MAX_VALUE; i++){
        sum += i;
    }
}
```

因为sum定义为了Long而不是long,所以每次调用getSum\(\)时都会多创建大约2^31个多余的Long实例,导致getSum\(\)运行变慢.可以维护自己的对象池,但是注意一定要是重量级的才可以放到对象池,例如数据库连接池,不要将对象池搞得太臃肿

## 第6条 消除过期的对象引用

过期引用是指永远不会被解除的引用,消除过期的对象引用可以防止内存泄漏 

```text
public class Stack{ 
    private Object[] elements; 
    private int size = 0; 
    private static final int DEFAULT_INITIAL_CAPACITY = 16;

    public Stack(){
        elements = new Object[DEFAULT_INITIAL_CAPACITY];
    }

    public void push(Object e){
        ensureCapacity();
        elements[size++] = e;
    }
    
    public Object pop(){
        if(size = 0){
            throw new EmptyStackException();
        }
        return elements[--size];  // 这里会发生内存泄漏,改进方法如下
        /*
        Object result = elements[--size];
        elements[size] = null;
        return result;
        */
    }
    
    private void ensureCapacity(){
        if(elements.length = size){
            elements = Arrays.copyOf(elements, 2 * size + 1);
        }
    }
}
```

内存泄露的一个常见来源就是缓存,如果只要在缓存之外存在对某个项的键的引用,该项就有意义,那么就可以用WeakHashMap代表缓存,当缓存中的项过期之后,它们就会自动被删除

## 第7条 避免使用finalize\(\)

这一条不是很懂... 使用finalize\(\)是记得调用super.finalize\(\),防止父类永远无法调用finalize\(\)

