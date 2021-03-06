#### 一、面向对象

##### 1.1、多态

​	面向对象编程的三大特性：封装、继承、多态

 - 封装：隐藏类的内部实现。
 - 继承：子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
 - 多态：同一个行为具有多个不同表现形式或形态的能力。
    - 多态的好处
       - 可替换性：多态对已存在的代码具有可替换性。
       - 可扩充性：多态对代码具有可扩充性。新增加的子类不影响已存在类的多态性、继承性，以及其他特性的运行和操作。
       - 接口性：多态是超类通过方法签名，向子类提供了一个共同接口，由子类来完善或者覆盖它而实现的。
       - 灵活性：在应用中体现了灵活多样的操作，提高了使用效率。
       - 简化行：多态简化对应用软件代码的编写和修改过程，尤其在处理大量对象的运算和操作时，这个特点尤为突出和重要。
   - 多态的三个必要条件
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

##### 2.3、String
 - new String与直接赋值的区别

    - `String str1 = "ABCD"`，可能创建一个或不创建对象，如果`ABCD`这个字符串在常量池中已经存在，那么`str1`直接指向这个常量池中的对象。

    - `String str2 = new String("ABCD")`，最多创建两个`String`对象，至少创建一个对象。一定会在堆中创建一个`str2`对象，`value`是`ABCD`，如果`ABCD`这个字符串在常量池中不存在，会在池中创建一个对象。

      ![20180306210631112](https://img-blog.csdn.net/20180306210631112?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZHJlYW16dW9yYQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
      
    - 例1：

      ```java
      String s = "a" + "b" + "c" + "d";
      ```

      只创建了一个对象，在编译器编译时优化后，相当于直接定义了一个`abcd`字符串。

    - 例2：

      ```java
      String ab = "ab";
      String cd = "cd";
      String abcd = ab + cd;
      String s = "abcd";
      ```

      `ab`和`cd`存储的是两个常量池中的对象，当执行`ab+cd`时，首先会在堆中创建一个`StringBuilder`类，同时用`ab`指向的字符串对象完成初始化，然后调用`append`方法完成对`cd`指向的字符串的合并操作，接着调用`StringBuilder`的`toString`方法在堆中创建一个`String`对象，最后将刚生成的`String`对象的地址存放在局部变量`abcd`中。

- String、StringBuilder、StringBuffer的区别

    - `String`是`final`类，不能被继承。对于已经存在的`String`对象，修改它的值，就是重新创建一个对象。
    - `StringBuffer`是一个类似于`String`的字符串缓冲区，使用`append()`方法修改`StringBuffer`的值，使用`toString()`方法转换为字符串，是线程安全的。
    - `StringBuilder`用来代替`StringBuffer`，`StringBuilder`是非线程安全的，但速度更快。

- String为什么要设计成不可变类

    不仅可变性可以保证线程安全以及字符串常量池的实现。

    `String`用`final`修饰，不可继承，`String`本质上是个`final`的`char[]`数组，所以`charp[]`数组的内存地址不会被修改，而且`String`也没有对外暴露修改`char[]`数组的方法。

- 如何实现不可变

    - 将类声明为`final`
    - 将所有成员声明为私有的
    - 对变量不提供`set`方法
    - 将所有可变成员声明为`final`，只能对它们赋值一次
    - 通过构造器初始化所有成员，进行深拷贝`deep copy`
    - `getter`方法中，不要直接返回对象本身，而是克隆对象，并返回对象的拷贝

#### 三、关键字

##### 3.1、final

- `final`可以声明成员变量、方法、类及本地变量
- `final`成员变量必须在声明的时候初始化或者在构造器中初始化，否则就会报编译错误
- `final`变量是只读的
- `final`申明的方法不可以被子类的方法重写
- `final`类通常功能是完整的，不能被继承
- `final`变量可以安全的在多线程环境下进行共享，而不需要额外的同步开销
- `final`关键字提高了性能，`JVM`和`Java`应用都会缓存`final`变量，会对方法、变量及类进行优化
- 方法内部类访问方法中的局部变量，必须用`final`修饰才能访问

##### 3.2、static

- 静态变量

  - 又称为类变量，也就是说这个变量属于类，类所有的实例都共享静态变量，可以直接通过类型访问。静态变量在内存中只存在一份。

  - 实例变量：每创建一个实例就会产生一个实例变量，它与该实例同生共死

    ```java
    public class A {
        private int x; // 实例变量
        private static int y; // 静态变量
    
        public static void main(String[] args) {
            A a = new A();
            int x = a.x;
            int y = A.y;
        }
    }
    ```

- 静态方法

  静态方法在类加载的时候就存在了，它不依赖于任何实例。所以静态方法必须有实现，也就是说它不能是抽象方法。

  ```java
  public abstract class A {
      public static void func1() {
          
      }
      // public abstract static void func2(); // Illegal combination of modifiers:'abstract' and 'static'
  }
  ```

  只能访问所属类的静态字段和静态方法，方法中不能有`this`和`super`关键字，因为这两个关键字与具体对象关联。

  ```java
  public class A {
  
      private static int x;
      private int y;
  
      public static void func1() {
          int a = x;
          int b = y; // Non-static field 'y' cannot be referenced from a static context
          int b = this.y; // 'A.this' cannot be referenced from a static context
      }
  }
  ```

- 静态语句块

  静态语句块在类初始化时运行一次

  ```java
  public class A {
      
      static {
          System.out.println("123");
      }
  
      public static void main(String[] args) {
          A a1 = new A();
          A a2 = new A();
      }
  } 
  
  123
  ```

- 静态内部类

  非静态内部类依赖于外部类的实例，也就是说需要先创建外部类实例，才能用这个实例去创建非静态内部类。

  而静态内部类不需要。

  ```java
  public class OuterClass {
  
      class InnerClass {}
  
      static class StaticInnerClass { }
  
      public static void main(String[] args) {
      	// InnerClass innerClass = new InnerClass(); // 'OuterClass.this' cannot be referenced from a static context
          OuterClass outerClass = new OuterClass();
          InnerClass innerClass = outerClass.new InnerClass();
          StaticInnerClass staticInnerClass = new StaticInnerClass();
      }
  }
  ```

  静态内部类不能访问外部类的非静态变量和方法。

- 静态导包

  在使用静态变量和方法是不用再指明`ClassName`，从而简化代码，但可读性大大降低。

  ``` java
  import static com.xxx.ClassName.*
  ```

- 初始化顺序

  静态变量和静态语句块优先于实例变量和普通语句块，静态变量和静态语句块的初始化顺序取决于它们在代码中的顺序。

  ```java
  public static String staticField = "静态变量";
      
  static {
      System.out.println("静态语句块");
  }
  
  public String field = "实例变量";
      
  {
      System.out.peintln("普通语句块");
  }
  ```

  最后才是构造函数的初始化。

  ```java
  public InitialOrderTest() {
      System.out.println("构造函数");
  }
  ```

  存在继承的情况下，初始化顺序为

  - 父类（静态变量、静态语句块）
  - 子类（静态变量、静态语句块）
  - 父类（实例变量、普通语句块）
  - 父类（构造函数）
  - 子类（实例变量、普通语句块）
  - 子类（构造方法）

#### 四、内部类

在一个外部类的内部再定义一个类。

- 非静态内部类无法在外部类的静态方法中实例化。
- 非静态内部类的方法可以直接访问外部类的所有数据，包括私有的数据。
- 在静态内部类中调用外部类成员，成员也要用`static`修饰。
- 创建静态内部类的对象可以直接通过外部类调用静态内部类的构造器；创建非静态内部类的对象必须先创建外部类的对象，通过外部类的对象调用内部类的构造器。

##### 4.1、匿名内部类

- 匿名内部类不能定义任何静态成员、方法。
- 匿名内部类中的方法不能时抽象的。
- 匿名内部类必须实现接口或抽象父类所有的抽象方法。
- 匿名内部类不能定义构造器。
- 匿名内部类访问外部类成员变量或成员方法必须用`final`修饰。

##### 4.2、成员内部类

​	作为外部类的成员，可以直接使用外部类的所有成员和方法。

##### 4.3、局部内部类

​	定义在方法和作用域内。

##### 4.4、静态内部类

​	声明为`static`的内部类。

#### 五、抽象类&接口

- 抽象类和接口都不能直接实例化，如果要实例化，抽象类变量必须指向实现所有抽象方法的子类对象，接口变量必须指向实现所有接口方法的类对象。
- 抽象类要被子类继承，接口要被类实现。
- 接口里定义的便李总只能是公共的静态常量，抽象类中的变量可以是普通变量。
- 抽象类里可以没有抽象方法
- 接口可以被类多实现（被其他接口多继承），抽象类只能被单继承
- 接口中没有`this`指针，没有构造函数，不能拥有实例字段（实例变量）或实例方法
- 抽象类不能在`Java8`的`lambda`表达式中使用