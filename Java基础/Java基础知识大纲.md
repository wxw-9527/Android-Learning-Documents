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

    假如我们只重写了`equals`方法而没有重写`hashCode`方法，就会导致逻辑上相等的两个`key`，放在了容器中不同的为之