# Android-Learning-Documents

	一、Java基础

​	1.1、Java基础知识大纲
​	1.2、注解
​	1.3、序列化
​	1.4、内存区域
​	1.5、垃圾收集器与内存分配策略
​	1.6、字节输入输出流
​	1.7、Android虚拟机
​	1.8、容器类
​	1.9、LruCache源码解析
​	1.10、SparseArray源码解析
​	1.11、浅拷贝 VS 深拷贝
​	1.12、泛型
​	1.13、反射

	二、Android基础

​	2.1、Activity知识梳理
​	​	2.1.1、Activity生命周期
​	​	2.1.2、Activity栈
​	​	2.1.2、Activity状态保存和恢复
​	2.2、Fragment知识梳理
​	​	2.2.1、Fragment源码解析
​	​	2.2.2、Fragment状态保存和恢复
​	​	2.2.3、FragmentPagerAdapter和FragmentStatePagerAdapter解析
​	​	2.2.4、FragmentPagerAdapter和FragmentStatePagerAdapter的数据更新问题
​	2.3、RecyclerView知识梳理
​	​	2.3.1、综述
​	​	2.3.2、Adapter
​	​	2.3.3、LayoutManager
​	​	2.3.4、ItemDecoration
​	​	2.3.5、ItemTouchHelper
​	2.4、Loader知识梳理
​	​	2.4.1、LoaderManager初探
​	​	2.4.2、initLoader和restarLoader的区别
​	​	2.4.3、自定义Loader
​	2.5、Android异步任务知识梳理
​	​	2.5.1、AsyncTask解析
​	​	2.5.2、HanderThread解析
​	​	2.5.3、AsyncQueryHandler解析
​	2.6、Android数据存储知识梳理
​	​	2.6.1、SQliteOpenHelper源码解析
​	​	2.6.2、Android存储目录
​	​	2.6.3、SharedPreference源码解析
​	​	2.6.4、数据库升级操作的处理策略
​	2.7、状态栏
​	2.8、广播
​	2.9、Service
​	2.10、版本适配

	三、开源框架

​	3.1、Retrofit
​	​	3.1.1、流程分析
​	​	3.1.2、Retrofit动态代理内部实现
​	3.2、OkHttp
​	​	3.2.1、源码解析入门
​	​	3.2.2、源码解析之异步请求&线程调度
​	​	3.2.3、缓存基础
​	​	3.2.4、缓存源码解析
​	3.3、Glide
​	​	3.3.1、基本用法
​	​	3.3.2、自定义Target
​	​	3.3.3、自定义transform
​	​	3.3.4、自定义GlideModule
​	​	3.3.5、Glide源码解析之流程剖析

	四、算法

​	4.1、排序算法
​	4.2、字符串算法(一)
​	4.3、字符串算法(二)
​	4.4、数组(一)
​	4.5、数组(二)
​	4.6、数组(三)
​	4.7、数组(四)
​	4.8、二分查找及其变型
​	4.9、链表算法
​	4.10、二叉查找树
​	4.11、二叉树算法(一)
​	4.12、二叉树算法(二)
​	4.13、二叉树算法(三)
​	4.14、数字算法

	五、kotlin

​	5.1、kotlin基础
​	5.2、函数的定义与调用
​	5.3、类、对象和接口
​	5.4、数据类、类委托及object关键字
​	5.5、Lambda表达式和成员引用
​	5.6、kotlin可空性
​	5.7、kotlin的类型系统
​	5.8、运算符重载及其他约定
​	5.9、类委托属性
​	5.10、高阶函数：Lambda作为形参或返回值
​	5.11、内联函数
​	5.12、泛型类型参数
​	5.13、运行时的泛型

	六、多线程

​	6.1、并发编程的艺术
​	6.2、synchronized之基本使用
​	6.3、synchronized之锁优化
​	6.4、synchronized之等待/通知模型
​	6.5、Executor
​	6.6、ThreadPoolExecutor
​	6.7、ConcurrentHashMap实现原理
​	6.8、volatile关键字
​	6.9、Thread Local
​	6.10、死锁
​	6.11、队列同步器实现原理&应用
​	6.12、ReentrantLock解析
​	6.13、ReentrantReadWriteLock原理

	七、插件化

​	7.1、Small框架之如何引入应用插件
​	7.2、Small框架之如何让引入公共库插件
​	7.3、Small框架之宿主分身
​	7.4、Small框架之如何实现插件更新
​	7.5、Small框架之如何不将插件打包到宿主程序中
​	7.6、Small源码分析之Hook原理
​	7.7、类的动态加载
​	7.8、类的动态加载源码入门
​	7.9、类的动态加载实例及源码分析
​	7.10、Service插件化实现及原理

	八、NDK

​	8.1、使用CMake进行NDK开发(一)
​	8.2、使用CMake进行NDK开发并编写CMakeLists.txt脚本

	九、Material Design控件

​	9.1、Android Design Support Library
​	9.2、AppBarLayout & Collapsing ToolbarLayout
​	9.3、BottomSheet & BottomSheetDialog & BottomSheetDialogFragment
​	9.4、FloatingActionButton
​	9.5、DrawerLayout & NavigationView
​	9.6、Snackbar
​	9.7、BottomNavigationBar
​	9.8、TabLayout
​	9.9、TextInputLayout

	十、性能优化

​	10.1、性能优化工具
​	​	10.1.1、TraceView
​	​	10.1.2、Systrace
​	​	10.1.3、调试GPU过度绘制&GPU呈现模式分析
​	​	10.1.4、Hierarchy Viewer
​	​	10.1.5、MAT
​	​	10.1.6、Memory Monitor & Heap Viewer & Allocation Tracker
​	​	10.1.7、LeakCanary
​	​	10.1.8、Lint
​	10.2、性能优化技巧
​	​	10.2.1、布局优化
​	​	10.2.2、内存优化
​	​	10.2.3、列表卡顿排查

	十一、设计模式

​	11.1、适配器模式
​	11.2、桥接模式
​	11.3、组合模式
​	11.4、装饰模式
​	11.5、外观模式
​	11.6、享元模式
​	11.7、代理模式

	十二、组件化

​	12.1、Arouter的基本使用
​	12.2、Arouter源码分析之Complier SDK
​	12.3、Arouter源码分析之运行时SDK

	十三、View

​	13.1、View绘制体系
​	​	13.1.1、LayoutInflater#inflate源码解析
​	​	13.1.2、setContentView源码解析
​	​	13.1.3、绘制流程之Measure解析
​	​	13.1.4、绘制流程之Layout解析
​	​	13.1.5、绘制流程之Draw解析
​	​	13.1.6、绘制流程之requestLayout和invalidate详解
​	​	13.1.7、getMeasureWidth和getWidth的区别
​	13.2、事件传递
​	​	13.2.1、事件分发机制
​	​	13.2.2、嵌套滑动的实现原理
​	13.3、Cancas&Paint
​	​	13.3.1、Canvas基础
​	​	13.3.2、Canvas的保存和恢复
​	​	13.3.3、颜色合成 Paint#setColorFilter
​	​	13.3.4、图像合成 Paint#setXfermode
​	​	13.3.5、Paint#setShader
​	​	13.3.6、绘制路线Path基本用法
​	13.4、动画
​	​	13.4.1、转场动画ContentTransition理论
​	​	13.4.1、转场动画ContentTransition实践

	十四、图片

​	14.1、图片基础知识
​	​	14.1.1、ImageView的ScaleType属性解析
​	​	14.1.2、Bitmap占用内存分析
​	​	14.1.3、Bitmap&BitmapFactory解析
​	14.2、图片压缩
​	​	14.2.1、PNG原理
​	​	14.2.2、减小PNG大小
​	​	14.2.3、VectorDrawable简介
​	​	14.2.4、VectorDeawable及AnimatedVectorDrawable使用详解
​	​	14.2.5、webp使用详解
​	​	14.2.6、选择合适的图片格式

	十五、Gradle

​	15.1、Gradle使用配置总结