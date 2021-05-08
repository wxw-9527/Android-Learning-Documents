#### 一、面向对象

##### 1.1、多态

​	面向对象编程的三大特性：封装、继承、多态

 - 封装：隐藏类的内部实现。
 - 继承：子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
 - 多态：同一个行为具有多个不同表现形式或形态的能力。
    - 多态存在的三个必要条件
       - 继承
       - 重写
       - 向上转型：父类引用指向子类对象，该引用具备调用子类方法的能力。  `Perent p = new Child()`
   - 实现形式
     - 基于继承实现的多态
     - 基于接口实现的多态
   - 父类的静态方法不能被子类重写。当子类中含有和父类签名相同的静态方法时，一般称之为隐藏。

#### 二、Object

##### 2.1、Java中==、equals和hashCode的区别

 - ==

    - 基本数据类型：包括`byte`、`short`、`char`、`int`、`long`、`float`、`double`、`boolean`八种。对于基本数据类型，`==`比较的是它们的值。
    - 引用类型：比较的是它们在内存中的存放地址，即比较的是否是同一个对象。

- equals

  - `Object`中`equals`默认的实现是比较两个对象是不是`==`，即是否指向同一对象。

  - Java提供的某些类重写了equals方法，先判断类型是否一致，再判断内容是否一致。例：

    ```java
    public boolean equals(Object anObject) {
        if (this == anObject) { // 先判断引用是否相同(是否为同一对象)
            return true;
        }
        if (anObject instanceof String) { // 再判断类型是否一致
            String anotherString = (String)anObject;
            int n = length();
            if (n == anotherString.length()) { // 最后判断内容
                int i = 0;
                while (n-- != 0) {
                    if (charAt(i) != anotherString.charAt(i))
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
    ```

    **注意：当`equals`方法被复写时，`hashCode()`也要被复写。**

- hashCode

    `hashCode`用于在对象进行散列的时候作为`key`输入，保证散列的存取性能。`Object`的默认`hashCode`实现为在对象的内存地址上经过特定的算法计算出来的。

    由此可见，`equals`和`hashCode`没有什么关系。但是由于`HashSet/HashMap`容器的存在，又要保证：

    - `equals`相等的两个对象，其`hashCode`一定相等
    - `equals`不同的对象要尽量做到`hashCode`不同

    `HashMap`中，`value`的替换条件时判断`key`：

    ```java
    if (e.hash == hash // 1、hash值相同
        && ((k = e.key) == key || (key != null && key.equals(k)))) // key指向同一内存地址或key的equals方法返回true
    ```

    假如我们只重写了`equals`方法而没有重写`hashCode`方法，就会导致逻辑上相等的两个`key`，放在了容器中不同的位置。

##### 2.2、int & Integer

 - 存储原理

    - `int`属于基本数据类型，存储在栈中。
    - `Ingeger`属于符合数据类型，引用存储在栈中，引用所指向的对象存储在堆中。

- 缺省值

  - 0
  - null

- 泛型支持

  泛型支持`Integer`，不支持`int`

- int与Integer间的比较

  ```java
  int i1 = 128; // 基本数据类型
  Integer i2 = 128; // 非new出来的
  Integer i3 = new Integer(128); // new出来的
  ```

  - `i2`和`i3`不相等，`i2`指向存放它的常量池（数值位与`-128`到`127`之间）或者堆，后者指向堆中的另外一块内存。

  - 两个都是非`new`出来的`Integer`比较，如果在`-128`到`127`之间，返回`true`，否则返回`false`。因为`Java`在编译`Integer i2 = 128`的时候，会翻译成`Integer.valueOf(128)`，而`valueOf`函数会对`-128`到`127`之间的数进行缓存。

    ```java
    public static Integer valueOf(int i) {
        // low = -128
        // high = 127
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
    ```

  - 两个都是`new`出来的比较，返回`false`。

  - `int`与`Integer`比较，都为`true`，因为会把`Integer`自动拆箱成`int`再去比较。