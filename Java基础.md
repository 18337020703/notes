# Java基础知识总结

## 1.Java语法基础

### 关键字,保留字

> 关键字：其实就是某种语言赋予了特殊含义的单词。 
> 保留字：其实就是还没有赋予特殊含义，但是准备日后要使用过的单词。

### 标识符

> 其实就是在程序中自定义的名词。比如类名，变量名，函数名。包含 0-9、a-z、$、_ ； 
> 注意： 
>    1，数字不可以开头。 
>    2，不可以使用关键字。

### 常量

> 是在程序中的不会变化的数据。

### 变量

> 其实就是内存中的一个存储空间，用于存储常量数据。
>    作用：方便于运算。因为有些数据不确定。所以确定该数据的名词和存储空间。
>    特点：变量空间可以重复使用。

+ **什么时候定义变量？**只要是数据不确定的时候，就定义变量。
+ **变量空间的开辟需要什么要素呢？**
  
  1. 这个空间要存储什么数据？数据类型.
  2. 这个空间叫什么名字啊？变量名称.
3. 这个空间的第一次的数据是什么？ 变量的初始化值。

+ 变量的作用域和生存期

  + **变量的作用域**

    + 作用域从变量定义的位置开始，到该变量所在的那对大括号结束；

  + **生命周期**
    
    + 变量从定义的位置就开始在内存中存活了
    + 变量到达它所在的作用域的时候就在内存中消失了
    
  + **数据类型**
    
    + **基本数据类型**：`byte、short、int、long、float、double、char、boolean`
    + **引用数据类型**: 数组、类、接口。
    > **级别从低到高为：**byte,char,short(这三个平级)`–>int–>float–>long–>double`
    >
    > 自动类型转换：从低级别到高级别，系统自动转的；
    >
    > 强制类型转换：什么情况下使用?把一个高级别的数赋给一个别该数的级别低的变量；
  + **运算符号**
    
    + **算术运算符**
    
      > `+  - * / %` 
      > %:任何整数模2不是0就是1，所以只要改变被模数就可以实现开关运算。
      > +:连接符。 
      >
      > ++,–
  
    + **赋值运算符**  
    
      > =   +=   -=   *=   /=   %=
    + **比较运算符**
    
      > 特点：该运算符的特点是：运算完的结果，要么是true，要么是false。
    
    + **逻辑运算符**
    
      > `&  |  ^  !  &&  ||`
      >
      >   逻辑运算符除了 **!** 外都是用于连接两个`boolean`类型表达式。
      >
      >   **&**: 只有两边都为true结果是true。否则就是false。
      >
      >   **|**:只要两边都为false结果是false，否则就是true
      >
      >    **^**:异或：和或有点不一样。
      >     两边结果一样，就为false。
      >     两边结果不一样，就为true.
      >   **&** 和 **&&**区别： & ：无论左边结果是什么，右边都参与运算。
      >        &&：短路与，如果左边为false，那么右边不参数与运算。
      >   **|** 和**||** 区别：**|**：两边都运算。
      >        **||**：短路或，如果左边为true，那么右边不参与运算。
    
    + **位运算符**
    
      > **&  |  ^**
      > & << >> >>>(无符号右移)
    
      ```java
       int a  = 3,b = 5;-->b = 3,a = 5;
      
                  a = a + b; a = 8;
      
                  b = a - b; b = 3;
      
                  a = a - b; a = 5;
      
                  a = a ^ b;//
      
                  b = a ^ b;//b = a ^ b ^ b = a
      
                  a = a ^ b;//a = a ^ b ^ a = b;
      
              练习：高效的算出 2*8 = 2<<3;
      ```
    
      

### 语句

> **If    switch   do   while   while   for**

+ 这些语句什么时候用？

  1. 当判断固定个数的值的时候，可以使用if，也可以使用switch。但是建议使用switch，效率相对较高.

     > switch(变量){ 
     >    case 值:要执行的语句;break; 
     >    … 
     >   default:要执行的语句; 
     >   }
     >
     >   工作原理：用小括号中的变量的值依次和case后面的值进行对比，和哪个case后面的值相同了
     >   就执行哪个case后面的语句，如果没有相同的则执行default后面的语句；
     >
     >   细节：1.break是可以省略的，如果省略了就一直执行到遇到break为止；
     >      2.switch 后面的小括号中的变量应该是`byte,char,short,int`四种类型中的一种；
     >      3.default可以写在switch结构中的任意位置；如果将default语句放在了第一行，则不管expression与case中的value是否匹配，程序会从default开始执行直到第一个break出现。


  2.  当判断数据范围，获取判断运算结果`boolean`类型时，需要使用if。


  3. 当某些语句需要执行很多次时，就用循环结构。 while和for可以进行互换。
     区别在于：如果需要定义变量控制循环次数。建议使用for。因为for循环完毕，变量在内存中释放。

     > **break**:作用于switch ，和循环语句，用于跳出，或者称为结束。
     >
     > break语句单独存在时，下面不要定义其他语句，因为执行不到，编译会失败。当循环嵌套时，break只跳出当前所在循环。要跳出嵌套中的外部循环，只要给循环起名字即可，这个名字称之为标号。
     >
     > **continue**:只作用于循环结构，继续循环用的。
     >
     > 作用：结束本次循环，继续下次循环。该语句单独存在时，下面不可以定义语句，执行不到。

### 函数

  > 为了提高代码的复用性，可以将其定义成一个单独的功能，该功能的体现就是java中的函数。函数就是体现之一。

+ **java中的函数的定义格式**

  > 修饰符 返回值类型 函数名(参数类型 形式参数1，参数类型 形式参数1，…){
  >       执行语句；
  >      return 返回值；
  >   }没有具体的返回值时，返回的返回值类型用void关键字表示。
  >
  > 如果函数的返回值类型是void时，return语句可以省略不写的，系统会帮你自动加上。
  >
  > return的作用：结束函数。结束功能。
  
  + 如何定义一个函数
  
    函数其实就是一个功能，定义函数就是实现功能，通过两个明确来完成。
  
    1. 明确该功能的运算完的结果，其实是在明确这个函数的返回值类型。
    2. 在实现该功能的过程中是否有未知内容参与了运算，其实就是在明确这个函数的参数列表(参数类型&参数个数)
  
+ 函数的作用

  + 用于定义功能
  + 用于封装代码提高代码的复用性
  + 注意：函数中只能调用函数，不能定义函数。
  
+ 主函数

  + 保证该类的独立运行。
  
  + 因为它是程序的入口。
  
  + 因为它在被`jvm`调用。
  
    函数定义名称是为什么呐？
  
    1. 为了对该功能进行标示，方便于调用。
    2. 为了通过名称就可以明确函数的功能，为了增加代码的阅读性
  
+ 重载

  > 在一个类中，如果出现了两个或者两个以上的同名函数，只要它们的参数的个数，或者参数的类型不同，即可称之为该函数重载了。
  
  + 如何区分重载
  
    > 当函数同名时，只看参数列表。和返回值类型没关系。 

+ 数组

  > 用于存储同一类型数据的一个容器。好处：可以对该容器中的数据进行编号，从0开始。数组用于封装数据，就是一个具体的实体。

  + 如何在java中表现一个数组呢？两种表现形式。
    1. 元素类型[] 变量名 = new 元素类型[元素的个数]；
    2. 元素类型[] 变量名 = {元素1，元素2…}；
    3. 元素类型[] 变量名 = new 元素类型[]{元素1，元素2…}；

+ 内存

  > java分了5片内存。

  + 寄存器

  + 本地方法区

  + 方法区

  + 栈

    1. 存储的都是局部变量 ( 函数中定义的变量，函数上的参数，语句中的变量 )
    2. 只要数据运算完成所在的区域结束，该数据就会被释放。

  + 堆

    > 用于存储数组和对象，也就是实体。啥是实体啊？就是用于封装多个数据的。

    1. 每一个实体都有内存首地址值
    2. 堆内存中的变量都有默认初始化值。因为数据类型不同，值也不一样
    3. 垃圾回收机制

## 2.Java面向对象

+ **特点**

  1. 将复杂的事情简单化。
  2. 面向对象将以前的过程中的执行者，变成了指挥者。
  3. 面向对象这种思想是符合现在人们思考习惯的一种思想。
  4. 过程和对象在我们的程序中是如何体现的呢？过程其实就是函数；对象是将函数等一些内容进行了封装。
+ **匿名对象使用场景**

  1. 当对方法只进行一次调用的时候，可以使用匿名对象。
  2. 当对象对成员进行多次调用时，不能使用匿名对象。必须给对象起名字。
+ **在类中定义其实都称之为成员。成员有两种**

  1. 成员变量：其实对应的就是事物的属性。
  2. 成员函数：其实对应的就是事物的行为。
  3. 所以，其实定义类，就是在定义成员变量和成员函数。
  4. 但是在定义前，必须先要对事物进行属性和行为的分析，才可以用代码来体现。
+ **private**

  1. 私有的访问权限最低，只有在本类中的访问有效。
  2. 私有仅仅是封装的一种体现形式而已
  3. 私有的成员：其他类不能直接创建对象访问，
  4. 所以只有通过本类对外提供具体的访问方式来完成对私有的访问，可以通过对外提供函数的形式对其进行访问
  5. 好处：可以在函数中加入逻辑判断等操作，对数据进行判断等操作。
  6. 总结：开发时，记住，属性是用于存储数据的，直接被访问，容易出现安全隐患，
  7. 所以，类中的属性通常被私有化，并对外提供公共的访问方法。
  8. 这个方法一般有两个，规范写法：对于属性 xxx，可以使用`setXXX(),getXXX()`对其进行操作。
+ **成员变量和局部变量的区别**

  1. 成员变量直接定义在类中。局部变量定义在方法中，参数上，语句中。
  2. 成员变量在这个类中有效。局部变量只在自己所属的大括号内有效，大括号结束，局部变量失去作用域。
  3. 成员变量存在于堆内存中，随着对象的产生而存在，消失而消失。
  4. 局部变量存在于栈内存中，随着所属区域的运行而存在，结束而释放。
+ **类中怎么没有定义主函数呢？**

  1. 主函数的存在，仅为该类是否需要独立运行，如果不需要，主函数是不用定义的。
  2. 主函数的解释：保证所在类的独立运行，是程序的入口，被`jvm`调用。
+ **构造函数**

  1. 用于给对象进行初始化，是给与之对应的对象进行初始化，它具有针对性，函数中的一种。
2. 特点
  
   1. 该函数的名称和所在类的名称相同
   
   2. 不需要定义返回值类型
   
   3. 该函数没有具体的返回值
  
3. 注意事项：一个类在定义时，如果没有定义过构造函数，那么该类中会自动生成一个空参数的构造函数，为了方便该类创建对象，完成初始化。如果在类中自定义了构造函数，那么默认的构造函数就没有了。
  4. 一个类中，可以有多个构造函数，因为它们的函数名称都相同，所以只能通过参数列表来区分。所以，一个类中如果出现多个构造函数。它们的存在是以重载体现的。
+ **构造函数和一般函数有什么区别呢？**
  1. 两个函数定义格式不同。
  2. 构造函数是在对象创建时，就被调用，用于初始化，而且初始化动作只执行一次。
  3. 一般函数，是对象创建后，需要调用才执行，可以被调用多次。
  4. 分析事物时，发现具体事物一出现，就具备了一些特征，那就将这些特征定义到构造函数内。
+ **构造代码块和构造函数有什么区别？**
  1. 构造代码块：是给所有的对象进行初始化，也就是说，所有的对象都会调用一个代码块，只要对象一建立，就会调用这个代码块。
  2. 构造函数：是给与之对应的对象进行初始化，它具有针对性。
+ **创建一个对象都在内存中做了什么事情？**
  1. 先将硬盘上指定位置的`Person.class`文件加载进内存。
  2. 执行main方法时，在栈内存中开辟了main方法的空间(压栈-进栈)，然后在main方法的栈区分配了一个变量p。
  3. 在堆内存中开辟一个实体空间，分配了一个内存首地址值。new
  4. 在该实体空间中进行属性的空间分配，并进行了默认初始化。
  5. 对空间中的属性进行显示初始化。
  6. 进行实体的构造代码块初始化。
  7. 调用该实体对应的构造函数，进行构造函数初始化（）
  8. 将首地址赋值给p ，p变量就引用了该实体。(指向了该对象)

### 封装

+ 是指隐藏对象的属性和实现细节，仅对外提供公共访问方式。
+ 好处：将变化隔离；便于使用；提高重用性；安全性
+ 封装原则：将不需要对外提供的内容都隐藏起来，把属性都隐藏，提供公共方法对其访问。

### this

+ 代表对象，就是所在函数所属对象的引用。
+ this到底代表什么呢？哪个对象调用了this所在的函数，this就代表哪个对象，就是哪个对象的引用。
+ 在定义功能时，如果该功能内部使用到了调用该功能的对象，这时就用this来表示这个对象。
+ this 还可以用于构造函数间的调用
  1. 调用格式：this(实际参数)；
  2. this对象后面跟上 . 调用的是成员属性和成员方法(一般方法)；
  3. this对象后面跟上 () 调用的是本类中的对应参数的构造函数。
  4. 用this调用构造函数，必须定义在构造函数的第一行。因为构造函数是用于初始化的，所以初始化动作一定要执行。否则编译失败。

### static

+ **关键字**，是一个**修饰符**，用于修饰成员(成员变量和成员函数)。
+ **特点**
  
  1. 想要实现对象中的共性数据的对象共享，可以将这个数据进行静态修饰。
  2. 被静态修饰的成员，可以直接被类名所调用。也就是说，静态的成员多了一种调用方式。类名.静态方式。
3. 静态随着类的加载而加载，而且优先于对象存在

+ **弊端**
  
  1. 有些数据是对象特有的数据，是不可以被静态修饰的。因为那样的话，特有数据会变成对象的共享数据。这样对事物的描述就出了问题。所以，在定义静态时，必须要明确，这个数据是否是被对象所共享的。
  2. 静态方法只能访问静态成员，不可以访问非静态成员。因为静态方法加载时，优先于对象存在，所以没有办法访问对象中的成员。
  3. 静态方法中不能使用this，super关键字。因为this代表对象，而静态在时，有可能没有对象，所以this无法使用。
4. 主函数是静态的。

+ **定义成员时，到底需不需要被静态修饰呢？**

  + 成员分两种：

    1. **成员变量。（数据共享时静态化）**
    +  该成员变量的数据是否是所有对象都一样？
  
    +  如果是，那么该变量需要被静态修饰，因为是共享的数据。
    +  如果不是，那么就说这是对象的特有数据，要存储到对象中。

    2. **成员函数。（方法中没有调用特有数据时就定义成静态）**

    + 如果判断成员函数是否需要被静态修饰呢？

    + 只要参考，该函数内是否访问了对象中的特有数据：

    + 如果有访问特有数据，那方法不能被静态修饰。

    + 如果没有访问过特有数据，那么这个方法需要被静态修饰。
  
+ **成员变量和静态变量的区别**

    1. 成员变量所属于对象，所以也称为实例变量。静态变量所属于类，所以也称为类变量。
    2. 成员变量存在于堆内存中。静态变量存在于方法区中。
    3. 成员变量随着对象创建而存在，随着对象被回收而消失。静态变量随着类的加载而存在，随着类的消失而消失。
    4. 成员变量只能被对象所调用。静态变量可以被对象调用，也可以被类名调用。
    5. 所以，成员变量可以称为对象的特有数据，静态变量称为对象的共享数据

+ **静态的生命周期很长。**
+ **静态代码块：就是一个有静态关键字标示的一个代码块区域，定义在类中。**
  
  + 作用：可以完成类的初始化，静态代码块随着类的加载而执行，而且只执行一次（new 多个对象就只执行一次）。如果和主函数在同一类中，优先于主函数执行。

### 继承

+ 优点
  1. 提高了代码的复用性。
  2. 让类与类之间产生了关系，提供了另一个特征多态的前提。

+ 父类的由来：其实是由多个类不断向上抽取共性内容而来的。
+ java中对于继承，java只支持单继承。java虽然不直接支持多继承，但是保留了这种多继承机制，进行改良。
+ 单继承：一个类只能有一个父类。
+ 多继承：一个类可以有多个父类。
+ 为什么不支持多继承呢？
  1. 因为当一个类同时继承两个父类时，两个父类中有相同的功能，那么子类对象调用该功能时，运行哪一个呢？因为父类中的方法中存在方法体。
  2. 但是java支持多重继承。A继承B B继承C C继承D。
  3. 多重继承的出现，就有了继承体系。体系中的顶层父类是通过不断向上抽取而来的。它里面定义的该体系最基本最共性内容的功能。
  4. 所以，一个体系要想被使用，直接查阅该系统中的父类的功能即可知道该体系的基本用法。那么想要使用一个体系时，需要建立对象。建议建立最子类对象，因为最子类不仅可以使用父类中的功能。还可以使用子类特有的一些功能。
  5. 简单说：对于一个继承体系的使用，查阅顶层父类中的内容，创建最底层子类的对象。

+ **子父类出现后，类中的成员都有了哪些特点：**

  1. **成员变量**

     当子父类中出现一样的属性时，子类类型的对象，调用该属性，值是子类的属性值。

     如果想要调用父类中的属性值，需要使用一个关键字：super

     This：代表是本类类型的对象引用。

     Super ：代表是子类所属的父类中的内存空间引用。

     注意：子父类中通常是不会出现同名成员变量的，因为父类中只要定义了，子类就不用在定义了，直接继承过来用就可以了。

  2. **成员函数**

     当子父类中出现了一模一样的方法时，建立子类对象会运行子类中的方法。好像父类中的方法被覆盖掉一样。所以这种情况，是函数的另一个特性：覆盖(复写，重写)

     什么时候使用覆盖呢？当一个类的功能内容需要修改时，可以通过覆盖来实现。

  3. **构造函数**

     发现子类构造函数运行时，先运行了父类的构造函数。为什么呢?

     原因：子类的所有构造函数中的第一行，其实都有一条隐身的语句super();

     super(): 表示父类的构造函数，并会调用于参数相对应的父类中的构造函数。而super():是在调用父类中空参数的构造函数。

     为什么子类对象初始化时，都需要调用父类中的函数？(为什么要在子类构造函数的第一行加入这个super()?)

     因为子类继承父类，会继承到父类中的数据，所以必须要看父类是如何对自己的数据进行初始化的。所以子类在进行对象初始化时，先调用父类的构造函数，这就是子类的实例化过程。

     注意：子类中所有的构造函数都会默认访问父类中的空参数的构造函数，因为每一个子类构造内第一行都有默认的语句super();

     如果父类中没有空参数的构造函数，那么子类的构造函数内，必须通过super语句指定要访问的父类中的构造函数。

     如果子类构造函数中用this来指定调用子类自己的构造函数，那么被调用的构造函数也一样会访问父类中的构造函数。

  4. **super()和this()是否可以同时出现的构造函数中。**

     两个语句只能有一个定义在第一行，所以只能出现其中一个。

     super()或者this():为什么一定要定义在第一行？

     因为super()或者this()都是调用构造函数，构造函数用于初始化，所以初始化的动作要先完成。

+ **继承的细节**

  1. **什么时候使用继承呐？**

     当类与类之间存在着所属关系时，才具备了继承的前提。a是b中的一种。a继承b。狼是犬科中的一种。

     英文书中，所属关系：” is a “

     注意：不要仅仅为了获取其他类中的已有成员进行继承。

     所以判断所属关系，可以简单看，如果继承后，被继承的类中的功能，都可以被该子类所具备，那么继承成立。如果不是，不可以继承。

     

  2. **在方法覆盖时，注意两点**：
  
     1：子类覆盖父类时，必须要保证，子类方法的权限必须大于等于父类方法权限可以实现继承。否则，编译失败。
  
     2：覆盖时，要么都静态，要么都不静态。 (静态只能覆盖静态，或者被静态覆盖)
  
     继承的一个弊端：打破了封装性。对于一些类，或者类中功能，是需要被继承，或者复写的。
  
     这时如何解决问题呢？介绍一个关键字，final:最终。

    3. **final**
  
       1：这个关键字是一个修饰符，可以修饰类，方法，变量。
  
       2：被final修饰的类是一个最终类，不可以被继承。
  
       3：被final修饰的方法是一个最终方法，不可以被覆盖。
  
       4：被final修饰的变量是一个常量，只能赋值一次。
  
       其实这样的原因的就是给一些固定的数据起个阅读性较强的名称。 
       不加final修饰不是也可以使用吗？那么这个值是一个变量，是可以更改的。加了final，程序更为严谨。常量名称定义时，有规范，所有字母都大写，如果由多个单词组成，中间用 _ 连接。

### 抽象类

+ 抽象：不具体，看不明白。抽象类表象体现。
+ 在不断抽取过程中，将共性内容中的方法声明抽取，但是方法不一样，没有抽取，这时抽取到的方法，并不具体，需要被指定关键字abstract所标示，声明为抽象方法。
+ 抽象方法所在类一定要标示为抽象类，也就是说该类需要被abstract关键字所修饰。
+ 抽象类的特点
  1. 抽象方法只能定义在抽象类中，抽象类和抽象方法必须由abstract关键字修饰（可以描述类和方法，不可以描述变量）。
  2. 抽象方法只定义方法声明，并不定义方法实现。
  3. 抽象类不可以被创建对象(实例化)。
  4. 只有通过子类继承抽象类并覆盖了抽象类中的所有抽象方法后，该子类才可以实例化。否则，该子类还是一个抽象类。

+ 抽象类的细节
  1. 抽象类中是否有构造函数？有，用于给子类对象进行初始化。
  2. 抽象类中是否可以定义非抽象方法？
     + 可以。其实，抽象类和一般类没有太大的区别，都是在描述事物，只不过抽象类在描述事物时，有些功能不具体。
       所以抽象类和一般类在定义上，都是需要定义属性和行为的。
       只不过，比一般类多了一个抽象函数。而且比一般类少了一个创建对象的部分。
  3. ：抽象关键字abstract和哪些不可以共存？final , private , static
  4. 抽象类中可不可以不定义抽象方法？可以。抽象方法目的仅仅为了不让该类创建对象。

## 3.Java中的设计模式

> Java 中一般认为有23种设计模式，当然暂时不需要所有的都会，但是其中常见的几种设计模式应该去掌握。
> 总体来说设计模式分为三大类：
> 创建型模式，共五种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。
> 结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。
> 行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。

### 单例模式

> 所谓的单例设计指的是一个类只允许产生一个实例化对象。
> 最好理解的一种设计模式，分为懒汉式和饿汉式。

+ 懒汉式：当第一次去使用Singleton对象的时候才会为其产生实例化对象的操作

  ```java
  class Singleton {
  
      /**
       * 声明变量
       */
      private static volatile Singleton singleton = null;
  
      /**
       * 私有构造方法
       */
      private Singleton() {
  
      }
  
      /**
       * 提供对外方法
       * @return 
       */
      public static Singleton getInstance() {
          // 还未实例化
          if (singleton == null) {
       /*
        *当多个线程并发执行 getInstance 方法时，懒汉式会存在线程安全问题，所以用到了 synchronized 来实现线程       *的同步，当一个线程获得锁的时候其他线程就只能在外等待其执行完毕。而饿汉式则不存在线程安全的问题。
        */
              synchronized (Singleton.class) {
                  if (singleton == null) {
                      singleton = new Singleton();
                  }
              }
          }
          return singleton;
      }
      public void print() {
          System.out.println("Hello World");
      }
  }
  ```

  + 饿汉式：构造方法私有化，外部无法产生新的实例化对象，只能通过static方法取得实例化对象

  ```java
  class Singleton {
      /**
       * 在类的内部可以访问私有结构，所以可以在类的内部产生实例化对象
       */
      private static Singleton instance = new Singleton();
      /**
       * private 声明构造
       */
      private Singleton() {
  
      }
      /**
       * 返回对象实例
       */
      public static Singleton getInstance() {
          return instance;
      }
  
      public void print() {
          System.out.println("Hello Singleton...");
      }
  }
  ```
  
### 工厂设计模式

> 建立一个工厂类，对实现了同一接口的一些类进行实例的创建。

  

```java
interface Sender {
    void Send();
}

class MailSender implements Sender {

    @Override
    public void Send() {
        System.out.println("This is mail sender...");
    }
}

class SmsSender implements Sender {

    @Override
    public void Send() {
        System.out.println("This is sms sender...");
    }
}

public class FactoryPattern {
    public static void main(String[] args) {
        Sender sender = produce("mail");
        sender.Send();
    }
    public static Sender produce(String str) {
        if ("mail".equals(str)) {
            return new MailSender();
        } else if ("sms".equals(str)) {
            return new SmsSender();
        } else {
            System.out.println("输入错误...");
            return null;
        }
    }
}
```

### 多个工厂方法模式

> 该模式是对普通工厂方法模式的改进，在普通工厂方法模式中，如果传递的字符串出错，则不能正确创建对象，而多个工厂方法模式是提供多个工厂方法，分别创建对象。

```java
interface Sender {
    void Send();
}

class MailSender implements Sender {

    @Override
    public void Send() {
        System.out.println("This is mail sender...");
    }
}

class SmsSender implements Sender {

    @Override
    public void Send() {
        System.out.println("This is sms sender...");
    }
}

class SendFactory {
    public Sender produceMail() {
        return new MailSender();
    }

    public Sender produceSms() {
        return new SmsSender();
    }
}

public class FactoryPattern {
    public static void main(String[] args) {
        SendFactory factory = new SendFactory();
        Sender sender = factory.produceMail();
        sender.Send();
    }
}
```

### 静态工厂方法模式

> 将上面的多个工厂方法模式里的方法置为静态的，不需要创建实例，直接调用即可。

```java
interface Sender {
    void Send();
}

class MailSender implements Sender {

    @Override
    public void Send() {
        System.out.println("This is mail sender...");
    }
}

class SmsSender implements Sender {

    @Override
    public void Send() {
        System.out.println("This is sms sender...");
    }
}

class SendFactory {
    public static Sender produceMail() {
        return new MailSender();
    }

    public static Sender produceSms() {
        return new SmsSender();
    }
}

public class FactoryPattern {
    public static void main(String[] args) {
        Sender sender = SendFactory.produceMail();
        sender.Send();
    }
}
```

### 抽象工厂模式

> 工厂方法模式有一个问题就是，类的创建依赖工厂类，也就是说，如果想要扩展程序，必须对工厂类进行修改，这违背了闭包原则，所以，从设计角度考虑，有一定的问题，如何解决？
> 那么这就用到了抽象工厂模式，创建多个工厂类，这样一旦需要增加新的功能，直接增加新的工厂类就可以了，不需要修改之前的代码。

```java
interface Provider {
    Sender produce();
}

interface Sender {
    void Send();
}

class MailSender implements Sender {

    public void Send() {
        System.out.println("This is mail sender...");
    }
}

class SmsSender implements Sender {

    public void Send() {
        System.out.println("This is sms sender...");
    }
}

class SendMailFactory implements Provider {

    public Sender produce() {
        return new MailSender();
    }
}

class SendSmsFactory implements Provider {

    public Sender produce() {
        return new SmsSender();
    }
}


public class FactoryPattern {
    public static void main(String[] args) {
        Provider provider = new SendMailFactory();
        Sender sender = provider.produce();
        sender.Send();
    }
}
```

### 建造者模式

> 工厂类模式提供的是创建单个类的模式，而建造者模式则是将各种产品集中起来管理，用来创建复合对象，所谓复合对象就是指某个类具有不同的属性。

```java
import java.util.ArrayList;
import java.util.List;

abstract class Builder {
    /**
     * 第一步：装CPU
     */
   public abstract void buildCPU();

    /**
     * 第二步：装主板
     */
    public abstract void buildMainBoard();

    /**
     * 第三步：装硬盘
     */
    public abstract void buildHD();

    /**
     * 获得组装好的电脑
     * @return
     */
    public abstract Computer getComputer();
}

/**
 * 装机人员装机
 */
class Director {
    public void Construct(Builder builder) {
        builder.buildCPU();
        builder.buildMainBoard();
        builder.buildHD();
    }
}

/**
 * 具体的装机人员
 */
class ConcreteBuilder extends  Builder {

    Computer computer = new Computer();

    @Override
    public void buildCPU() {
        computer.Add("装CPU");
    }

    @Override
    public void buildMainBoard() {
        computer.Add("装主板");
    }

    @Override
    public void buildHD() {
        computer.Add("装硬盘");
    }

    @Override
    public Computer getComputer() {
        return computer;
    }
}

class Computer {

    /**
     * 电脑组件集合
     */
    private List<String> parts = new ArrayList<String>();

    public void Add(String part) {
        parts.add(part);
    }

    public void print() {
        for (int i = 0; i < parts.size(); i++) {
            System.out.println("组件:" + parts.get(i) + "装好了...");
        }
        System.out.println("电脑组装完毕...");
    }
}

public class BuilderPattern {

    public static void main(String[] args) {
        Director director = new Director();
        Builder builder = new ConcreteBuilder();
        director.Construct(builder);
        Computer computer = builder.getComputer();
        computer.print();
    }
}
```

### 适配器模式

> 适配器模式是将某个类的接口转换成客户端期望的另一个接口表示，目的是消除由于接口不匹配所造成的的类的兼容性问题。主要分三类：类的适配器模式、对象的适配器模式、接口的适配器模式。

+ ### 类的适配器模式

  ```java
  class Source {
      public void method1() {
          System.out.println("This is original method...");
      }
  }
  
  interface Targetable {
  
      /**
       * 与原类中的方法相同
       */
      public void method1();
  
      /**
       * 新类的方法
       */
      public void method2();
  }
  
  class Adapter extends Source implements Targetable {
  
      @Override
      public void method2() {
          System.out.println("This is the targetable method...");
      }
  }
  
  public class AdapterPattern {
      public static void main(String[] args) {
          Targetable targetable = new Adapter();
          targetable.method1();
          targetable.method2();
      }
  }
  ```

  

+ ### 对象的适配器模式

  > 基本思路和类的适配器模式相同，只是将Adapter 类作修改，这次不继承Source 类，而是持有Source 类的实例，以达到解决兼容性的问题。
  >

  ```java
  class Source {
      public void method1() {
          System.out.println("This is original method...");
      }
  }
  
  interface Targetable {
  
      /**
       * 与原类中的方法相同
       */
      public void method1();
  
      /**
       * 新类的方法
       */
      public void method2();
  }
  
  class Wrapper implements Targetable {
  
      private Source source;
  
      public Wrapper(Source source) {
          super();
          this.source = source;
      }
  
      @Override
      public void method1() {
          source.method1();
      }
  
      @Override
      public void method2() {
          System.out.println("This is the targetable method...");
      }
  }
  
  public class AdapterPattern {
      public static void main(String[] args) {
          Source source = new Source();
          Targetable targetable = new Wrapper(source);
          targetable.method1();
          targetable.method2();
      }
  }
  ```

+ ### 接口的适配器模式

  > 接口的适配器是这样的：有时我们写的一个接口中有多个抽象方法，当我们写该接口的实现类时，必须实现该接口的所有方法，这明显有时比较浪费，因为并不是所有的方法都是我们需要的，有时只需要某一些，此处为了解决这个问题，我们引入了接口的适配器模式，借助于一个抽象类，该抽象类实现了该接口，实现了所有的方法，而我们不和原始的接口打交道，只和该抽象类取得联系，所以我们写一个类，继承该抽象类，重写我们需要的方法就行。

  ```java
  /**
   * 定义端口接口，提供通信服务
 */
  interface Port {
      /**
       * 远程SSH端口为22
       */
      void SSH();
  
      /**
       * 网络端口为80
       */
      void NET();
  
      /**
       * Tomcat容器端口为8080
       */
      void Tomcat();
  
      /**
       * MySQL数据库端口为3306
       */
      void MySQL();
  }
  
  /**
   * 定义抽象类实现端口接口，但是什么事情都不做
   */
  abstract class Wrapper implements Port {
      @Override
      public void SSH() {
  
      }
  
      @Override
      public void NET() {
  
      }
  
      @Override
      public void Tomcat() {
  
      }
  
      @Override
      public void MySQL() {
  
      }
  }
  
  /**
   * 提供聊天服务
   * 需要网络功能
   */
  class Chat extends Wrapper {
      @Override
      public void NET() {
          System.out.println("Hello World...");
      }
  }
  
  /**
   * 网站服务器
   * 需要Tomcat容器，Mysql数据库，网络服务，远程服务
   */
  class Server extends Wrapper {
      @Override
      public void SSH() {
          System.out.println("Connect success...");
      }
  
      @Override
      public void NET() {
          System.out.println("WWW...");
      }
  
      @Override
      public void Tomcat() {
          System.out.println("Tomcat is running...");
      }
  
      @Override
      public void MySQL() {
          System.out.println("MySQL is running...");
      }
  }
  
  public class AdapterPattern {
  
      private static Port chatPort = new Chat();
      private static Port serverPort = new Server();
  
      public static void main(String[] args) {
          // 聊天服务
          chatPort.NET();
  
          // 服务器
          serverPort.SSH();
          serverPort.NET();
          serverPort.Tomcat();
          serverPort.MySQL();
      }
  }
  ```
  
  

### 装饰模式

> 顾名思义，装饰模式就是给一个对象增加一些新的功能，而且是动态的，要求装饰对象和被装饰对象实现同一个接口，装饰对象持有被装饰对象的实例。


  ```java
  interface Shape {
    void draw();
}

/**
 * 实现接口的实体类
 */
class Rectangle implements Shape {

    @Override
    public void draw() {
        System.out.println("Shape: Rectangle...");
    }
}

class Circle implements Shape {

    @Override
    public void draw() {
        System.out.println("Shape: Circle...");
    }
}

/**
 * 创建实现了 Shape 接口的抽象装饰类。
 */
abstract class ShapeDecorator implements Shape {
    protected Shape decoratedShape;

    public ShapeDecorator(Shape decoratedShape) {
        this.decoratedShape = decoratedShape;
    }

    @Override
    public void draw() {
        decoratedShape.draw();
    }
}

/**
 *  创建扩展自 ShapeDecorator 类的实体装饰类。
 */
class RedShapeDecorator extends ShapeDecorator {

    public RedShapeDecorator(Shape decoratedShape) {
        super(decoratedShape);
    }

    @Override
    public void draw() {
        decoratedShape.draw();
        setRedBorder(decoratedShape);
    }

    private void setRedBorder(Shape decoratedShape) {
        System.out.println("Border Color: Red");
    }
}

/**
 * 使用 RedShapeDecorator 来装饰 Shape 对象。
 */
public class DecoratorPattern {
    public static void main(String[] args) {
        Shape circle = new Circle();
        Shape redCircle = new RedShapeDecorator(new Circle());
        Shape redRectangle = new RedShapeDecorator(new Rectangle());
        System.out.println("Circle with normal border");
        circle.draw();

        System.out.println("\nCircle of red border");
        redCircle.draw();

        System.out.println("\nRectangle of red border");
        redRectangle.draw();
    }
}
  ```

  

### 策略模式

> 策略模式定义了一系列算法，并将每个算法封装起来，使他们可以相互替换，且算法的变化不会影响到使用算法的客户。需要设计一个接口，为一系列实现类提供统一的方法，多个实现类实现该接口，设计一个抽象类（可有可无，属于辅助类），提供辅助函数。策略模式的决定权在用户，系统本身提供不同算法的实现，新增或者删除算法，对各种算法做封装。因此，策略模式多用在算法决策系统中，外部用户只需要决定用哪个算法即可。

```java
/**
 * 抽象算法的策略类，定义所有支持的算法的公共接口
 */
abstract class Strategy {
    /**
     * 算法方法
     */
    public abstract void AlgorithmInterface();
}

/**
 * 具体算法A
 */
class ConcreteStrategyA extends Strategy {
    //算法A实现方法
    @Override
    public void AlgorithmInterface() {
        System.out.println("算法A的实现");
    }
}

/**
 * 具体算法B
 */
class ConcreteStrategyB extends Strategy {
    /**
     * 算法B实现方法
     */
    @Override
    public void AlgorithmInterface() {
        System.out.println("算法B的实现");
    }
}

/**
 * 具体算法C
 */
class ConcreteStrategyC extends Strategy {
    @Override
    public void AlgorithmInterface() {
        System.out.println("算法C的实现");
    }
}

/**
 * 上下文，维护一个对策略类对象的引用
 */
class Context {
    Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public void contextInterface(){
        strategy.AlgorithmInterface();
    }
}

/**
 * 客户端代码：实现不同的策略
 */
public class StrategyPattern {
    public static void main(String[] args) {

        Context context;

        context = new Context(new ConcreteStrategyA());
        context.contextInterface();

        context = new Context(new ConcreteStrategyB());
        context.contextInterface();

        context = new Context(new ConcreteStrategyC());
        context.contextInterface();
    }
}
```

### 代理模式

> 代理模式指给一个对象提供一个代理对象，并由代理对象控制对原对象的引用。代理可以分为静态代理和动态代理。
> 通过代理模式，可以利用代理对象为被代理对象添加额外的功能，以此来拓展被代理对象的功能。可以用于计算某个方法执行时间，在某个方法执行前后记录日志等操作。

#### 静态代理

> 静态代理需要我们写出代理类和被代理类，而且一个代理类和一个被代理类一一对应。代理类和被代理类需要实现同一个接口，通过聚合使得代理对象中有被代理对象的引用，以此实现代理对象控制被代理对象的目的。

```java
/**
 * 代理类和被代理类共同实现的接口
 */
interface IService {

    void service();
}


/**
 * 被代理类
 */
class Service implements IService{

    @Override
    public void service() {
        System.out.println("被代理对象执行相关操作");
    }
}

/**
 * 代理类
 */
class ProxyService implements IService{
    /**
     * 持有被代理对象的引用
     */
    private IService service;

    /**
     * 默认代理Service类
     */
    public ProxyService() {
        this.service = new Service();
    }

    /**
     * 也可以代理实现相同接口的其他类
     * @param service
     */
    public ProxyService(IService service) {
        this.service = service;
    }

    @Override
    public void service() {
        System.out.println("开始执行service()方法");
        service.service();
        System.out.println("service()方法执行完毕");
    }
}


//测试类
public class ProxyPattern {

    public static void main(String[] args) {
        IService service = new Service();
        //传入被代理类的对象
        ProxyService proxyService = new ProxyService(service);
        proxyService.service();
    }
}
```

#### 动态代理

> JDK 1.3 之后，Java通过java.lang.reflect包中的三个类Proxy、InvocationHandler、Method来支持动态代理。动态代理常用于有若干个被代理的对象，且为每个被代理对象添加的功能是相同的（例如在每个方法运行前后记录日志）。
>
> 动态代理的代理类不需要我们编写，由Java自动产生代理类源代码并进行编译最后生成代理对象。
> 创建动态代理对象的步骤：
> 1. 指明一系列的接口来创建一个代理对象
> 2. 创建一个调用处理器（InvocationHandler）对象
> 3. 将这个代理指定为某个其他对象的代理对象
> 4. 在调用处理器的invoke（）方法中采取代理，一方面将调用传递给真实对象，另一方面执行各种需要的操作

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

/**
 * 代理类和被代理类共同实现的接口
 */
interface IService {
    void service();
}

class Service implements IService{

    @Override
    public void service() {
        System.out.println("被代理对象执行相关操作");
    }
}

class ServiceInvocationHandler implements InvocationHandler {

    /**
     * 被代理的对象
     */
    private Object srcObject;

    public ServiceInvocationHandler(Object srcObject) {
        this.srcObject = srcObject;
    }

    @Override
    public Object invoke(Object proxyObj, Method method, Object[] args) throws Throwable {
        System.out.println("开始执行"+method.getName()+"方法");
        //执行原对象的相关操作，容易忘记
        Object returnObj = method.invoke(srcObject,args);
        System.out.println(method.getName()+"方法执行完毕");
        return returnObj;
    }
}

public class ProxyPattern {
    public static void main(String[] args) {
        IService service = new Service();
        Class<? extends IService> clazz = service.getClass();

        IService proxyService = (IService) Proxy.newProxyInstance(clazz.getClassLoader(),
                                        clazz.getInterfaces(), new ServiceInvocationHandler(service));
        proxyService.service();
    }
}
```

## 4.Java反射
### **Class的加载过程**

> ​     反射是框架设计的灵魂，使用的前提条件：必须先得到代表的字节码的Class，Class类用于表示.class的字节码文件
>
> JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。
> 要想解剖一个类,必须先要获取到该类的字节码文件对象。而解剖使用的就是Class类中的方法.所以先要获取到每一个字节码文件对应的Class类型的对象.
>
> 反射就是把java类中的各种成分映射成一个个的Java对象
> 例如：一个类有：成员变量、方法、构造方法、包等等信息，利用反射技术可以对一个类进行解剖，把个个组成部分映射成一个个对象。
>      （其实：一个类中这些成员方法、构造方法、在加入类中都有一个类来描述）
> 如图是类的正常加载过程：反射的原理在与class对象。
> 熟悉一下加载的时候：Class对象的由来是将class文件读入内存，并为之创建一个Class对象。

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-24_154917.png)

### Class类在java中的api详解（1.7的API）

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-24_185042.png)

+ Class 类的实例表示正在运行的 Java 应用程序中的类和接口。也就是`jvm`中有N多的实例每个类都有该Class对象。（包括基本数据类型）
+ Class 没有公共构造方法。Class 对象是在加载类时由 Java 虚拟机以及通过调用类加载器中的`defineClass` 方法自动构造的。也就是这不需要我们自己去处理创建，JVM已经帮我们创建好了。

+ 没有公共的构造方法，方法共有64个，具体去看api

### 反射的使用

#### 获取Class对象的三种方式

1. `Object.getClass() //返回一个对象的运行时类`
2. 任何数据类型(包括基本类型)都有一个静态的Class属性
3. 通过Class类的静态方法：`forName(String className)`

```java
//Student类 省略...

package fanshe;
/**
 * 获取Class对象的三种方式
 * 1 Object ——> getClass();
 * 2 任何数据类型（包括基本数据类型）都有一个“静态”的class属性
 * 3 通过Class类的静态方法：forName（String  className）(常用)
 *
 */
public class Fanshe {
	public static void main(String[] args) {
         Student stu1 = new Student();//这一new 产生一个Student对象，一个Class对象。
		
        //第一种方式获取Class对象  
		Class stuClass = stu1.getClass();//获取Class对象
		System.out.println(stuClass.getName());
		
		//第二种方式获取Class对象
		Class stuClass2 = Student.class;
		System.out.println(stuClass == stuClass2);//判断第一种方式获取的Class对象和第二种方式获取的是否是同一个
		
		//第三种方式获取Class对象
		try {
			Class stuClass3 = Class.forName("fanshe.Student");//注意此字符串必须是真实路径，就是带包名的类路径，包名.类名
			System.out.println(stuClass3 == stuClass2);//判断三种方式是否获取的是同一个Class对象
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
		
	}
}
```

**注意：**在运行期间，一个类，只有一个Class对象产生

+ **三种方式常用第三种**，第一种对象都有了还要反射干什么。第二种需要导入类的包，依赖太强，不导包就抛编译错误。一般都第三种，一个字符串可以传入也可写在配置文件中等多种方法

#### 通过反射获取构造方法并使用

+ student类

  ```java
  
  package fanshe;
   
  public class Student {
  	
  	//---------------构造方法-------------------
  	//（默认的构造方法）
  	Student(String str){
  		System.out.println("(默认)的构造方法 s = " + str);
  	}
  	
  	//无参构造方法
  	public Student(){
  		System.out.println("调用了公有、无参构造方法执行了。。。");
  	}
  	
  	//有一个参数的构造方法
  	public Student(char name){
  		System.out.println("姓名：" + name);
  	}
  	
  	//有多个参数的构造方法
  	public Student(String name ,int age){
  		System.out.println("姓名："+name+"年龄："+ age);//这的执行效率有问题，以后解决。
  	}
  	
  	//受保护的构造方法
  	protected Student(boolean n){
  		System.out.println("受保护的构造方法 n = " + n);
  	}
  	
  	//私有构造方法
  	private Student(int age){
  		System.out.println("私有的构造方法   年龄："+ age);
  	}
   
  }
  ```

+ 共有6个构造方法

  ```java
  package fanshe;
   
  import java.lang.reflect.Constructor;
   
   
  /*
   * 通过Class对象可以获取某个类中的：构造方法、成员变量、成员方法；并访问成员；
   * 
   * 1.获取构造方法：
   * 		1).批量的方法：
   * 			public Constructor[] getConstructors()：所有"公有的"构造方法
              public Constructor[] getDeclaredConstructors()：获取所有的构造方法(包括私有、受保护、默认、公有)
       
   * 		2).获取单个的方法，并调用：
   * 			public Constructor getConstructor(Class... parameterTypes):获取单个的"公有的"构造方法：
   * 			public Constructor getDeclaredConstructor(Class... parameterTypes):获取"某个构造方法"可以是私有的，或受保护、默认、公有；
   * 		
   * 			调用构造方法：
   * 			Constructor-->newInstance(Object... initargs)
   */
  public class Constructors {
   
  	public static void main(String[] args) throws Exception {
  		//1.加载Class对象
  		Class clazz = Class.forName("fanshe.Student");
  		
  		
  		//2.获取所有公有构造方法
  		System.out.println("**********************所有公有构造方法*********************************");
  		Constructor[] conArray = clazz.getConstructors();
  		for(Constructor c : conArray){
  			System.out.println(c);
  		}
  		
  		
  		System.out.println("************所有的构造方法(包括：私有、受保护、默认、公有)***************");
  		conArray = clazz.getDeclaredConstructors();
  		for(Constructor c : conArray){
  			System.out.println(c);
  		}
  		
  		System.out.println("*****************获取公有、无参的构造方法*******************************");
  		Constructor con = clazz.getConstructor(null);
  		//1>、因为是无参的构造方法所以类型是一个null,不写也可以：这里需要的是一个参数的类型，切记是类型
  		//2>、返回的是描述这个无参构造函数的类对象。
  	
  		System.out.println("con = " + con);
  		//调用构造方法
  		Object obj = con.newInstance();
  	//	System.out.println("obj = " + obj);
  	//	Student stu = (Student)obj;
  		
  		System.out.println("******************获取私有构造方法，并调用*******************************");
  		con = clazz.getDeclaredConstructor(char.class);
  		System.out.println(con);
  		//调用构造方法
  		con.setAccessible(true);//暴力访问(忽略掉访问修饰符)
  		obj = con.newInstance('男');
  	}
  	
  }
  ```

+ 后台输出

  ```properties
  **********************所有公有构造方法*********************************
  public fanshe.Student(java.lang.String,int)
  public fanshe.Student(char)
  public fanshe.Student()
  ************所有的构造方法(包括：私有、受保护、默认、公有)***************
  private fanshe.Student(int)
  protected fanshe.Student(boolean)
  public fanshe.Student(java.lang.String,int)
  public fanshe.Student(char)
  public fanshe.Student()
  fanshe.Student(java.lang.String)
  *****************获取公有、无参的构造方法*******************************
  con = public fanshe.Student()
  调用了公有、无参构造方法执行了。。。
  ******************获取私有构造方法，并调用*******************************
  public fanshe.Student(char)
  姓名：男
  ```

  

> 1.获取构造方法：
>   1).批量的方法：
> public Constructor[] getConstructors()：所有"公有的"构造方法
>             public Constructor[] getDeclaredConstructors()：获取所有的构造方法(包括私有、受保护、默认、公有)
>    
>   2).获取单个的方法，并调用：
> public Constructor getConstructor(Class... parameterTypes):获取单个的"公有的"构造方法：
> public Constructor getDeclaredConstructor(Class... parameterTypes):获取"某个构造方法"可以是私有的，或受保护、默认、公有；
>
>   调用构造方法：
> Constructor-->newInstance(Object... initargs)
>
> 2、newInstance是 Constructor类的方法（管理构造函数的类）
> api的解释为：
> newInstance(Object... initargs)
>            使用此 Constructor 对象表示的构造方法来创建该构造方法的声明类的新实例，并用指定的初始化参数初始化该实例。
> 它的返回值是T类型，所以`newInstance`是创建了一个构造方法的声明类的新实例对象。并为之调用

#### 获取成员变量并调用

+ student

  ```java
  package fanshe.field;
   
  public class Student {
  	public Student(){
  		
  	}
  	//**********字段*************//
  	public String name;
  	protected int age;
  	char sex;
  	private String phoneNum;
  	
  	@Override
  	public String toString() {
  		return "Student [name=" + name + ", age=" + age + ", sex=" + sex
  				+ ", phoneNum=" + phoneNum + "]";
  	}
  }
  ```

+ 测试类：

  ```java
  package fanshe.field;
  import java.lang.reflect.Field;
  /*
   * 获取成员变量并调用：
   * 
   * 1.批量的
   * 		1).Field[] getFields():获取所有的"公有字段"
   * 		2).Field[] getDeclaredFields():获取所有字段，包括：私有、受保护、默认、公有；
   * 2.获取单个的：
   * 		1).public Field getField(String fieldName):获取某个"公有的"字段；
   * 		2).public Field getDeclaredField(String fieldName):获取某个字段(可以是私有的)
   * 
   * 	 设置字段的值：
   * 		Field --> public void set(Object obj,Object value):
   * 					参数说明：
   * 					1.obj:要设置的字段所在的对象；
   * 					2.value:要为字段设置的值；
   * 
   */
  public class Fields {
   
  		public static void main(String[] args) throws Exception {
  			//1.获取Class对象
  			Class stuClass = Class.forName("fanshe.field.Student");
  			//2.获取字段
  			System.out.println("************获取所有公有的字段********************");
  			Field[] fieldArray = stuClass.getFields();
  			for(Field f : fieldArray){
  				System.out.println(f);
  			}
  			System.out.println("************获取所有的字段(包括私有、受保护、默认的)********************");
  			fieldArray = stuClass.getDeclaredFields();
  			for(Field f : fieldArray){
  				System.out.println(f);
  			}
  			System.out.println("*************获取公有字段**并调用***********************************");
  			Field f = stuClass.getField("name");
  			System.out.println(f);
  			//获取一个对象
  			Object obj = stuClass.getConstructor().newInstance();//产生Student对象--》Student stu = new Student();
  			//为字段设置值
  			f.set(obj, "刘德华");//为Student对象中的name属性赋值--》stu.name = "刘德华"
  			//验证
  			Student stu = (Student)obj;
  			System.out.println("验证姓名：" + stu.name);
  			
  			
  			System.out.println("**************获取私有字段****并调用********************************");
  			f = stuClass.getDeclaredField("phoneNum");
  			System.out.println(f);
  			f.setAccessible(true);//暴力反射，解除私有限定
  			f.set(obj, "18888889999");
  			System.out.println("验证电话：" + stu);
  			
  		}
  	}
  ```

+ 后台输出

  ```properties
  ************获取所有公有的字段********************
  public java.lang.String fanshe.field.Student.name
  ************获取所有的字段(包括私有、受保护、默认的)********************
  public java.lang.String fanshe.field.Student.name
  protected int fanshe.field.Student.age
  char fanshe.field.Student.sex
  private java.lang.String fanshe.field.Student.phoneNum
  *************获取公有字段**并调用***********************************
  public java.lang.String fanshe.field.Student.name
  验证姓名：刘德华
  **************获取私有字段****并调用********************************
  private java.lang.String fanshe.field.Student.phoneNum
  验证电话：Student [name=刘德华, age=0, sex=
  ```

  

> 由此可见
> 调用字段时：需要传递两个参数：
> Object obj = stuClass.getConstructor().newInstance();//产生Student对象--》Student stu = new Student();
> //为字段设置值
> f.set(obj, "刘德华");//为Student对象中的name属性赋值--》stu.name = "刘德华"
> 第一个参数：要传入设置的对象，第二个参数：要传入实参

#### 获取成员方法并调用

+ student类

  ```java
  package fanshe.method;
   
  public class Student {
  	//**************成员方法***************//
  	public void show1(String s){
  		System.out.println("调用了：公有的，String参数的show1(): s = " + s);
  	}
  	protected void show2(){
  		System.out.println("调用了：受保护的，无参的show2()");
  	}
  	void show3(){
  		System.out.println("调用了：默认的，无参的show3()");
  	}
  	private String show4(int age){
  		System.out.println("调用了，私有的，并且有返回值的，int参数的show4(): age = " + age);
  		return "abcd";
  	}
  }
  ```

  

+ 测试类

  ```java
  package fanshe.method;
   
  import java.lang.reflect.Method;
   
  /*
   * 获取成员方法并调用：
   * 
   * 1.批量的：
   * 		public Method[] getMethods():获取所有"公有方法"；（包含了父类的方法也包含Object类）
   * 		public Method[] getDeclaredMethods():获取所有的成员方法，包括私有的(不包括继承的)
   * 2.获取单个的：
   * 		public Method getMethod(String name,Class<?>... parameterTypes):
   * 					参数：
   * 						name : 方法名；
   * 						Class ... : 形参的Class类型对象
   * 		public Method getDeclaredMethod(String name,Class<?>... parameterTypes)
   * 
   * 	 调用方法：
   * 		Method --> public Object invoke(Object obj,Object... args):
   * 					参数说明：
   * 					obj : 要调用方法的对象；
   * 					args:调用方式时所传递的实参；
  ):
   */
  public class MethodClass {
   
  	public static void main(String[] args) throws Exception {
  		//1.获取Class对象
  		Class stuClass = Class.forName("fanshe.method.Student");
  		//2.获取所有公有方法
  		System.out.println("***************获取所有的”公有“方法*******************");
  		stuClass.getMethods();
  		Method[] methodArray = stuClass.getMethods();
  		for(Method m : methodArray){
  			System.out.println(m);
  		}
  		System.out.println("***************获取所有的方法，包括私有的*******************");
  		methodArray = stuClass.getDeclaredMethods();
  		for(Method m : methodArray){
  			System.out.println(m);
  		}
  		System.out.println("***************获取公有的show1()方法*******************");
  		Method m = stuClass.getMethod("show1", String.class);
  		System.out.println(m);
  		//实例化一个Student对象
  		Object obj = stuClass.getConstructor().newInstance();
  		m.invoke(obj, "刘德华");
  		
  		System.out.println("***************获取私有的show4()方法******************");
  		m = stuClass.getDeclaredMethod("show4", int.class);
  		System.out.println(m);
  		m.setAccessible(true);//解除私有限定
  		Object result = m.invoke(obj, 20);//需要两个参数，一个是要调用的对象（获取有反射），一个是实参
  		System.out.println("返回值：" + result);
  		
  		
  	}
  }
  ```

  

+ 控制台

  ```java
  ***************获取所有的”公有“方法*******************
  public void fanshe.method.Student.show1(java.lang.String)
  public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
  public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
  public final void java.lang.Object.wait() throws java.lang.InterruptedException
  public boolean java.lang.Object.equals(java.lang.Object)
  public java.lang.String java.lang.Object.toString()
  public native int java.lang.Object.hashCode()
  public final native java.lang.Class java.lang.Object.getClass()
  public final native void java.lang.Object.notify()
  public final native void java.lang.Object.notifyAll()
  ***************获取所有的方法，包括私有的*******************
  public void fanshe.method.Student.show1(java.lang.String)
  private java.lang.String fanshe.method.Student.show4(int)
  protected void fanshe.method.Student.show2()
  void fanshe.method.Student.show3()
  ***************获取公有的show1()方法*******************
  public void fanshe.method.Student.show1(java.lang.String)
  调用了：公有的，String参数的show1(): s = 刘德华
  ***************获取私有的show4()方法******************
  private java.lang.String fanshe.method.Student.show4(int)
  调用了，私有的，并且有返回值的，int参数的show4(): age = 20
  返回值：abcd
  ```

  

> 由此可见：
> `m = stuClass.getDeclaredMethod("show4", int.class)`;//调用制定方法（所有包括私有的），需要传入两个参数，第一个是调用的方法名称，第二个是方法的形参类型，切记是类型。
> `System.out.println(m);`
> `m.setAccessible(true);`//解除私有限定
> `Object result = m.invoke(obj, 20)`;//需要两个参数，一个是要调用的对象（获取有反射），一个是实参
> `System.out.println("返回值：" + result);//`

#### 反射main方法

+ student

  ```java
  
  package fanshe.main;
   
  public class Student {
   
  	public static void main(String[] args) {
  		System.out.println("main方法执行了。。。");
  	}
  }
  
  ```

  

+ 测试类：

  ```java
  package fanshe.main;
   
  import java.lang.reflect.Method;
   
  /**
   * 获取Student类的main方法、不要与当前的main方法搞混了
   */
  public class Main {
  	
  	public static void main(String[] args) {
  		try {
  			//1、获取Student对象的字节码
  			Class clazz = Class.forName("fanshe.main.Student");
  			
  			//2、获取main方法
  			 Method methodMain = clazz.getMethod("main", String[].class);//第一个参数：方法名称，第二个参数：方法形参的类型，
  			//3、调用main方法
  			// methodMain.invoke(null, new String[]{"a","b","c"});
  			 //第一个参数，对象类型，因为方法是static静态的，所以为null可以，第二个参数是String数组，这里要注意在jdk1.4时是数组，jdk1.5之后是可变参数
  			 //这里拆的时候将  new String[]{"a","b","c"} 拆成3个对象。。。所以需要将它强转。
  			 methodMain.invoke(null, (Object)new String[]{"a","b","c"});//方式一
  			// methodMain.invoke(null, new Object[]{new String[]{"a","b","c"}});//方式二
  			
  		} catch (Exception e) {
  			e.printStackTrace();
  		}
  		
  		
  	}
  }
  ```

  

#### 通过反射运行配置文件内容

+ student

  ```java
  
  public class Student {
  	public void show(){
  		System.out.println("is show()");
  	}
  }
  
  ```

  

+ 配置文件以txt文件为例子（pro.txt）

  ```
  className = cn.fanshe.Student
  methodName = show
  ```

  

+ 测试类

  ```java
  import java.io.FileNotFoundException;
  import java.io.FileReader;
  import java.io.IOException;
  import java.lang.reflect.Method;
  import java.util.Properties;
   
  /*
   * 我们利用反射和配置文件，可以使：应用程序更新时，对源码无需进行任何修改
   * 我们只需要将新类发送给客户端，并修改配置文件即可
   */
  public class Demo {
  	public static void main(String[] args) throws Exception {
  		//通过反射获取Class对象
  		Class stuClass = Class.forName(getValue("className"));//"cn.fanshe.Student"
  		//2获取show()方法
  		Method m = stuClass.getMethod(getValue("methodName"));//show
  		//3.调用show()方法
  		m.invoke(stuClass.getConstructor().newInstance());
  		
  	}
  	
  	//此方法接收一个key，在配置文件中获取相应的value
  	public static String getValue(String key) throws IOException{
  		Properties pro = new Properties();//获取配置文件的对象
  		FileReader in = new FileReader("pro.txt");//获取输入流
  		pro.load(in);//将流加载到配置文件对象中
  		in.close();
  		return pro.getProperty(key);//返回根据key获取的value值
  	}
  }
  
  //控制台输出：
  //is show()
  ```

  

+ 需求

  > 当我们升级这个系统时，不要Student类，而需要新写一个Student2的类时，这时只需要更改pro.txt的文件内容就可以了。代码就一点不用改动

+ 要替换的student2类

  ```java
  public class Student2 {
  	public void show2(){
  		System.out.println("is show2()");
  	}
  }
  ```

  

+ 配置文件更改为

  ```
  className = cn.fanshe.Student2
  methodName = show2
  ```

  

+ 控制台输出

  ```
  is show2();
  ```

  

#### 通过反射越过泛型检查

> 泛型用在编译期，编译过后泛型擦除（消失掉）。所以是可以通过反射越过泛型检查的

+ 测试类

  ```java
  
  import java.lang.reflect.Method;
  import java.util.ArrayList;
   
  /*
   * 通过反射越过泛型检查
   * 
   * 例如：有一个String泛型的集合，怎样能向这个集合中添加一个Integer类型的值？
   */
  public class Demo {
  	public static void main(String[] args) throws Exception{
  		ArrayList<String> strList = new ArrayList<>();
  		strList.add("aaa");
  		strList.add("bbb");
  		
  	//	strList.add(100);
  		//获取ArrayList的Class对象，反向的调用add()方法，添加数据
  		Class listClass = strList.getClass(); //得到 strList 对象的字节码 对象
  		//获取add()方法
  		Method m = listClass.getMethod("add", Object.class);
  		//调用add()方法
  		m.invoke(strList, 100);
  		
  		//遍历集合
  		for(Object obj : strList){
  			System.out.println(obj);
  		}
  	}
  }
  //控制台输出
  //aaa
  //bbb
  //100
  ```

  

## 5.Java线程

### 概念原理

+ 进程与线程

>  ​    **进程:**是指一个内存中运行的应用程序，每个进程都有自己独立的一块内存空间，即进程空间或（虚空间）。进程不依赖于线程而独立存在，一个进程中可以启动多个线程。比如在Windows系统中，一个运行的exe就是一个进程。
>
>  ​    **线程:**是指进程中的一个执行流程，一个进程中可以运行多个线程。比如java.exe进程中可以运
>  行很多线程。线程总是属于某个进程，线程没有自己的虚拟地址空间，与进程内的其他线程一起
>  共享分配给该进程的所有资源。
>
>  “同时”执行是人的感觉，在线程之间实际上轮换执行。       
>  进程在执行过程中拥有独立的内存单元，进程有独立的地址空间，而多个线程共享内存，从而极>  大地提高了程序的运行效率。
>
>  线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序>列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执>行控制。
>
>  进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动，进程是系统进
>  行资源分配和调度的一个独立单位。
>
>  线程是进程的一个实体，是CPU调度和分派的基本单位，它是比进程更小的能独立运行
>  的基本单位。线程自己基本上不拥有系统资源，只拥有一点在运行中必不可少的资源（如程
>  序计数器,一组寄存器和栈），但是它可与同属一个进程的其他的线程共享进程所拥有的全部>资源。        
>  线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间，
>
>  **一个线程包含以下内容：**
>
>  一个指向当前被执行指令的指令指针；
>  一个栈；
>  一个寄存器值的集合，定义了一部分描述正在执行线程的处理器状态的值
>  一个私有的数据区。
>  我们使用Join()方法挂起当前线程，直到调用Join()方法的线程执行完毕。该方法
>  还存在包含参数的重载版本，其中的参数用于指定等待线程结束的最长时间（即超
>  时）所花费的毫秒数。如果线程中的工作在规定的超时时段内结束，该版本的Join()方法将返回>一个布尔量True。
>
>   **简而言之：**
>  一个程序至少有一个进程，一个进程至少有一个线程。
>  线程的划分尺度小于进程，使得多进程程序的并发性高。
>  另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。
>  线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。
>  从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别。
>       **在Java中，每次程序运行至少启动2个线程：一个是main线程，一个是垃圾收集线程**。因为每当使用java命令执行一个类的时候，实际上都会启动一个JVM，每一个JVM实际上就>是在操作系统中启动了一个进程。

+ Java中的线程

> 在Java中，“线程”指两件不同的事情：
>         1、`java.lang.Thread`类的一个实例；         
>         2、线程的执行。       
>         **在 Java程序中，有两种方法创建线程：        
>         一是对 Thread 类进行派生并覆盖 run方法；        
>         二是通过实现Runnable接口创建**。         
>         使用`java.lang.Thread`类或者`java.lang.Runnable`接口编写代码来定义、实例化和启动新线程。        
>         一个Thread类实例只是一个对象，像Java中的任何其他对象一样，具有变量和方法，生死于堆上。         
>         Java中，每个线程都有一个调用栈，即使不在程序中创建任何新的线程，线程也在后台运行着。        
>         一个Java应用总是从main()方法开始运行，main()方法运行在一个线程内，他被称为主线程。        
>         一旦创建一个新的线程，就产生一个新的调用栈。        
>         线程总体分两类：用户线程和守候线程。       
>         当所有用户线程执行完毕的时候，JVM自动关闭。但是守候线程却不独立于JVM，守候线程一般是由操作系统  或者用户自己创建的。

### 线程的创建于启动

#### 定义线程

 1、扩展`java.lang.Thread`类。

```markdown
    此类中有个run()方法，应该注意其用法：public void run()

    如果该线程是使用独立的Runnable运行对象构造的，则调用该Runnable对象的run方法；否则，该方法不执行任何操作并返回。

    Thread的子类应该重写该方法。
```

2、实现`java.lang.Runnable`接口。

```markdown
    void run()

    使用实现接口Runnable的对象创建一个线程时，启动该线程将导致在独立执行的线程中调用对象的run方法。

    方法run的常规协定是，它可能执行任何所需的操作。
```
#### 实例化线程

1. 如果是扩展`java.lang.Thread`类的线程，则直接new即可。
2. 如果是实现了`java.lang.Runnable`接口的类，则用Thread的构造方法：

```java
 // Runnable target：实现了Runnable接口的类的实例。
//Thread类也实现了Runnable接口，因此，从Thread类继承的类的实例也可以作为target传入这个构造方法。
Thread(Runnabletarget) 
//线程池建立多线程。
// String name：线程的名子。这个名子可以在建立Thread实例后通过Thread类的setName方法设置。默认线程名：Thread-N，N是线程建立的顺序，是一个不重复的正整数。
Thread(Runnabletarget, String name)  
// ThreadGroup group：当前建立的线程所属的线程组。如果不指定线程组，所有的线程都被加到一个默认的线程组中。
Thread(ThreadGroupgroup, Runnable target)  
Thread(ThreadGroupgroup, Runnable target, String name) 
// long stackSize：线程栈的大小，这个值一般是CPU页面的整数倍。如x86的页面大小是4KB.在x86平台下，默认的线程栈大小是12KB
Thread(ThreadGroupgroup, Runnable target, String name, long stackSize)  
```

#### 启动线程

+ 在线程的Thread对象上调用start()方法，而不是run()或者别的方法。
+ 在调用start()方法之前：线程处于新状态中，新状态指有一个Thread对象，但还没有一个真正的线程。
+ 在调用start()方法之后：发生了一系列复杂的事情
  1. 启动新的执行线程（具有新的调用栈）
  2. 该线程从新状态转移到可运行状态
  3. 当该线程获得机会执行时，其目标run()方法将运行

> 对Java来说，run()方法没有任何特别之处。像main()方法一样，它只是新线程知道调用的方法名称（和签名）。因此，在Runnable上或者Thread上调用run方法是合法的。但并不启动新的线程。

#### 实例演示

1. 实现Runnable接口的多线程例子

   ```java
   /** 
    * 实现Runnable接口的类 
    */  
   public class RunnableImpl implements Runnable{  
       private String name;  
       public RunnableImpl(String name) {  
          this.name = name;  
       }  
       @Override  
       public void run() {  
          for (int i = 0; i < 5; i++) {  
         //for(long k=0;k<100000000;k++);是用来模拟一个非常耗时的操作的。
              for(long k=0;k<100000000;k++);  
              System.out.println(name+":"+i);  
          }       
       }  
   }  
      
   /** 
    * 测试Runnable类实现的多线程程序 
    */  
   public class TestRunnable {  
      
       public static void main(String[] args) {  
          RunnableImpl ri1=new RunnableImpl("李白");  
          RunnableImpl ri2=new RunnableImpl("屈原");  
          Thread t1=new Thread(ri1);  
          Thread t2=new Thread(ri2);  
          t1.start();  
          t2.start();  
       }  
   }  
   
   //输出结果
   屈原:0  
   李白:0  
   屈原:1  
   李白:1  
   屈原:2  
   李白:2  
   李白:3  
   屈原:3  
   李白:4  
   屈原:4  
   ```

2. 扩展Thread类实现的多线程例子

   ```java
   /** 
    * 测试扩展Thread类实现的多线程程序 
    */  
   public class TestThread extends Thread {  
       public TestThread(String name){  
          super(name);  
       }  
       @Override  
       public void run() {  
          for(int i=0;i<5;i++){  
              for(long k=0;k<100000000;k++);  
              System.out.println(this.getName()+":"+i);  
          }  
       }  
       public static void main(String[] args){  
          Thread t1=new TestThread("李白");  
          Thread t2=new TestThread("屈原");  
          t1.start();  
          t2.start();        
       }  
   }  
   //执行结果
   屈原:0  
   李白:0  
   屈原:1  
   李白:1  
   屈原:2  
   李白:2  
   屈原:3  
   屈原:4  
   李白:3  
   李白:4  
   ```

   

### 常见问题

```markdown
    1、线程的名字，一个运行中的线程总是有名字的，名字有两个来源，一个是虚拟机自己给的名字，一个是你自己的定的名字。在没有指定线程名字的情况下，虚拟机总会为线程指定名字，并且主线程的名字总是mian，非主线程的名字不确定。

    2、线程都可以设置名字，也可以获取线程的名字，连主线程也不例外。

    3、获取当前线程的对象的方法是：Thread.currentThread()；

    4、在上面的代码中，只能保证：每个线程都将启动，每个线程都将运行直到完成。一系列线程以某种顺序启动并不意味着将按该顺序执行。对于任何一组启动的线程来说，调度程序不能保证其执行次序，持续时间也无法保证。

    5、当线程目标run()方法结束时该线程完成。

    6、一旦线程启动，它就永远不能再重新启动。只有一个新的线程可以被启动，并且只能一次。一个可运行的线程或死线程可以被重新启动。

    7、线程的调度是JVM的一部分，在一个CPU的机器上上，实际上一次只能运行一个线程。一次只有一个线程栈执行。JVM线程调度程序决定实际运行哪个处于可运行状态的线程。

    众多可运行线程中的某一个会被选中做为当前线程。可运行线程被选择运行的顺序是没有保障的。

    8、尽管通常采用队列形式，但这是没有保障的。队列形式是指当一个线程完成“一轮”时，它移到可运行队列的尾部等待，直到它最终排队到该队列的前端为止，它才能被再次选中。事实上，我们把它称为可运行池而不是一个可运行队列，目的是帮助认识线程并不都是以某种有保障的顺序排列而成一个一个队列的事实。

    9、尽管我们没有无法控制线程调度程序，但可以通过别的方式来影响线程调度的方式。
```
### 线程栈模型与线程的变量

> ​     要理解线程调度的原理，以及线程执行过程，必须理解线程栈模型。
>
> ​      **线程栈**是指某时刻时内存中线程调度的栈信息，当前调用的方法总是位于栈顶。线程栈的内容是随着程序的运行动态变化的，因此研究线程栈必须选择一个运行的时刻（实际上指代码运行到什么地方)。
>
> 下面通过一个示例性的代码说明线程（调用）栈的变化过程。

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-25_174021.png)

> ​    这幅图描述在代码执行到两个不同时刻1、2时候，虚拟机线程调用栈示意图。
>
> ​    当程序执行到`t.start()`;时候，程序多出一个分支（增加了一个调用栈B），这样，栈A、栈B并行执行。
>
> ​    从这里就可以看出**方法调用和线程启动的区别**了。

### 线程状态的转换

+ 线程的状态转换是线程控制的基础。线程状态总的可以分为五大状态。用一个图来描述如下

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-25_192118.png)

1. **新状态**：线程对象已经创建，还没有在其上调用start()方法。
2. **可运行状态**：当线程有资格运行，但调度程序还没有把它选定为运行线程时线程所处的状态。当start()方法调用时，线程首先进入可运行状态。在线程运行之后或者从阻塞、等待或睡眠状态回来后，也返回到可运行状态。
3. **运行状态**：线程调度程序从可运行池中选择一个线程作为当前线程时线程所处的状态。这也是线程进入运行状态的唯一一种方式。
4. **等待/阻塞/睡眠状态**：这是线程有资格运行时它所处的状态。实际上这个三状态组合为一种，其共同点是：线程仍旧是活的，但是当前没有条件运行。换句话说，它是可运行的，但是如果某件事件出现，他可能返回到可运行状态
5. 死亡态：当线程的run()方法完成时就认为它死去。这个线程对象也许是活的，但是，它已经不是一个单独执行的线程。线程一旦死亡，就不能复生。如果在一个死去的线程上调用start()方法，会抛出`java.lang.IllegalThreadStateException`异常。

### 阻止线程执行

>  对于线程的阻止，考虑一下三个方面，不考虑IO阻塞的情况; 睡眠；等待;因为需要一个对象的锁定而被阻塞;

1.**睡眠**

> `Thread.sleep(longmillis)`和`Thread.sleep(long millis, int nanos)`静态方法强制当前正在执行的线程休眠（暂停执行），以“减慢线程”。当线程睡眠时，它入睡在某个地方，在苏醒之前不会返回到可运行状态。当睡眠      时间到期，则返回到可运行状态。
>   线程睡眠的原因：线程执行太快，或者需要强制进入下一轮，因为Java规范不保证合> 理的轮换。
>   睡眠的实现：调用静态方法。
>
>  睡眠的位置：为了让其他线程有机会执行，可以将`Thread.sleep()`的调用放线程run()之内。这样才能保证该线程执行过程中会睡眠。
>
>  例如，在前面的例子中，将一个耗时的操作改为睡眠，以减慢线程的执行。可以这么写

```java
public class TestThread extends Thread {  
    public TestThread(String name){  
       super(name);  
    }  
    @Override  
    public void run() {  
       for(int i=0;i<5;i++){  
           //睡眠3秒，减缓方法
          try {  
                Thread.sleep(3);  
            } catch (InterruptedException e) {  
                e.printStackTrace();  
            }  
           System.out.println(this.getName()+":"+i);  
       }  
    }  
    //这样，线程在每次执行过程中，总会睡眠3毫秒，睡眠了，其他的线程就有机会执行了。
    //线程睡眠到期自动苏醒，并返回到可运行状态，不是运行状态。sleep()中指定的时间是线程不会运行的最短时间。因此，sleep()方法不能保证该线程睡眠到期后就开始执行。
    //sleep()是静态方法，只能控制当前正在运行的线程线程的优先级和线程让步yield()
```

2. **线程的优先级和线程让步yield()**

>  线程的让步是通过`Thread.yield()`来实现的。yield()方法的作用是：暂停当前正在执行的线程对象，并执行其他线程。
>
> 要理解yield()，必须了解线程的优先级的概念。线程总是存在优先级，优先级范围在1~10之间。JVM线程调度程序是基于优先级的抢先调度机制。在大多数情况下，当前运行的线程优先级将大于或等于线程池中任何线程的优先级。但这仅仅是大多数情况。
>
> 注意：当设计多线程应用程序的时候，一定不要依赖于线程的优先级。因为线程调度优先级操作是没有保障的，只能把线程优先级作用作为一种提高程序效率的方法，但是要保证程序不依赖这种操作。
>
> 当线程池中线程都具有相同的优先级，调度程序的JVM实现自由选择它喜欢的线程。这时候调度程序的操作有两种可能：一是选择一个线程运行，直到它阻塞或者运行完成为止。二是时间分片，为池内的每个线程提供均等的运行机会。
>
> 设置线程的优先级：线程默认的优先级是创建它的执行线程的优先级。可以通过`setPriority(int newPriority)`更改线程的优先级。例如：

```java
Thread t = new MyThread();  
t.setPriority(8);  //优先级 1-10
t.start();  
//线程优先级为1~10之间的正整数，JVM从不会改变一个线程的优先级。然而，1~10之间的值是没有保证的。一些JVM可能不能识别10个不同的值，而将这些优先级进行每两个或多个合并，变成少于10个的优先级，则两个或多个优先级的线程可能被映射为一个优先级。
```

+ 线程默认优先级是5，Thread类中有三个常量，定义线程优先级范围

```java
static intMAX_PRIORITY; //线程可以具有的最高优先级。  
static intMIN_PRIORITY; //线程可以具有的最低优先级。  
static intNORM_PRIORITY; //分配给线程的默认优先级。
```

+ `Thread.yield()`方法

>  `Thread.yield()`方法作用是：**暂停当前正在执行的线程对象**，并执行其他线程。
>          `yield()`应该做的是让当前运行线程回到可运行状态，以允许具有相同优先级的其他线程获得运行机会。因此，使用yield()的目的是让相同优先级的线程之间能适当的轮转执行。但是，实际中无法保证`yield()`达到让步目的，因为让步的线程还有可能被线程调度程序再次选中。
>         结论：`yield()`从未导致线程转到等待/睡眠/阻塞状态。在大多数情况下，`yield()`将导致线程从运行状态转到可运行状态，但有可能没有效果。

+ join()方法

>  Thread的非静态方法join()让一个线程B“加入”到另外一个线程A的尾部。在A执行完毕之前，B不能工作。例如

```java
Thread t = new MyThread();  
t.start();  
t.join();  
```

> 另外，`join()`方法还有带超时限制的重载版本。例如`t.join(5000);`则让线程等待5000毫秒，如果超过这个时间，则停止等待，变为可运行状态。
>
> 线程的加入join()对线程栈导致的结果是线程栈发生了变化，当然这些变化都是瞬时的。下面给示意图：

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-25_221837.png)

### 总结

+ 到目前位置，介绍了线程离开运行状态的3种方法
  1. 调用`Thread.sleep()`：使当前线程睡眠至少多少毫秒（尽管它可能在指定的时间之前被中断）。
  2. 调用`Thread.yield()`：不能保障太多事情，尽管通常它会让当前运行线程回到可运行性状态，使得有相同优先级的线程有机会执行。
  3. 调用join()方法：保证当前线程停止执行，直到该线程所加入的线程完成为止。然而，如果它加入的线程没有存活，则当前线程不需要停止。

+  除了以上三种方式外，还有下面几种特殊情况可能使线程离开运行状态
  1. 线程的run()方法完成。
  2. 在对象上调用wait()方法（不是在线程上调用）。
  3. 线程不能在对象上获得锁定，它正试图运行该对象的方法代码。
  4. 线程调度程序可以决定将当前运行状态移动到可运行状态，以便让另一个线程获得运行机会，而不需要任何理由。

## 6.线程的同步与锁

### 同步问题提出

> 线程的同步是为了防止多个线程访问一个数据对象时，对数据造成的破坏。
>
> ​    例如：两个线程`ThreadA、ThreadB`都操作同一个对象Foo对象，并修改Foo对象上的数据。

```java
public class Foo {  
    private int x = 100;  
    public int getX() {  
        return x;  
    }  
    public int fix(int y) {  
        x = x - y;  
        return x;  
    }  
}   
   
public class FooRunnable implements Runnable {  
    private Foo foo =new Foo();  
   
    public static void main(String[] args) {  
       FooRunnable r = new FooRunnable();  
        Thread ta = new Thread(r,"Thread-A");  
        Thread tb = new Thread(r,"Thread-B");  
        ta.start();  
        tb.start();  
    }  
   
    @Override  
    public void run() {  
       for (int i = 0; i < 3; i++) {  
            this.fix(30);  
            try {  
                Thread.sleep(1);  
            } catch (InterruptedException e) {  
                e.printStackTrace();  
            }  
            System.out.println(Thread.currentThread().getName()+ " :当前foo对象的x值= " + foo.getX());  
        }  
    }  
   
    public int fix(int y) {  
       return foo.fix(y);  
    }  
}  
//运行结果
Thread-B :当前foo对象的x值= 40  
Thread-A :当前foo对象的x值=  10  
Thread-B :当前foo对象的x值= -20  
Thread-A :当前foo对象的x值= -50  
Thread-B :当前foo对象的x值= -80  
Thread-A :当前foo对象的x值= -80 
```

+ 从结果发现，这样的输出值明显是不合理的，原因是两个线程不加控制的访问Foo对象并修改其数据所致。
+  如果要保持结果的合理性，只需要达到一个目的，就是将对Foo的访问加以限制，每次只能有一个线程在访问。这样就能保证Foo对象中数据的合理性了。
+ 在具体的Java代码中需要完成以下两个操作
  1. 把竞争访问的资源类Foo变量x标识为private
  2. 同步修改变量的代码，使用synchronized关键字同步方法或代码。

### 同步和锁定

+ 锁的原理

  >  ​     **Java中每个对象都有一个内置锁**。
  >    ​     当程序运行到非静态的synchronized同步方法上时，自动获得与正在执行代码类的当前实例（this实例）有关的锁。获得一个对象的锁也称为获取锁、锁定对象、在对象上锁定或在对象上同步。    
  >       当程序运行到synchronized同步方法或代码块时才该对象锁才起作用。
  >       一个对象只有一个锁。所以，**如果一个线程获得该锁，就没有其他线程可以获得锁**，直到第一个线程释放（或返回）锁。这也意味着任何其他线程都不能进入该对象上的synchronized方法或代码块，直到该锁被释放。
  >       释放锁是指持锁线程退出了synchronized同步方法或代码块。

+ 关于锁和同步，有一下几个要点
  1. 只能同步方法，而不能同步变量和类；
  2. 每个对象只有一个锁；当提到同步时，应该清楚在什么上同步？也就是说，在哪个对象上同步？
  3. 不必同步类中所有的方法，类可以同时拥有同步和非同步方法。
  4. 如果两个线程要执行一个类中的synchronized方法，并且两个线程使用相同的实例来调用方法，那么一次只能有一个线程能够执行方法，另一个需要等待，直到锁被释放。也就是说：如果一个线程在对象上获得一个锁，就没有任何其他线程可以进入（该对象的）类中的任何一个同步方法。
  5. 如果线程拥有同步和非同步方法，则非同步方法可以被多个线程自由访问而不受锁的限制。
  6. 线程睡眠时，它所持的任何锁都不会释放。
  7. 线程可以获得多个锁。比如，在一个对象的同步方法里面调用另外一个对象的同步方法，则获取了两个对象的同步锁。
  8. 同步损害并发性，应该尽可能缩小同步范围。同步不但可以同步整个方法，还可以同步方法中一部分代码块。
  9. 在使用同步代码块时候，应该指定在哪个对象上同步，也就是说要获取哪个对象的锁。例如：

```java
public int fix(int y) {  
       synchronized (this) {  
           x = x - y;  
       }  
       return x;  
   }  
```

+  当然，同步方法也可以改写为非同步方法，但功能完全一样的，例如

```java
public synchronized int getX() {  
    return x++;  
}  
//与
public int getX() {  
      synchronized (this) {  
          return x;  
      }  
  }      
```

### 静态方法同步

+  要同步静态方法，需要一个用于整个类对象的锁，这个对象是就是这个类`（XXX.class)`

```java
public static intsetName(String name){  
      synchronized(Xxx.class){  
            Xxx.name = name;  
      }  
}  
```

### 如果线程不能获得锁会怎么样

> 如果线程试图进入同步方法，而其锁已经被占用，则线程在该对象上被阻塞。实质上，线程进入该对象的一种池中，必须在那里等待，直到其锁被释放，该线程再次变为可运行或运行为止

+  当考虑阻塞时，一定要注意哪个对象正被用于锁定
  1. 调用同一个对象中非静态同步方法的线程将彼此阻塞。如果是不同对象，则每个线程有自己的对象的锁，线程间彼此互不干预。
  2. 调用同一个类中的静态同步方法的线程将彼此阻塞，它们都是锁定在相同的Class对象上。
  3. 静态同步方法和非静态同步方法将永远不会彼此阻塞，因为静态方法锁定在Class对象上，非静态方法锁定在该类的对象上。
  4. 对于同步代码块，要看清楚什么对象已经用于锁定（synchronized后面括号的内容）。在同一个对象上进行同步的线程将彼此阻塞，在不同对象上锁定的线程将永远不会彼此阻塞。

### 何时需要同步

+  在多个线程同时访问互斥（可交换）数据时，应该同步以保护数据，确保两个线程不会同时修改更改它。
+ 对于非静态字段中可更改的数据，通常使用非静态方法访问。
+ 对于静态字段中可更改的数据，通常使用静态方法访问。
+ 如果需要在非静态方法中使用静态字段，或者在静态字段中调用非静态方法，问题将变得非常复杂。

### 线程安全类

> ​      当一个类已经很好的同步以保护它的数据时，这个类就称为“线程安全的”。
>    ​     即使是线程安全类，也应该特别小心，因为操作的线程之间仍然不一定安全。    
>    ​     举个形象的例子，比如一个集合是线程安全的，有两个线程在操作同一个集合对象，当第一个线程查询集合非空后，删除集合中所有元素的时候。第二个线程也来执行与第一个线程相同的操作，也许在第一个线程查询后，第二个线程也查询出集合非空，但是当第一个执行清除后，第二个再执行删除显然是不对的，因为此时集合已经为空了。例如：

```java
public class NameList {  
    private List nameList = Collections.synchronizedList(newLinkedList());  
   
    public void add(String name) {  
        nameList.add(name);  
    }  
   
    public String removeFirst() {  
       if (nameList.size()>0) {  
       return (String) nameList.remove(0);  
       } else {  
           return null;  
       }  
    }    
}  
   
public class TestNameList {  
    public static void main(String[] args) {  
        final NameList nl =new NameList();  
         nl.add("苏东坡");  
         class NameDropper extends Thread{  
           @Override  
           public void run() {  
              String name = nl.removeFirst();  
                System.out.println(name);  
           }          
         }  
         Thread t1=new NameDropper();  
         Thread t2=new NameDropper();  
         t1.start();  
         t2.start();  
    }  
}  
//执行结果
苏东坡  
null  
```

### 线程死锁

>  死锁对Java程序来说，是很复杂的，也很难发现问题。当两个线程被阻塞，每个线程在等待另一个线程时就发生死锁。还是看一个比较直观的死锁例子：

```java
public class Deadlock {  
    private static class Resource{  
       public int value;  
    }  
    private Resource resourceA=new Resource();  
    private Resource resourceB=new Resource();  
    public int read(){  
       synchronized (resourceA) {  
           synchronized (resourceB) {  
              return resourceB.value+resourceA.value;  
           }  
       }  
    }  
    public void write(int a,int b){  
       synchronized(resourceB){  
           synchronized (resourceA) {  
              resourceA.value=a;  
              resourceB.value=b;  
           }  
       }  
    }  
}  
```

> 假设read()方法由一个线程启动，write()方法由另外一个线程启动。读线程将拥有`resourceA`锁，写线程将拥有`resourceB`锁，两者都坚持等待的话就出现死锁。
>         实际上，上面这个例子发生死锁的概率很小。因为在代码内的某个点，CPU必须从读线程切换到写线程，所以，死锁基本上不能发生。
>         但是，无论代码中发生死锁的概率有多小，一旦发生死锁，程序就死掉。有一些设计方法能帮助避免死锁，包括始终按照预定义的顺序获取锁这一策略。已经超出SCJP的考试范围。

### 线程同步小结

+ 线程同步的目的是为了保护多个线程访问一个资源时对资源的破坏。
+ 线程同步方法是通过锁来实现，每个对象都有切仅有一个锁，这个锁与一个特定的对象关联，线程一旦获取了对象锁，其他访问该对象的线程就无法再访问该对象的其他同步方法。
+ 对于同步，要时刻清醒在哪个对象上同步，这是关键。
+ 编写线程安全的类，需要时刻注意对多个线程竞争访问资源的逻辑和安全做出正确的判断，对“原子”操作做出分析，并保证原子操作期间别的线程无法访问竞争资源。
+ 当多个线程等待一个对象锁时，没有获取到锁的线程将发生阻塞。
+ 死锁是线程间相互等待锁锁造成的，在实际中发生的概率非常的小。真让你写个死锁程序，不一定好使，呵呵。但是，一旦程序发生死锁，程序将死掉。

### 线程的交互

> 线程交互是比较复杂的问题，SCJP要求不很基础：给定一个场景，编写代码来恰当使用等待、通知和通知所有线程。

#### 线程交互的基本知识

+ 线程交互知识点需要从`java.lang.Object`的类的三个方法来学习：

```java
void notify() //唤醒在此对象监视器上等待的单个线程。  
void notifyAll() //唤醒在此对象监视器上等待的所有线程。  
void wait() //导致当前的线程等待，直到其他线程调用此对象的 notify()方法或 notifyAll()方法
```

+ wait 的两个重载方法

```java
void wait(longtimeout) //导致当前的线程等待，直到其他线程调用此对象的 notify()方法或 notifyAll()方法，或者超过指定的时间量。  
void wait(longtimeout, int nanos) //导致当前的线程等待，直到其他线程调用此对象的 notify()方法或 notifyAll()方法，或者其他某个线程中断当前线程，或者已超过某个实际时间量。
```

以上这些方法是帮助线程传递线程关心的时间状态。

+  关于等待/通知，要记住的关键点是
  + 必须从同步环境内调用`wait()、notify()、notifyAll()`方法。线程不能调用对象上等待或通知的方法，除非它拥有那个对象的锁。
  + `wait()、notify()、notifyAll()`都是Object的实例方法。与每个对象具有锁一样，每个对象可以有一个线程列表，他们等待来自该信号（通知）。线程通过执行对象上的wait()方法获得这个等待列表。从那时候起，它不再执行任何其他指令，直到调用对象的notify()方法为止。如果多个线程在同一个对象上等待，则将只选择一个线程（不保证以何种顺序）继续执行。如果没有线程等待，则不采取任何特殊操作。


+ 例如

```java
/** 
 * 计算输出其他线程锁计算的数据 
 */  
public class ThreadA {  
    public static void main(String[] args) {  
       ThreadB b=new ThreadB();  
       //启动计算线程  
       b.start();  
       //线程A拥有b对象上的锁。线程为了调用wait()或notify()方法，该线程必须是那个对象锁的拥有者  
       synchronized (b) {  
           try {  
              System.out.println("等待对象b完成计算......");  
              b.wait();  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
           System.out.println("b对象计算的总和是：" + b.total);  
       }  
    }  
}  
   
/** 
 * 计算1+2+3+...+100的和 
 */  
public class ThreadB extends Thread {  
    int total;  
    public void run(){  
       synchronized (this) {  
           for (int i=0;i<101;i++){  
              total+=i;  
           }  
           //（完成计算了）唤醒在此对象监视器上等待的单个线程，在本例中线程A被唤醒  
           notify();  
       }  
    }  
}  
//执行结果
等待对象b完成计算......  
b对象计算的总和是：5050  
```

**注意**：当在对象上调用wait()方法时，执行该代码的线程立即放弃它在对象上的锁。然而调用notify()时，并不意味着这时线程会放弃其锁。如果线程荣然在完成同步代码，则线程在移出之前不会放弃锁。因此，只要调用notify()并不意味着这时该锁变得可用。

#### 多个线程在等待一个对象锁时候使用`notifyAll()`

> 在多数情况下，最好通知等待某个对象的所有线程。如果这样做，可以在对象上使用`notifyAll()`让所有在此对象上等待的线程冲出等待区，返回到可运行状态。

+ 举例说明

```java
/** 
 * 计算线程 
 */  
public class Calculator extends Thread {  
    int total;  
    @Override  
    public void run() {  
       synchronized (this) {  
           for(int i=0;i<101;i++){  
              total+=i;  
           }  
        }  
       //通知所有在此对象上等待的线程  
       notifyAll();  
    }    
}  
   
/** 
 * 获取计算结果并输出 
 */  
public class ReaderResult extends Thread {  
    Calculator c;  
    public ReaderResult(Calculator c) {  
       this.c = c;  
    }  
    public void run(){  
       synchronized (c) {  
           try {  
              System.out.println(Thread.currentThread() + "等待计算结果......");  
              c.wait();  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
            System.out.println(Thread.currentThread()+ "计算结果为：" + c.total);  
       }  
    }  
    public static void main(String[] args) {  
       Calculator calculator=new Calculator();  
       //启动三个线程，分别获取计算结果  
       new ReaderResult(calculator).start();  
       new ReaderResult(calculator).start();  
       new ReaderResult(calculator).start();  
       //启动计算线程  
       calculator.start();  
    }  
}  

//执行结果
Thread[Thread-1,5,main]等待计算结果......  
Thread[Thread-2,5,main]等待计算结果......  
Thread[Thread-3,5,main]等待计算结果......  
Exception in thread"Thread-0" java.lang.IllegalMonitorStateException  
    atjava.lang.Object.notifyAll(Native Method)  
    attest.Calculator.run(Calculator.java:15)  
Thread[Thread-3,5,main]计算结果为：5050  
Thread[Thread-2,5,main]计算结果为：5050  
Thread[Thread-1,5,main]计算结果为：5050  
```

> ​      运行结果表明，程序中有异常，并且多次运行结果可能有多种输出结果。这就是说明，这个多线程的交互程序还存在问题。究竟是出了什么问题，需要深入的分析和思考，下面将做具体分析。
>
> ​      实际上，上面这个代码中，我们期望的是读取结果的线程在计算线程调用`notifyAll()`之前等待即可。但是，如果计算线程先执行，并在读取结果线程等待之前调用了notify()方法，那么又会发生什么呢？这种情况是可能发生的。因为无法保证线程的不同部分将按照什么顺序来执行。幸运的是当读取线程运行时，它只能马上进入等待状态----它没有做任何事情来检查等待的事件是否已经发生。 ----因此，如果计算线程已经调用了`notifyAll()`方法，那么它就不会再次调用`notifyAll()`，----并且等待的读取线程将永远保持等待。这当然是开发者所不愿意看到的问题。
>
> 因此，当等待的事件发生时，需要能够检查`notifyAll()`通知事件是否已经发生。
>
> 通常，解决上面问题的最佳方式是利用某种循环，该循环检查某个条件表达式，只有当正在等待的事情还没有发生的情况下，它才继续等待。

#### 线程的调度

##### 线程休眠

>  Java线程调度是Java多线程的核心，只有良好的调度，才能充分发挥系统的性能，提高程序的执行效率。
>
> 这里要明确的一点，不管程序员怎么编写调度，只能最大限度的影响线程执行的次序，而不能做到精准控制。
>
> 线程休眠的目的是使线程让出CPU的最简单的做法之一，线程休眠时候，会将CPU资源交给其他线程，以便能轮换执行，当休眠一定时间后，线程会苏醒，进入准备状态等待执行。
>
> 线程休眠的方法是`Thread.sleep(long millis)`和`Thread.sleep(long millis, int nanos)`，均为静态方法，那调用sleep休眠的哪个线程呢？简单说，哪个线程调用sleep，就休眠哪个线程。

```java
/** 
 * Java线程：线程的调度-休眠 
 */  
public class TestSleep {  
    public static void main(String[] args) {  
       Thread t1=new MyThread1();  
       Thread t2=new Thread(new MyRunnable());  
       t1.start();  
       t2.start();  
    }  
}  
class MyThread1 extends Thread{  
    @Override  
    public void run() {  
       for(int i=0;i<3;i++){  
           System.out.println("线程1第"+i+"次执行！");  
           try {  
              Thread.sleep(50);  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
       }  
    }    
}  
class MyRunnable implements Runnable{  
    @Override  
    public void run() {       
       for(int i=0;i<3;i++){  
           System.out.println("线程2第"+i+"次执行！");  
           try {  
              Thread.sleep(50);  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
       }  
    }    
}  
//执行结果
线程1第0次执行！  
线程2第0次执行！  
线程2第1次执行！  
线程1第1次执行！  
线程2第2次执行！  
线程1第2次执行！  
```

+ 从上面的结果输出可以看出，无法精准保证线程执行次序。

##### 线程优先级

> 与线程休眠类似，线程的优先级仍然无法保障线程的执行次序。只不过，优先级高的线程获取CPU资源的概率较大，优先级低的并非没机会执行。
>
> 线程的优先级用1-10之间的整数表示，数值越大优先级越高，默认的优先级为5。
>
>  在一个线程中开启另外一个新线程，则新开线程称为该线程的子线程，子线程初始优先级与父线程相同。

```java
/** 
 * Java线程：线程的调度-优先级 
 */  
public class TestPriority {  
    public static void main(String[] args) {  
       Thread t1=new MyThread1();  
       Thread t2=new Thread(new MyRunnable());  
       t1.setPriority(10);  
       t2.setPriority(1);  
       t1.start();  
       t2.start();  
    }  
}  
class MyThread1 extends Thread{  
    @Override  
    public void run() {  
       for(int i=0;i<10;i++){  
           System.out.println("线程1第"+i+"次执行！");  
           try {  
              Thread.sleep(100);  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
       }  
    }    
}  
class MyRunnable implements Runnable{  
    @Override  
    public void run() {       
       for(int i=0;i<10;i++){  
           System.out.println("线程2第"+i+"次执行！");  
           try {  
              Thread.sleep(100);  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
       }  
    }    
}  
//执行结果
线程1第0次执行！  
线程1第1次执行！  
线程1第2次执行！  
线程2第0次执行！  
线程1第3次执行！  
线程2第1次执行！  
线程1第4次执行！  
线程2第2次执行！  
线程1第5次执行！  
线程2第3次执行！  
线程1第6次执行！  
线程2第4次执行！  
线程1第7次执行！  
线程2第5次执行！  
线程1第8次执行！  
线程2第6次执行！  
线程1第9次执行！  
线程2第7次执行！  
线程2第8次执行！  
线程2第9次执行！  
```

##### 线程让步

> 线程的让步含义就是使当前运行着线程让出CPU资源，但是让给谁不知道，仅仅是让出，线程状态回到可运行状态。
>
> 线程的让步使用`Thread.yield()`方法，yield()为静态方法，功能是暂停当前正在执行的线程对象，并执行其他线程。

```java
/** 
 * Java线程：线程的调度-让步 
 */  
public class Test {  
    public static void main(String[] args) {  
       Thread t1=new MyThread1();  
       Thread t2=new Thread(new MyRunnable());  
       t1.start();  
       t2.start();  
    }  
}  
class MyThread1 extends Thread{  
    @Override  
    public void run() {  
       for(int i=0;i<10;i++){  
           System.out.println("线程1第"+i+"次执行！");          
       }  
    }    
}  
class MyRunnable implements Runnable{  
    @Override  
    public void run() {       
       for(int i=0;i<10;i++){  
           System.out.println("线程2第"+i+"次执行！");  
           Thread.yield();  
       }  
    }    
}  
//执行结果
线程2第0次执行！  
线程1第0次执行！  
线程1第1次执行！  
线程1第2次执行！  
线程1第3次执行！  
线程1第4次执行！  
线程1第5次执行！  
线程1第6次执行！  
线程1第7次执行！  
线程1第8次执行！  
线程1第9次执行！  
线程2第1次执行！  
线程2第2次执行！  
线程2第3次执行！  
线程2第4次执行！  
线程2第5次执行！  
线程2第6次执行！  
线程2第7次执行！  
线程2第8次执行！  
线程2第9次执行！
```

##### 线程合并

> 线程的合并的含义就是将几个并行线程的线程合并为一个单线程执行，应用场景是当一个线程必须等待另一个线程执行完毕才能执行时可以使用join方法。
>
> ​    join为非静态方法，定义如下：

```java
void join()——等待该线程终止。     
void join(longmillis)——等待该线程终止的时间最长为 millis毫秒。     
void join(longmillis,int nanos)——等待该线程终止的时间最长为 millis毫秒 + nanos 纳秒。  
//////////////////////////////////////////////////////////////////////////////////////////
/** 
 * Java线程：线程的调度-合并 
 */  
public class Test {  
    public static void main(String[] args) {  
       Thread t1=new MyThread1();       
       t1.start();  
       for (int i = 0; i < 20; i++) {  
           System.out.println("主线程第" + i +"次执行！");  
           if (i>2) {  
              try {  
                  ///t1线程合并到主线程中，主线程停止执行过程，转而执行t1线程，直到t1执行完毕后继续。  
                  t1.join();  
              } catch (InterruptedException e) {  
                  e.printStackTrace();  
              }  
           }  
       }  
    }  
}  
class MyThread1 extends Thread{  
    @Override  
    public void run() {  
       for(int i=0;i<10;i++){  
           System.out.println("线程1第"+i+"次执行！");          
       }  
    }    
}  
//执行结果
主线程第0次执行！  
主线程第1次执行！  
主线程第2次执行！  
主线程第3次执行！  
线程1第0次执行！  
线程1第1次执行！  
线程1第2次执行！  
线程1第3次执行！  
线程1第4次执行！  
线程1第5次执行！  
线程1第6次执行！  
线程1第7次执行！  
线程1第8次执行！  
线程1第9次执行！  
主线程第4次执行！  
主线程第5次执行！  
主线程第6次执行！  
主线程第7次执行！  
主线程第8次执行！  
主线程第9次执行！  
主线程第10次执行！
```

##### 守护线程

> 守护线程与普通线程写法上基本么啥区别，调用线程对象的方法`setDaemon(true)`，则可以将其设置为守护线程。
>
> 如果有用户自定义线程存在的话，`jvm`就不会退出——此时，守护线程也不能退出，也就是它还要运行，干嘛呢，就是为了执行垃圾回收的任务啊。
>
> 守护线程使用的情况较少，但并非无用，举例来说，JVM的垃圾回收、内存管理等线程都是守护线程。还有就是在做数据库应用时候，使用的数据库连接池，连接池本身也包含着很多后台线程，监控连接个数、超时时间、状态等等。
>
> ​    `setDaemon`方法的详细说明：

```java
public final void setDaemon(boolean on)
//将该线程标记为守护线程或用户线程。当正在运行的线程都是守护线程时，Java虚拟机退出。  
```

+ 该方法必须在启动线程前调用。
+ 该方法首先调用该线程的 `checkAccess`方法，且不带任何参数。这可能抛出 `SecurityException`（在当前线程中）
+ 参数：on - 如果为true，则将该线程标记为守护线程。
+ 可能抛出异常
  +  `IllegalThreadStateException`- 如果该线程处于活动状态。
  + `SecurityException`- 如果当前线程无法修改该线程。

```java
/** 
 * Java线程：线程的调度-守护线程 
 */  
public class Test {  
    public static void main(String[] args) {  
       Thread t1=new MyCommon();  
       Thread t2=new Thread(new MyDaemon());  
       t2.setDaemon(true);//设置为守护线程  
       t2.start();  
       t1.start();        
    }  
}  
class MyCommon extends Thread{  
    @Override  
    public void run() {  
       for(int i=0;i<5;i++){  
           System.out.println("线程1第"+i+"次执行！");  
           try {  
              Thread.sleep(7);  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
       }  
    }    
}  
class MyDaemon implements Runnable{  
    @Override  
    public void run() {  
       for (long i = 0; i < 9999999L; i++) {  
           System.out.println("后台线程第" + i +"次执行！");  
           try {  
              Thread.sleep(7);  
           } catch (InterruptedException e) {  
              e.printStackTrace();  
           }  
       }  
    }    
}  
//执行结果
线程1第0次执行！  
后台线程第0次执行！  
后台线程第1次执行！  
线程1第1次执行！  
后台线程第2次执行！  
线程1第2次执行！  
后台线程第3次执行！  
线程1第3次执行！  
后台线程第4次执行！  
线程1第4次执行！  
后台线程第5次执行！  
后台线程第6次执行！  
后台线程第7次执行！  
后台线程第8次执行！  
后台线程第9次执行！  
后台线程第10次执行！
```

> 从上面的执行结果可以看出：
>
> ​    前台线程是保证执行完毕的，后台线程还没有执行完毕就退出了。
>
> ​    实际上：JRE判断程序是否执行结束的标准是所有的前台执线程行完毕了，而不管后台线程的状态，因此，在使用后台县城时候一定要注意这个问题。

#### 线程的同步

##### 同步方法

> 线程的同步是保证多线程安全访问竞争资源的一种手段。
>
> ​    线程的同步是Java多线程编程的难点，往往开发者搞不清楚什么是竞争资源、什么时候需要考虑同步，怎么同步等等问题，当然，这些问题没有很明确的答案，但有些原则问题需要考虑，是否有竞争资源被同时改动的问题？
>
>  对于同步，在具体的Java代码中需要完成一下两个操作：
>
>         把竞争访问的资源标识为private；
>         
>         同步哪些修改变量的代码，使用synchronized关键字同步方法或代码。
>         
>         当然这不是唯一控制并发安全的途径。
>         
>         synchronized关键字使用说明
>         
>         synchronized只能标记非抽象的方法，不能标识成员变量。

+ 为了演示同步方法的使用，构建了一个信用卡账户，起初信用额为100w，然后模拟透支、存款等多个操作。显然银行账户User对象是个竞争资源，而多个并发操作的是账户方法`oper(int x)`，当然应该在此方法上加上同步，并将账户的余额设为私有变量，禁止直接访问。

```java
/** 
 * Java线程：线程的同步 
 */  
public class Test {  
    public static void main(String[] args) {  
       User u = new User("张三", 100);  
       MyThread t1 = new MyThread("线程A", u, 20);  
       MyThread t2 = new MyThread("线程B", u, -60);  
       MyThread t3 = new MyThread("线程C", u, -80);  
       MyThread t4 = new MyThread("线程D", u, -30);  
       MyThread t5 = new MyThread("线程E", u, 32);  
       MyThread t6 = new MyThread("线程F", u, 21);  
       t1.start();  
       t2.start();  
       t3.start();  
       t4.start();  
       t5.start();  
       t6.start();  
    }  
}  
   
class MyThread extends Thread {  
    private User u;  
    private int y = 0;  
   
    MyThread(String name, User u, int y) {  
       super(name);  
       this.u = u;  
       this.y = y;  
    }  
    public void run() {  
       u.oper(y);  
    }  
}  
   
class User {  
    private String code;  
    private int cash;  
    User(String code, int cash) {  
       this.code = code;  
       this.cash = cash;  
    }  
    public String getCode() {  
       return code;  
    }  
    public void setCode(String code) {  
       this.code = code;  
    }  
   
    /** 
     * 业务方法 
     * @param x  添加x万元 
     */  
    public synchronized void oper(int x) {  
       try {  
           Thread.sleep(10L);  
           this.cash += x;  
           System.out.println(Thread.currentThread().getName() + "运行结束，增加“"  
                  + x + "”，当前用户账户余额为：" + cash);  
           Thread.sleep(10L);  
       } catch (InterruptedException e) {  
           e.printStackTrace();  
       }  
    }  
    @Override  
    public String toString() {  
       return "User{" + "code='" + code + '\'' + ",cash=" + cash + '}';  
    }  
}  
//执行结果
线程A运行结束，增加“20”，当前用户账户余额为：120  
线程F运行结束，增加“21”，当前用户账户余额为：141  
线程D运行结束，增加“-30”，当前用户账户余额为：111  
线程B运行结束，增加“-60”，当前用户账户余额为：51  
线程E运行结束，增加“32”，当前用户账户余额为：83  
线程C运行结束，增加“-80”，当前用户账户余额为：3 
//反面教材，不同步的情况，也就是去掉oper(int x)方法的synchronized修饰符，然后运行程序，结果如下：
线程F运行结束，增加“21”，当前用户账户余额为：121  
线程D运行结束，增加“-30”，当前用户账户余额为：91  
线程B运行结束，增加“-60”，当前用户账户余额为：31  
线程E运行结束，增加“32”，当前用户账户余额为：63  
线程A运行结束，增加“20”，当前用户账户余额为：3  
线程C运行结束，增加“-80”，当前用户账户余额为：-17  
```

+ 很显然，上面的结果是错误的，**导致错误的原因是多个线程并发访问了竞争资源u**，并对u的属性做了改动。
+ 可见同步的重要性。
+ 通过前文可知，线程退出同步方法时将释放掉方法所属对象的锁，但还应该注意的是，同步方法中还可以使用特定的方法对线程进行调度。这些方法来自于`java.lang.Object`类。

```java
void notify()      //唤醒在此对象监视器上等待的单个线程。      
void notifyAll()      //唤醒在此对象监视器上等待的所有线程。      
void wait()      //导致当前的线程等待，直到其他线程调用此对象的 notify()方法或 notifyAll()方法。      
void wait(long timeout)      
   //导致当前的线程等待，直到其他线程调用此对象的 notify()方法或 notifyAll()方法，或者超过指定的时间量。      
void wait(long timeout,int nanos)      
    //导致当前的线程等待，直到其他线程调用此对象的 notify()方法或 notifyAll()方法，或者其他某个线程中断当前线程，或者已超过某个实际时间量。  
```

+  结合以上方法，处理多线程同步与互斥问题非常重要，著名的生产者-消费者例子就是一个经典的例子，任何语言多线程必学的例子

##### 同步块

>  对于同步，除了同步方法外，还可以使用同步代码块，有时候同步代码块会带来比同步方法更好的效果。
>         追其同步的根本的目的，是控制竞争资源的正确的访问，因此只要在访问竞争资源的时候保证同一时刻只能一个线程访问即可，因此Java引入了同步代码快的策略，以提高性能。    
>         在上个例子的基础上，对oper方法做了改动，由同步方法改为同步代码块模式，程序的执行逻辑并没有问。

```java
 public void oper(int x) {  
       try {  
           Thread.sleep(10L);  
           //同步代码块
           synchronized (this) {  
              this.cash += x;  
              System.out.println(Thread.currentThread().getName() + "运行结束，增加“"  
                     + x + "”，当前用户账户余额为：" + cash);  
           }           
           Thread.sleep(10L);  
       } catch (InterruptedException e) {  
           e.printStackTrace();  
       }  
    }  
```

+ 在使用synchronized关键字时候，应该尽可能避免在synchronized方法或synchronized块中使用sleep或者yield方法，因为synchronized程序块占有着对象锁，你休息那么其他的线程只能一边等着你醒来执行完了才能执行。不但严重影响效率，也不合逻辑。
+ 同样，在同步程序块内调用yeild方法让出CPU资源也没有意义，因为你占用着锁，其他互斥线程还是无法访问同步程序块。当然与同步程序块无关的线程可以获得更多的执行时间。

##### 并发协作

###### 生产者消费者模型

>  对于多线程程序来说，不管任何编程语言，生产者和消费者模型都是最经典的。就像学习每一门编程语言一样，Hello World！都是最经典的例子。
>
> 实际上，准确说应该是“生产者-消费者-仓储”模型，离开了仓储，生产者消费者模型就显得没有说服力了。

+ 对于此模型，应该明确一下几点：
  + 生产者仅仅在仓储未满时候生产，仓满则停止生产
  + 消费者仅仅在仓储有产品时候才能消费，仓空则等待
  + 当消费者发现仓储没产品可消费时候会通知生产者生产
  + 生产者在生产出可消费产品时候，应该通知等待的消费者去消费
  + 此模型将要结合java.lang.Object的wait与notify、notifyAll方法来实现以上的需求。这是非常重要的。

```java
/** 
 * Java线程：并发协作-生产者消费者模型 
 */  
public class Test {
    public static void main(String[] args) {
        Godown godown = new Godown(10);
        Producer p1 = new Producer(20, godown);
        Producer p2 = new Producer(30, godown);
        Producer p3 = new Producer(10, godown);
        Producer p4 = new Producer(25, godown);
        Producer p5 = new Producer(20, godown);
        Consume c1 = new Consume(20, godown);
        Consume c2 = new Consume(30, godown);
        Consume c3 = new Consume(10, godown);
        Consume c4 = new Consume(15, godown);
        Consume c5 = new Consume(50, godown);
        p1.start();
        p2.start();
        p3.start();
        p4.start();
        p5.start();
        c1.start();
        c2.start();
        c3.start();
        c4.start();
        c5.start();
    }
} 
/** 
 * 仓库 
 */  
public class Godown {
    public static final int MAX_SIZE = 100;//最大库存
    public int currentNum;//当前库存
    Godown(){};
    Godown(int currentNum){
        this.currentNum = currentNum;
    };
    /**
     * 生产指定数量的商品
     */
    public synchronized void product(int needNum) throws InterruptedException {
        while (needNum+currentNum>MAX_SIZE){
            System.out.println("需要生产的数量"+needNum+"超过剩余库存容量"+(MAX_SIZE-currentNum)+"不能继续生产");
            wait();
        }
        //可以生产的情况下
        currentNum+=needNum;
        System.out.println("生产出了"+needNum+"个产品,现仓库有"+currentNum);
        //唤醒在此对象上等待的所有线程
        notifyAll();
    }
    /**
     * 消费指定数量的产品
     */
    public synchronized void consume(int needNum) throws InterruptedException {
        while (needNum>currentNum){
			System.out.println("超过剩余库存容量");
            wait();
            
        }
        currentNum-=needNum;
        System.out.println("已经消费了"+needNum+"个，当前库存为"+currentNum);
        //唤醒在此对象上等待的所有线程
        notifyAll();
    }
}
//生产者  
public class Producer extends Thread {
    private int needNum;//生产产品的数量 
    private Godown godown;//仓库

       Producer(int needNum,Godown godown) {
        this.needNum = needNum;
        this.godown = godown;
    }

    @Override
    public void run() {
        try {
            godown.product(needNum);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
} 
//消费者  
public class Consume extends Thread {
    private int needNum;
    private Godown godown;
    Consume(int needNum,Godown godown){
        this.needNum = needNum;
        this.godown = godown;
    }

    @Override
    public void run() {
        try {
            godown.consume(needNum);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
//执行结果
生产出了20个产品,现仓库有30
生产出了30个产品,现仓库有60
生产出了10个产品,现仓库有70
生产出了25个产品,现仓库有95
需要生产的数量20超过剩余库存容量5不能继续生产
已经消费了20个，当前库存为75
生产出了20个产品,现仓库有95   //之前等待的线程
已经消费了30个，当前库存为65
已经消费了10个，当前库存为55
已经消费了15个，当前库存为40
超过剩余库存容量,线程等待
```

+ 对于本例，要说明的是当发现不能满足生产或者消费条件的时候，调用对象的wait方法，wait方法的作用是释放当前线程的所获得的锁，并调用对象的notifyAll()方法，通知（唤醒）该对象上其他等待线程，使得其继续执行。这样，整个生产者、消费者线程得以正确的协作执行。
+  **notifyAll() 方法，起到的是一个通知作用，不释放锁，也不获取锁**。只是告诉该对象上等待的线程“可以竞争执行了，都醒来去执行吧”。
+ 本例仅仅是生产者消费者模型中最简单的一种表示，本例中，**如果消费者消费的仓储量达不到满足，而又没有生产者，则程序会一直处于等待状态，这当然是不对的**。实际上可以将此例进行修改，修改为，根据消费驱动生产，同时生产兼顾仓库，如果仓不满就生产，并对每次最大消费量做个限制，这样就不存在此问题了，当然这样的例子更复杂，更难以说明这样一个简单模型。

###### 死锁

>  线程发生死锁可能性很小，即使看似可能发生死锁的代码，在运行时发生死锁的可能性也是小之又小。
>
> ​    发生死锁的原因一般是两个对象的锁相互等待造成的。

```java
/** 
 * Java线程：并发协作-死锁 
 */  
public class Test {  
    public static void main(String[] args) {  
       DeadlockRisk dead = new DeadlockRisk();  
       MyThread t1 = new MyThread(dead, 1, 2);  
       MyThread t2 = new MyThread(dead, 3, 4);  
       MyThread t3 = new MyThread(dead, 5, 6);  
       MyThread t4 = new MyThread(dead, 7, 8);  
       t1.start();  
       t2.start();  
       t3.start();  
       t4.start();  
    }  
}  
   
class MyThread extends Thread {  
    private DeadlockRisk dead;  
    private int a, b;  
   
    MyThread(DeadlockRisk dead, int a, int b) {  
       this.dead = dead;  
       this.a = a;  
       this.b = b;  
    }  
    @Override  
    public void run() {  
       dead.read();  
       dead.write(a, b);  
    }  
}  
   
class DeadlockRisk {  
    private static class Resource {  
       public int value;  
    }  
    private Resource resourceA = new Resource();  
    private Resource resourceB = new Resource();  
    public int read() {  
       synchronized (resourceA) {  
           System.out.println("read():" + Thread.currentThread().getName()  
                  + "获取了resourceA的锁！");  
           synchronized (resourceB) {  
              System.out.println("read():" + Thread.currentThread().getName()  
                     + "获取了resourceB的锁！");  
              return resourceB.value + resourceA.value;  
           }  
       }  
    }  
    public void write(int a, int b) {  
       synchronized (resourceB) {  
           System.out.println("write():" + Thread.currentThread().getName()  
                  + "获取了resourceA的锁！");  
           synchronized (resourceA) {  
              System.out.println("write():"  
                     + Thread.currentThread().getName() + "获取了resourceB的锁！");  
              resourceA.value = a;  
              resourceB.value = b;  
           }  
       }  
    }  
}  
//执行结果
read():Thread-1获取了resourceA的锁！  
read():Thread-1获取了resourceB的锁！  
write():Thread-1获取了resourceA的锁！  
write():Thread-1获取了resourceB的锁！  
read():Thread-3获取了resourceA的锁！  
read():Thread-3获取了resourceB的锁！  
write():Thread-3获取了resourceA的锁！  
write():Thread-3获取了resourceB的锁！  
read():Thread-2获取了resourceA的锁！  
read():Thread-2获取了resourceB的锁！  
write():Thread-2获取了resourceA的锁！  
write():Thread-2获取了resourceB的锁！  
read():Thread-0获取了resourceA的锁！  
read():Thread-0获取了resourceB的锁！  
write():Thread-0获取了resourceA的锁！  

```

#### 线程新特征

##### 线程池

> Sun在Java5中，对Java线程的类库做了大量的扩展，其中线程池就是Java5的新特征之一，除了线程池之外，还有很多多线程相关的内容，为多线程的编程带来了极大便利。为了编写高效稳定可靠的多线程程序，线程部分的新增内容显得尤为重要。
>
> 有关Java5线程新特征的内容全部在java.util.concurrent下面，里面包含数目众多的接口和类，熟悉这部分API特征是一项艰难的学习过程。目前有关这方面的资料和书籍都少之又少，大所属介绍线程方面书籍还停留在java5之前的知识层面上。
>
> 当然新特征对做多线程程序没有必须的关系，在java5之前通用可以写出很优秀的多线程程序。只是代价不一样而已。
>
> 线程池的基本思想还是一种对象池的思想，开辟一块内存空间，里面存放了众多（未死亡）的线程，池中线程执行调度由池管理器来处理。当有线程任务时，从池中取一个，执行完成后线程对象归池，这样可以避免反复创建线程对象所带来的性能开销，节省了系统的资源。
>
>  在Java5之前，要实现一个线程池是相当有难度的，现在Java5为我们做好了一切，我们只需要按照提供的API来使用，即可享受线程池带来的极大便利。
>
>  Java5的线程池分好多种：固定尺寸的线程池、单任务线程池、可变尺寸连接池、延迟连接池、单任务延迟连接池、自定义线程池。
>
> 在使用线程池之前，必须知道如何去创建一个线程池，在Java5中，需要了解的是java.util.concurrent.Executors类的API，这个类提供大量创建连接池的静态方法，是必须掌握的。

###### 固定大小的线程池

```java
/** 
 * Java线程：线程池 
 */ 
public class PoolTest {
    public static void main(String[] args) {
        //创建一个可重用固定线程数的线程池  
        ExecutorService pool = Executors.newFixedThreadPool(2);
        //创建实现了Runnable接口对象，Thread对象当然也实现了Runnable接口 
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();
        MyThread t4 = new MyThread();
        //将线程放入线程池中进行执行
        pool.execute(t1);
        pool.execute(t2);
        pool.execute(t3);
        pool.execute(t4);
        //关闭线程池
        pool.shutdown();
    }
}
class MyThread extends Thread{  
    public void run(){  
       System.out.println(Thread.currentThread().getName()+"正在执行...");  
    }  
}  
//执行结果
pool-1-thread-1正在执行...
pool-1-thread-2正在执行...
pool-1-thread-3正在执行...
pool-1-thread-4正在执行...
```

###### 单任务线程池

```java
//只更改线程池的创建方式即可
//创建一个使用单个 worker线程的 Executor，以无界队列方式来运行该线程。  
ExecutorService pool=Executors.newSingleThreadExecutor();  

//执行结果
pool-1-thread-1正在执行
pool-1-thread-1正在执行
pool-1-thread-1正在执行
pool-1-thread-1正在执行
```

+ 对于以上两种连接池，大小都是固定的，当要加入的池的线程（或者任务）超过池最大尺寸时候，则入此线程池需要排队等待。
+  一旦池中有线程完毕，则排队等待的某个线程会入池执行。

###### 多任务线程池

+ 与上面的类似，只是改动下pool的创建方式：

```java
//创建一个可根据需要创建新线程的线程池，但是在以前构造的线程可用时将重用它们。  
        ExecutorService pool=Executors.newCachedThreadPool(); 

//执行结果
pool-1-thread-2正在执行...  
pool-1-thread-4正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-3正在执行...  
```

###### 延迟连接池

```java
/** 
 * Java线程：线程池 
 */  
public class Test {  
    public static void main(String[] args) {  
       //创建一个线程池，它可安排在给定延迟后运行命令或者定期地执行。  
        ScheduledExecutorServicepool=Executors.newScheduledThreadPool(2);  
       //创建实现了Runnable接口对象，Thread对象当然也实现了Runnable接口  
        Thread t1 = new MyThread();  
        Thread t2 = new MyThread();  
        Thread t3 = new MyThread();  
        Thread t4 = new MyThread();  
        Thread t5 = new MyThread();  
        //将线程放入线程池中进行执行  
        pool.execute(t1);  
        pool.execute(t2);  
        pool.execute(t3);  
        //使用延迟执行风格的方法  
        pool.schedule(t4, 10, TimeUnit.MILLISECONDS);  
        pool.schedule(t5, 10, TimeUnit.MILLISECONDS);  
        //关闭线程池  
        pool.shutdown();  
    }  
}  
class MyThread extends Thread{  
    public void run(){  
       System.out.println(Thread.currentThread().getName()+"正在执行...");  
    }  
}  
//执行结果
pool-1-thread-1正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-2正在执行...  
```

###### 单任务延迟连接池

```java
//创建一个单任务执行线程池，它可安排在给定延迟后运行命令或者定期地执行。  
 ScheduledExecutorServicepool=Executors.newSingleThreadScheduledExecutor(); 

//执行结果
pool-1-thread-1正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-1正在执行...  
```

###### 自定义线程池

+ ThreadPoolExecutor

```java
 ThreadPoolExecutor(int corePoolSize,  int maximumPoolSize,  long keepAliveTime,  TimeUnit unit,        BlockingQueue<Runnable> workQueue) 
    
    
corePoolSize //池中所保存的线程数，包括空闲线程。  
maximumPoolSize //池中允许的最大线程数。  
keepAliveTime //当线程数大于核心时，此为终止前多余的空闲线程等待新任务的最长时间。  
unit -keepAliveTime //参数的时间单位。  
workQueue //执行前用于保持任务的队列。此队列仅保持由execute方法提交的Runnable任务
```



```java
/** 
 * Java线程：线程池-自定义线程池 
 */  
public class Test {  
    public static void main(String[] args) {  
       //创建阻塞队列  
       BlockingQueue<Runnable> bqueue=newArrayBlockingQueue<Runnable>(20);  
  //创建一个单线程执行任务，它可安排在给定延迟后运行命令或者定期地执行。
        ThreadPoolExecutor pool=new ThreadPoolExecutor(2, 3, 2, TimeUnit.MILLISECONDS, bqueue);  
       //创建实现了Runnable接口对象，Thread对象当然也实现了Runnable接口  
       Thread t1 = new MyThread();  
       Thread t2 = new MyThread();  
        Thread t3 = new MyThread();  
        Thread t4 = new MyThread();  
        Thread t5 = new MyThread();  
        Thread t6 = new MyThread();  
        Thread t7 = new MyThread();  
        //将线程放入线程池中进行执行  
        pool.execute(t1);  
        pool.execute(t2);  
        pool.execute(t3);  
        pool.execute(t4);  
        pool.execute(t5);  
        pool.execute(t6);  
        pool.execute(t7);  
        //关闭线程池  
        pool.shutdown();  
    }  
}  
class MyThread extends Thread{  
    public void run(){  
       System.out.println(Thread.currentThread().getName()+"正在执行...");  
       try {  
           Thread.sleep(100L);  
       } catch (InterruptedException e) {  
           e.printStackTrace();  
       }  
    }  
}  
//执行结果
pool-1-thread-1正在执行...  
pool-1-thread-2正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-2正在执行...  
pool-1-thread-1正在执行...  
pool-1-thread-2正在执行...  
pool-1-thread-1正在执行...  
```

##### 有返回值的线程

> 在Java5之前，线程是没有返回值的，常常为了“有”返回值，破费周折，而且代码很不好写。或者干脆绕过这道坎，走别的路了。现在Java终于有可返回值的任务（也可以叫做线程）了。
>
> 可返回值的任务必须实现Callable接口，类似的，无返回值的任务必须Runnable接口。
>
>  执行Callable任务后，可以获取一个Future的对象，在该对象上调用get就可以获取到Callable任务返回的Object了。

```java
public class PoolTest {
    public static void main(String[] args) throws ExecutionException, InterruptedException {

        ExecutorService pool = Executors.newFixedThreadPool(4);  
        //创建两个有返回值的任务  
        MyCallable t1 = new MyCallable(1);
        MyCallable t2 = new MyCallable(2);
        MyCallable t3 = new MyCallable(3);
        MyCallable t4 = new MyCallable(4);
        //执行任务并获取Future对象 
        Future<?> f1 = pool.submit(t1);
        Future<?> f2 = pool.submit(t2);
        Future<?> f3 = pool.submit(t3);
        Future<?> f4 = pool.submit(t4);
        //从Future对象上获取任务的返回值，并输出到控制台 
        System.out.println(">>>"+f1.get().toString());
        System.out.println(">>>"+f2.get().toString());
        System.out.println(">>>"+f3.get().toString());
        System.out.println(">>>"+f4.get().toString());
        //关闭线程池
        pool.shutdown();
    }
}

public class Callable implements Callable {

    private int y = 0;
    MyThread(int y){
        this.y=y;
    };
    @Override
    public Object call() throws Exception {
        return y+"个";
    }
}

//执行结果
>>>1个
>>>2个
>>>3个
>>>4个
```

##### 锁(上)普通锁

> 在Java5中，专门提供了锁对象，利用锁可以方便的实现资源的封锁，用来控制对竞争资源并发访问的控制，这些内容主要集中在java.util.concurrent.locks包下面，里面有三个重要的接口Condition、Lock、ReadWriteLock。

```markdown
	Condition将Object监视器方法（wait、notify和 notifyAll）分解成截然不同的对象，以便通过将这些对象与任意Lock实现组合使用，为每个对象提供多个等待 set（wait-set）。  
	Lock实现提供了比使用synchronized方法和语句可获得的更广泛的锁定操作。  
	ReadWriteLock维护了一对相关的锁定，一个用于只读操作，另一个用于写入操作。
```

+ 举例

```java
/** 
 * Java线程：线程池-锁 
 */  
public class Test {
    public static void main(String[] args) {
        MyCount myCount = new MyCount("18337020703", 10000);
        Lock lock = new ReentrantLock();  //普通锁
        ExecutorService pool = Executors.newCachedThreadPool();
        User u1 = new User("王向斌", myCount, -4000, lock);
        User u2 = new User("崔莲花", myCount, 5000, lock);
        User u3 = new User("王先锋", myCount, 10000, lock);
        User u4 = new User("刘蕊", myCount, -10000, lock);
        pool.execute(u1);
        pool.execute(u2);
        pool.execute(u3);
        pool.execute(u4);
        pool.shutdown();
    }
}
//信用卡用户  
public class User implements Runnable {
    private String name;//用户名  
    private MyCount myCount;//所要操作的账户  
    private int iocash;//操作的金额，当然有正负之分了  
    private Lock myLock;//执行操作所需的锁对象  

    public User(String name, MyCount myCount, int iocash, Lock myLock) {
        this.name = name;
        this.myCount = myCount;
        this.iocash = iocash;
        this.myLock = myLock;
    }

    @Override
    public void run() {
        //获取锁
        myLock.lock();
        //执行业务操作
        System.out.println(name+"正在操作"+myCount.getOid()+"账户"+"，当前金额为"+myCount.getCash()+"存入金额"+iocash);
        myCount.setCash(myCount.getCash()+iocash);
        System.out.println(name+"操作"+myCount.getOid()+"账户成功，存入金额为"+iocash+"，当前金额为"+myCount.getCash());
        ////释放锁，否则别的线程没有机会执行了
        myLock.unlock();
    }
}
//信用卡账户，可随意透支  
public class MyCount {
    private String Oid; //账号
    private int cash;   //账户余额

    public MyCount(String oid, int cash) {
        Oid = oid;
        this.cash = cash;
    }

    public String getOid() {
        return Oid;
    }

    public void setOid(String oid) {
        Oid = oid;
    }

    public int getCash() {
        return cash;
    }

    public void setCash(int cash) {
        this.cash = cash;
    }

    @Override
    public String toString() {
        return "MyCount{" +
                "Oid='" + Oid + '\'' +
                ", cash=" + cash +
                '}';
    }
}
//执行结果
王向斌正在操作18337020703账户，当前金额为10000存入金额-4000
王向斌操作18337020703账户成功，存入金额为-4000，当前金额为6000
崔莲花正在操作18337020703账户，当前金额为6000存入金额5000
崔莲花操作18337020703账户成功，存入金额为5000，当前金额为11000
王先锋正在操作18337020703账户，当前金额为11000存入金额10000
王先锋操作18337020703账户成功，存入金额为10000，当前金额为21000
刘蕊正在操作18337020703账户，当前金额为21000存入金额-10000
刘蕊操作18337020703账户成功，存入金额为-10000，当前金额为11000
```



##### 锁(下)读写锁

>  在上文中提到了Lock接口以及对象，使用它，很优雅的控制了竞争资源的安全访问，但是这种锁不区分读写，称这种锁为普通锁。为了提高性能，Java提供了读写锁，在读的地方使用读锁，在写的地方使用写锁，灵活控制，在一定程度上提高了程序的执行效率。
>
>  Java中读写锁有个接口java.util.concurrent.locks.ReadWriteLock，也有具体的实现ReentrantReadWriteLock，详细的API可以查看JavaAPI文档。
>
>  下面这个例子是在文例子的基础上，将普通锁改为读写锁，并添加账户余额查询的功能，代码如下：

```java
/** 
 * Java线程：线程池-锁 
 */  
public class Test {
    public static void main(String[] args) {
        MyCount myCount = new MyCount("18337020703", 10000);
        ReadWriteLock lock = new ReentrantReadWriteLock(false);  //读写锁
        ExecutorService pool = Executors.newCachedThreadPool();
        User u1 = new User("王向斌", myCount, -4000, lock,false); //false写操作
        User u2 = new User("崔莲花", myCount, 5000, lock,false);
        User u3 = new User("王先锋", myCount, 10000, lock,false);
        User u4 = new User("刘蕊", myCount, -10000, lock,false);
        User u5 = new User("王先锋", myCount, 0, lock,true);  //true读操作
        pool.execute(u1);
        pool.execute(u2);
        pool.execute(u3);
        pool.execute(u4);
        pool.execute(u5);
        pool.shutdown();
    }
}
//信用卡用户  
public class User implements Runnable {
    private String name;//用户名  
    private MyCount myCount;//所要操作的账户  
    private int iocash;//操作的金额，当然有正负之分了  
    private ReadWriteLock myLock;//执行操作所需的锁对象  
    private Boolean isCheck;  //是否查询

    public User(String name, MyCount myCount, int iocash, ReadWriteLock myLock,Boolean isCheck) {
        this.name = name;
        this.myCount = myCount;
        this.iocash = iocash;
        this.myLock = myLock;
        this.isCheck = isCheck;
    }

    @Override
    public void run() {
        if (isCheck){  //判断是否为读
            myLock.readLock().lock();  //开启读锁
            System.out.println("读操作"+name + "正在查询" + myCount.getOid() + "账户" + "，当前金额为" + myCount.getCash());
            myLock.readLock().unlock();  //关闭读锁
        }else {
            myLock.writeLock().lock();  //开启写锁
            System.out.println("写操作"+name + "正在操作" + myCount.getOid() + "账户" + "，当前金额为" + myCount.getCash() + "存入金额" + iocash);
            myCount.setCash(myCount.getCash() + iocash);
            System.out.println("写操作"+name + "操作" + myCount.getOid() + "账户成功，存入金额为" + iocash + "，当前金额为" + myCount.getCash());
            myLock.writeLock().unlock(); //关闭写锁
        }
    }
}
//信用卡账户，可随意透支  
public class MyCount {
    private String Oid; //账号
    private int cash;   //账户余额

    public MyCount(String oid, int cash) {
        Oid = oid;
        this.cash = cash;
    }

    public String getOid() {
        return Oid;
    }

    public void setOid(String oid) {
        Oid = oid;
    }

    public int getCash() {
        return cash;
    }

    public void setCash(int cash) {
        this.cash = cash;
    }

    @Override
    public String toString() {
        return "MyCount{" +
                "Oid='" + Oid + '\'' +
                ", cash=" + cash +
                '}';
    }
}
//执行结果
写操作 王向斌正在操作18337020703账户，当前金额为10000存入金额-4000
写操作 王向斌操作18337020703账户成功，存入金额为-4000，当前金额为6000
写操作 崔莲花正在操作18337020703账户，当前金额为6000存入金额5000
写操作 崔莲花操作18337020703账户成功，存入金额为5000，当前金额为11000
写操作 王先锋正在操作18337020703账户，当前金额为11000存入金额10000
写操作 王先锋操作18337020703账户成功，存入金额为10000，当前金额为21000
写操作 刘蕊正在操作18337020703账户，当前金额为21000存入金额-10000
写操作 刘蕊操作18337020703账户成功，存入金额为-10000，当前金额为11000
读操作 王先锋正在查询18337020703账户，当前金额为11000  //读操作
```

 **在实际开发中，最好在能用读写锁的情况下使用读写锁，而不要用普通锁，以求更好的性能**

##### 信号量

>  Java的信号量实际上是一个功能完毕的计数器，对控制一定资源的消费与回收有着很重要的意义，信号量常常用于多线程的代码中，并能监控有多少数目的线程等待获取资源，并且通过信号量可以得知可用资源的数目等等，这里总是在强调“数目”二字，但不能指出来有哪些在等待，哪些资源可用。
>
> 这个信号量类如果能返回数目，还能知道哪些对象在等待，哪些资源可使用，就非常完美了，仅仅拿到这些概括性的数字，对精确控制意义不是很大。目前还没想到更好的用法

##### 阻塞队列

>  阻塞队列是Java5线程新特征中的内容，Java定义了阻塞队列的接口
>
> 阻塞队列的概念是，一个指定长度的队列，如果队列满了，添加新元素的操作会被阻塞等待，直到有空位为止。同样，当队列为空时候，请求队列元素的操作同样会阻塞等待，直到有可用元素为止。 
>
>  有了这样的功能，就为多线程的排队等候的模型实现开辟了便捷通道，非常有用。
>
>  java.util.concurrent.BlockingQueue继承了java.util.Queue接口，可以参看API文档。

```java
/** 
 * Java线程：线程池-阻塞队列 
 */  
public class Test {  
    public static void main(String[] args) throws InterruptedException{  
       BlockingQueue bqueue = new ArrayBlockingQueue(10);  
        for (int i = 0; i < 30; i++) {  
                //将指定元素添加到此队列中，如果没有可用空间，将一直等待（如果有必要）。  
                bqueue.put(i);  
                System.out.println("向阻塞队列中添加了元素:" + i);  
        }  
        System.out.println("程序到此运行结束，即将退出----");  
    }  
}  
//执行结果
向阻塞队列中添加了元素:0  
向阻塞队列中添加了元素:1  
向阻塞队列中添加了元素:2  
向阻塞队列中添加了元素:3  
向阻塞队列中添加了元素:4  
向阻塞队列中添加了元素:5  
向阻塞队列中添加了元素:6  
向阻塞队列中添加了元素:7  
向阻塞队列中添加了元素:8  
向阻塞队列中添加了元素:9  
```

##### 阻塞栈

>  对于阻塞栈，与阻塞队列相似。不同点在于栈是“后入先出”的结构，每次操作的是栈顶，而队列是“先进先出”的结构，每次操作的是队列头。
>
> 这里要特别说明一点的是，阻塞栈是Java6的新特征。

```java
/** 
 * Java线程：线程池-阻塞栈 
 */  
public class Test {  
    public static void main(String[] args) throws InterruptedException{  
       BlockingDeque bDeque = new LinkedBlockingDeque(10);  
        for (int i = 0; i < 30; i++) {  
        //将指定元素添加到此阻塞栈中，如果没有可用空间，将一直等待（如果有必要）。  
            bDeque.putFirst(i);  
            System.out.println("向阻塞栈中添加了元素:" + i);  
        }  
        System.out.println("程序到此运行结束，即将退出----");  
    }  
}  
//执行结果
向阻塞栈中添加了元素:0  
向阻塞栈中添加了元素:1  
向阻塞栈中添加了元素:2  
向阻塞栈中添加了元素:3  
向阻塞栈中添加了元素:4  
向阻塞栈中添加了元素:5  
向阻塞栈中添加了元素:6  
向阻塞栈中添加了元素:7  
向阻塞栈中添加了元素:8  
向阻塞栈中添加了元素:9  
```

##### 条件变量

>  条件变量是Java5线程中很重要的一个概念，顾名思义，条件变量就是表示条件的一种变量。但是必须说明，这里的条件是没有实际含义的，仅仅是个标记而已，并且条件的含义往往通过代码来赋予其含义。
>
> 这里的条件和普通意义上的条件表达式有着天壤之别。
>
> 条件变量都实现了java.util.concurrent.locks.Condition接口，条件变量的实例化是通过一个Lock对象上调用newCondition()方法来获取的，这样，条件就和一个锁对象绑定起来了。因此，Java中的条件变量只能和锁配合使用，来控制并发程序访问竞争资源的安全.
>
> 条件变量的出现是为了更精细控制线程等待与唤醒，在Java5之前，线程的等待与唤醒依靠的是Object对象的wait()和notify()/notifyAll()方法，这样的处理不够精细。
>
>  而在Java5中，一个锁可以有多个条件，每个条件上可以有多个线程等待，通过调用await()方法，可以让线程在该条件下等待。当调用signalAll()方法，又可以唤醒该条件下的等待的线程。有关Condition接口的API可以具体参考JavaAPI文档。

```java
/** 
 * Java线程：条件变量 
 */  
public class Test {  
    public static void main(String[] args){  
       //创建并发访问的账户  
       MyCount myCount=new MyCount("6215580000000000000",10000);  
       //创建一个线程池  
       ExecutorService pool = Executors.newFixedThreadPool(2);  
       Thread t1 = new SaveThread("张三", myCount, 2000);  
        Thread t2 = new SaveThread("李四", myCount, 3600);  
        Thread t3 = new DrawThread("王五", myCount, 2700);  
        Thread t4 = new SaveThread("老张", myCount, 600);  
        Thread t5 = new DrawThread("老牛", myCount, 1300);  
        Thread t6 = new DrawThread("胖子", myCount, 800);  
        //执行各个线程  
        pool.execute(t1);  
        pool.execute(t2);  
        pool.execute(t3);  
        pool.execute(t4);  
        pool.execute(t5);  
        pool.execute(t6);  
        //关闭线程池  
        pool.shutdown();  
    }  
}  
//存款线程类  
class SaveThread extends Thread {  
    private String name;            //操作人  
    private MyCount myCount;        //账户  
    private int x;                  //存款金额  
     
    SaveThread(String name, MyCount myCount, int x) {  
            this.name = name;  
            this.myCount = myCount;  
            this.x = x;  
    }  
    public void run() {  
            myCount.saving(x, name);  
    }  
}  
//取款线程类  
class DrawThread extends Thread {  
    private String name;                //操作人  
    private MyCount myCount;        //账户  
    private int x;                            //存款金额  
   
    DrawThread(String name, MyCount myCount, int x) {  
            this.name = name;  
            this.myCount = myCount;  
            this.x = x;  
    }  
    public void run() {  
            myCount.drawing(x, name);  
    }  
}  
//普通银行账户，不可透支  
class MyCount {  
     private String oid;                        //账号  
     private int cash;                            //账户余额  
     private Lock lock =new ReentrantLock();         //账户锁  
     private Condition _save = lock.newCondition();    //存款条件  
     private Condition _draw = lock.newCondition();    //取款条件  
     MyCount(String oid, int cash) {       
         this.oid = oid;  
         this.cash = cash;  
     }  
     /** 
      * 存款 
      * @param x 存款金额 
      * @param name 存款人 
      */  
     public void saving(int x,String name){  
         lock.lock();                        //获取锁  
       if (x > 0) {  
           cash += x; // 存款  
           System.out.println(name + "存款" + x + "，当前余额为" + cash);  
       }  
         _draw.signalAll();            //唤醒所有等待线程。  
         lock.unlock();                    //释放锁  
     }  
     //取款  
     public void drawing(int x, String name) {  
     lock.lock();                                 //获取锁  
       try {  
           if (cash - x < 0) {  
              _draw.await(); // 阻塞取款操作  
           } else {  
              cash -= x; // 取款  
              System.out.println(name + "取款" + x + "，当前余额为" + cash);  
           }  
           _save.signalAll(); // 唤醒所有存款操作  
       } catch (InterruptedException e) {  
           e.printStackTrace();  
       } finally {  
           lock.unlock(); // 释放锁  
       }  
     }  
}  
//执行结果
张三存款2000，当前余额为12000  
王五取款2700，当前余额为9300  
老张存款600，当前余额为9900  
老牛取款1300，当前余额为8600  
胖子取款800，当前余额为7800  
李四存款3600，当前余额为11400  
```

+ 其他方式实现

  + synchronized关键字

  ```java
  class MyCount {  
       private String oid;                        //账号  
       private int cash;                            //账户余额  
       MyCount(String oid, int cash) {       
           this.oid = oid;  
           this.cash = cash;  
       }  
       /** 
        * 存款 
        * @param x 存款金额 
        * @param name 存款人 
        */  
       public synchronized void saving(int x,Stringname){         
         if (x > 0) {  
             cash += x; // 存款  
             System.out.println(name + "存款" + x + "，当前余额为" + cash);  
         }  
         notifyAll(); //唤醒所有等待线程。  
       }  
       //取款  
       public synchronized void drawing(int x, String name){       
         if (cash - x < 0) {  
             try {  
                wait();  
             } catch (InterruptedException e) {  
                e.printStackTrace();  
             }  
         } else {  
             cash -= x; // 取款  
             System.out.println(name + "取款" + x + "，当前余额为" + cash);  
         }  
         notifyAll(); // 唤醒所有存款操作       
       }  
  }  
  ```

  

  + synchronized方法

  ```java
  class MyCount {  
       private String oid;                        //账号  
       private int cash;                            //账户余额  
       MyCount(String oid, int cash) {       
           this.oid = oid;  
           this.cash = cash;  
       }  
       /** 
        * 存款 
        * @param x 存款金额 
        * @param name 存款人 
        */  
       public void saving(int x,String name){        
         if (x > 0) {  
             synchronized (this) {  
                cash += x; // 存款  
                System.out.println(name + "存款" + x + "，当前余额为" + cash);  
                notifyAll(); //唤醒所有等待线程。  
             }  
         }       
       }  
       //取款  
       public synchronized void drawing(int x, String name) {      
       synchronized (this) {  
          if (cash - x < 0) {  
              try {  
                 wait();  
              }catch (InterruptedException e) {  
                 e.printStackTrace();  
              }  
          } else {  
              cash -= x; // 取款  
              System.out.println(name + "取款" + x + "，当前余额为" + cash);  
          }               
       }  
       notifyAll(); // 唤醒所有存款操作  
       }  
  }  
  ```

  

##### 原子量

> 所谓的原子量即操作变量的操作是“原子的”，该操作不可再分，因此是线程安全的。
>
> 为何要使用原子变量呢，原因是多个线程对单个变量操作也会引起一些问题。在Java5之前，可以通过volatile、synchronized关键字来解决并发访问的安全问题，但这样太麻烦
>
>  Java5之后，专门提供了用来进行单变量多线程并发安全访问的工具包java.util.concurrent.atomic，其中的类也很简单。
>
> 原子量虽然可以保证单个变量在某一个操作过程的安全，但无法保证你整个代码块，或者整个程序的安全性。因此，通常还应该使用锁等同步机制来控制整个程序的安全性。

```java
/** 
 * Java线程：新特征-原子量 
 */  
public class Test {  
    public static void main(String[] args){  
       //创建一个线程池  
       ExecutorService pool = Executors.newFixedThreadPool(2);  
       Lock lock=new ReentrantLock(false);  
       Runnable t1 = new MyRunnable("张三", 2000,lock);  
       Runnable t2 = new MyRunnable("李四", 3600,lock);  
       Runnable t3 = new MyRunnable("王五", 2700,lock);  
       Runnable t4 = new MyRunnable("老张", 600,lock);  
       Runnable t5 = new MyRunnable("老牛", 1300,lock);  
       Runnable t6 = new MyRunnable("胖子", 800,lock);  
        //执行各个线程  
        pool.execute(t1);  
        pool.execute(t2);  
        pool.execute(t3);  
        pool.execute(t4);  
        pool.execute(t5);  
        pool.execute(t6);  
        //关闭线程池  
        pool.shutdown();  
    }  
}  
class MyRunnable implements Runnable {  
    private static AtomicLong aLong =newAtomicLong(10000);   //原子量，每个线程都可以自由操作  
    private String name;          //操作人  
    private int x;                //操作数额  
    private Lock lock;  
    MyRunnable(String name, int x,Lock lock) {  
            this.name = name;  
            this.x = x;  
            this.lock=lock;  
    }  
    public void run() {  
    lock.lock();  
        System.out.println(name + "执行了" + x +"，当前余额：" + aLong.addAndGet(x));  
        lock.unlock();  
    }  
}  
//执行结果
张三执行了2000，当前余额：12000  
王五执行了2700，当前余额：14700  
老张执行了600，当前余额：15300  
老牛执行了1300，当前余额：16600  
胖子执行了800，当前余额：17400  
李四执行了3600，当前余额：21000 //这里使用了一个对象锁，来控制对并发代码的访问。不管运行多少次，执行次序如何，最终余额均为21000，这个结果是正确的。
```

##### 障碍器

> Java5中，添加了障碍器类，为了适应一种新的设计需求，比如一个大型的任务，常常需要分配好多子任务去执行，只有当所有子任务都执行完成时候，才能执行主任务，这时候，就可以选择障碍器了。

```java
import java.util.concurrent.BrokenBarrierException;  
import java.util.concurrent.CyclicBarrier;  
   
/** 
 * Java线程：新特征-障碍器 
 */  
public class Test {  
    public static void main(String[] args){  
       //创建障碍器，并设置MainTask为所有定数量的线程都达到障碍点时候所要执行的任务(Runnable)  
        CyclicBarrier cb = new CyclicBarrier(7,new MainTask());  
        new SubTask("A", cb).start();  
        new SubTask("B", cb).start();  
        new SubTask("C", cb).start();  
        new SubTask("D", cb).start();  
        new SubTask("E", cb).start();  
        new SubTask("F", cb).start();  
        new SubTask("G", cb).start();  
    }  
}  
//主任务  
class MainTask implements Runnable {  
    public void run() {  
    System.out.println(">>>>主任务执行了！<<<<");  
    }  
}  
//子任务  
class SubTask extends Thread {  
     private String name;  
     private CyclicBarrier cb;  
     SubTask(String name, CyclicBarrier cb) {  
     this.name = name;  
     this.cb = cb;  
     }  
     public void run(){  
     System.out.println("[子任务"+name+"]开始执行了！");  
     for(int i=0;i<999999;i++);//模拟耗时的任务  
     System.out.println("[子任务" + name +"]开始执行完成了，并通知障碍器已经完成！");  
     try {  
             //通知障碍器已经完成  
             cb.await();  
         } catch(InterruptedException e) {  
                e.printStackTrace();  
         } catch(BrokenBarrierException e) {  
                 e.printStackTrace();  
         }  
     }  
}  
//执行结果
[子任务B]开始执行了！  
[子任务A]开始执行了！  
[子任务D]开始执行了！  
[子任务A]开始执行完成了，并通知障碍器已经完成！  
[子任务D]开始执行完成了，并通知障碍器已经完成！  
[子任务C]开始执行了！  
[子任务C]开始执行完成了，并通知障碍器已经完成！  
[子任务F]开始执行了！  
[子任务B]开始执行完成了，并通知障碍器已经完成！  
[子任务E]开始执行了！  
[子任务F]开始执行完成了，并通知障碍器已经完成！  
[子任务G]开始执行了！  
[子任务E]开始执行完成了，并通知障碍器已经完成！  
[子任务G]开始执行完成了，并通知障碍器已经完成！  
>>>>主任务执行了！<<<<  
```

## 7.JVM详解

### 1.java自动管理堆和栈

> 程序员不能直接的设置堆和栈

### 2.操作系统的堆和栈

> 堆（操作系统）：一般由程序员分配释放，若程序员不释放，程序结束时可能由OS回收，分配方式类似于链表。
>
> 栈（操作系统）：由操作系统自动分配释放，存放函数的参数值，局部变量值等。操作方式与数据结构中的栈相类似。

### 3.为什么jvm的内存是分布在操作系统的堆中呢？

> 因为操作系统的栈是操作系统管理的，它随时会被回收，所以如果jvm放在栈中，那java的一个null对象就很难确定会被谁回收了，那gc的存在就一点意义都莫有了，而要对栈做到自动释放也是jvm需要考虑的，所以放在堆中就最合适不过了。

### 4.Jvm和操作系统

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-29_202120.png)

**上图解释：**

**jvm虚拟机位于操作系统的堆中，并且，程序员写好的类加载到虚拟机执行的过程是：当一个classLoder启动的时候，classLoader的生存地点在jvm中的堆，然后它会去主机硬盘上将A.class装载到jvm的方法区，方法区中的这个字节文件会被虚拟机拿来new A字节码()，然后在堆内存生成了一个A字节码的对象，然后A字节码这个内存文件有两个引用一个指向A的class对象，一个指向加载自己的classLoader，**

+ **堆和方法区的区别**

> 方法区存放了类的信息，有类的静态变量、final类型变量、field自动信息、方法信息，处理逻辑的指令集，我们仔细想想一个类里面也就这些东西，而堆中存放是对象和数组，咋一看好像方法区跟堆的作用是一样的。其实呢，
>
> 1，这里就关系到我们平时说的对象是类的实例，是不是有点恍然大悟了？这里的对应关系就是 “方法区--类”  “堆--对象”，以“人”为例就是，堆里面放的是你这个“实实在在的人，有血有肉的”，而方法区中存放的是描述你的文字信息，如“你的名字，身高，体重，还有你的行为，如吃饭，走路等”。
>
> 2，再者我们从另一个角度理解，就是从前我们得知方法区中的类是唯一的，同步的。但是我们在代码中往往同一个类会new几次，也就是有多个实例，既然有多个实例，那么在堆中就会分配多个实例空间内存。

+ **方法区，堆，栈，之前的过程**

> 类加载器加载的类信息放到方法区，--》执行程序后，方法区的方法压如栈的栈顶--》栈执行压入栈顶的方法--》遇到new对象的情况就在堆中开辟这个类的实例空间。（这里栈是有此对象在堆中的地址的）

### 5.java虚拟机的生命周期

> 声明周期起点是当一个java应用main函数启动时虚拟机也同时被启动，而只有当在虚拟机实例中的所有非守护进程都结束时，java虚拟机实例才结束生命。

### 6.JVM与main方法的关系

> main函数就是一个java应用的入口，main函数被执行时，java虚拟机就启动了。启动了几个main函数**就启动了几个java应用，同时也启动了几个java的虚拟机。**

### 7.JVM的两种线程

> 一种叫叫守护线程，一种叫非守护线程（也叫普通线程），main函数就是个非守护线程，虚拟机的gc就是一个守护线程。java的虚拟机中，只要有任何非守护线程还没有结束，java虚拟机的实例都不会退出，所以即使main函数这个非守护线程退出，但是由于在main函数中启动的匿名线程也是非守护线程，它还没有结束，所以jvm没办法退出

### 8.JVM的gc

> （垃圾回收机制）就是一个典型的守护线程

### 9.jvm声明周期实例

```java
public class MianAndThread{
    public static void main( String args[]){
        new Thread(new Runnable(){
                    @override
                    public void run(){
                        Thread.currendThread.sleep(5000s);
                        System.out.println("睡了5s后打印,这是出main之外的非守护线程，这个推出后这个引用结束，jvm声明周期结束。任务管理的java/javaw.exe进程结束"
                    }
        }
        System.out.println("mian线程直接打印，mian线程结束，电脑任务管理器的java/javaw.exe进程并没有结束。")
    }   
}
```

### 10.GC垃圾回收机制

> GC垃圾回收机制不是创建的变量为空是就被立刻回收，而是超出变量的**作用域**后就被自动回收。

### 11.程序在jvm运行的流程

> 首先，当一个程序启动之前，它的class会被类装载器装入方法区(不好听，其实这个区我喜欢叫做Permanent区)，执行引擎读取方法区的字节码自适应解析，边解析就边运行（其中一种方式），然后pc寄存器指向了main函数所在位置，虚拟机开始为main函数在java栈中预留一个栈帧（每个方法都对应一个栈帧），然后开始跑main函数，main函数里的代码被执行引擎映射成本地操作系统里相应的实现，然后调用本地方法接口，本地方法运行的时候，操纵系统会为本地方法分配本地方法栈，用来储存一些临时变量，然后运行本地方法，调用操作系统APIi等等

### 12.OutOfMemoryError异常

> 根据Java虚拟机规范的规定，如果方法区的内存空间不能满足内存分配需要时，将抛出OutOfMemoryError异常。

### 13.jvm的结构图

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-29_215426.png)

> 方便理解可把上图分为“功能区”和"数据区”（好好理解功能和数据的含义（一动一静））：参考下面13.1，功能区：垃圾回收系统、类加载器、执行引擎；数据区：也就是整个运行时数据区；

### 14. jvm内部执行运行流程图

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-29_222547.png)

### 15.jvm结构图各模块的生命周期总结

> 对13,14 中的结构图，做一下统计，启动一个jvm虚拟机程序就是启动了一个进程。启动的同时就在操作系统的堆内存中开辟一块jvm内存区，对于13图中各个小模块的声明周期：
>
> **虚拟机栈、本地方法栈、程序计数器这三个模块是线程私有的**，有多少线程就有多少个这三个模块，声明周期跟所属线程的声明周期一致。以程序计数器为例，因为多线程是通过线程轮流切换和分配执行时间来实现，所以当线程切回到正确执行位置，每个线程都有独立的程序计数器，各个线程之间的计数器互不影响，独立存储。其余是跟JVM虚拟机的生命周期一致。
>
> 程序计数器模块是JVM内存区域唯一不会报outofMemoryError情况的区域

### 16.JVM内存包含的**两个子系统**和**两个组件**

> 结合13图，我们总结出JVM内存包含**两个子系统**和**两个组件**，两个子系统是：ClassloaderSubsystem(**类加载器子系统**)和Executionengine(**执行引擎**)子系统；两个组件分别是：Runtimedataarea(**运行时数据区域**)组件和Nativeinterface(**本地库接口**)组件。
>
> 从图中可以看出运行时数据区域包含5部分：**方法区，堆，虚拟机栈，本地方法栈，程序计数器**

### 17.本地库接口和本地方法库

> （1）本地方法库接口：即操作系统所使用的编程语言的方法集，是归属于操作系统的。
>
> （2）本地方法库保存在动态链接库中，即.dll(windows系统)文件中，格式是各个平台专有的。
>
>   (3）个人感觉上图的本地库接口有点多余，以下面代码为例：

```java
class Calc
{
        static{
                System.loadLibrary("Calc");//加载c语言库（本地方法库）直接与操作系统平台交互
        }
 
        public static native int add(int a, int b);
 
        public static void main(String[] args)
        {
                System.out.println(add(11,23));
        }
}
```

+ 对应的C代码

```c

#include <stdio.h>
#include "Calc.h"
 
/* jint 对应着java 的int类型  */
JNIEXPORT jint JNICALL Java_Calc_add(JNIEnv *env, jclass jc, jint a, jint b)
{
        jint ret = a + b;
        return ret;
}
```

> **在java代码中会通过System.loadLibrary("")加载c语言库（本地方法库）直接与操作系统平台交互。**

### 18.双亲委派机制

> JVM在加载类时默认采用的是**双亲委派**机制。通俗的讲，就是某个特定的类加载器在接到加载类的请求时，首先将加载任务委托给父类加载器，依次递归，如果父类加载器可以完成类加载任务，就成功返回；只有父类加载器无法完成此加载任务时，才自己去加载。
>
> 当`jvm`要加载`Test.class`的时候
>
> （1）首先会到自定义加载器中查找（其实是看运行时数据区的方法区有没有加载），看是否已经加载过，如果已经加载过，则返回字节码。
>
> （2）如果自定义加载器没有加载过，则询问上一层加载器(即`AppClassLoader`)是否已经加载过`Test.class`。
>
> （3）如果没有加载过，则询问上一层加载器（`ExtClassLoader`）是否已经加载过。
>
> （4）如果没有加载过，则继续询问上一层加载（`BoopStrap ClassLoader`）是否已经加载过。
>
> （5）如果`BoopStrap ClassLoader`依然没有加载过，则到自己指定类加载路径下（"`sun.boot.class.path`"）查看是否有`Test.class`字节码，有则返回，没有通知下一层加载器`ExtClassLoader`到自己指定的类加载路径下（`java.ext.dirs`）查看。
>
> （6）依次类推，最后到自定义类加载器指定的路径还没有找到`Test.class`字节码，则抛出异常`ClassNotFoundException`。

```java

protected Class<?> loadClass(String name, boolean resolve)
        throws ClassNotFoundException
    {
        synchronized (getClassLoadingLock(name)) {
            // 首先，检查是否已经加载过
            Class<?> c = findLoadedClass(name);
            if (c == null) {
                long t0 = System.nanoTime();
                try {
                    if (parent != null) {
                        //父加载器不为空,调用父加载器的loadClass
                        c = parent.loadClass(name, false);
                    } else {
                        //父加载器为空则,调用Bootstrap Classloader
                        c = findBootstrapClassOrNull(name);
                    }
                } catch (ClassNotFoundException e) {
                    // ClassNotFoundException thrown if class not found
                    // from the non-null parent class loader
                }
 
                if (c == null) {
                    // If still not found, then invoke findClass in order
                    // to find the class.
                    long t1 = System.nanoTime();
                    //父加载器没有找到，则调用findclass
                    c = findClass(name);
 
                    // this is the defining class loader; record the stats
                    sun.misc.PerfCounter.getParentDelegationTime().addTime(t1 - t0);
                    sun.misc.PerfCounter.getFindClassTime().addElapsedTimeFrom(t1);
                    sun.misc.PerfCounter.getFindClasses().increment();
                }
            }
            if (resolve) {
                //调用resolveClass()
                resolveClass(c);
            }
            return c;
        }
    }
```

> 为什么要使用这种加载方式呢？这里要注意几点，1，类加载器代码本身也是java类，因此类加载器本身也是要被加载的，因此显然必须有第一个类加载器不是Java类，这就是`bootStrap`，是使用c++写的其他这是java了。2，虽说`bootStrap`、`extclassLoader`、`appclassloader`三个是父子类加载器关系，但是并没有使用继承，而是使用了组合关系。3，优点，具备了一种带优先级的层次关系，越是基础的类，越是被上层的类加载器进行加载，可以比较笼统的说像`jdk`自带的几个jar包肯定是位于最顶级的，再就是我们引用的包，最后是我们自己写的，保证了java程序的稳定性。

### 19.jdk，jre，JVM的关系

> JDK(Java Development Kit) 是 Java 语言的软件开发工具包([SDK](http://baike.baidu.com/view/429424.htm))。**在JDK的安装目录下有一个`jre`目录**，里面有两个文件夹bin和lib，在这里可以认为**bin里的就是`jvm`，lib中则是`jvm`工作所需要的类库，而`jvm`和 lib合起来就称为`jre`。**

+ `jdk`，`jre`，JVM的关系图

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-30_110712.png)

### 20.JVM运行简易过程

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-30_111751.png)

> 上图左半部分其实不是在JVM中，程序员在eclipse上写的是.java文件，经过编译成.class文件（比如maven工程需要maven install，打成jar报，jar包里面都是`.calss`文件）；这些步骤都是在eclipse上进行的。然后类加载器（`classloader`）一直到解释器是属于JVM的

### 21.JVM结构图各模块

#### 程序计数器

> （Program Counter Register）:也叫**PC寄存器**，是一块较小的内存空间，它可以看做是当前线程所执行的字节码的行号指示器。在虚拟机的概念模型里，字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令、分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。，（1），区别于计算机硬件的pc寄存器，两者不略有不同。计算机用pc寄存器来存放“伪指令”或地址，而相对于虚拟机，pc寄存器它表现为一块内存(一个字长，虚拟机要求字长最小为32位)，虚拟机的pc寄存器的功能也是存放伪指令，更确切的说**存放的是将要执行指令的地址**。
>
> （2）当虚拟机正在执行的方法是一个本地（native）方法的时候，`jvm`的pc寄存器存储的值是undefined。
>
> （3）程序计数器是线程私有的，它的生命周期与线程相同，每个线程都有一个。
>
> （4）此内存区域是唯一一个在Java虚拟机规范中没有规定任何`OutOfMemoryError`情况的区域。

#### JVM栈`JVMStack`

> （1）线程私有的，它的生命周期与线程相同，每个线程都有一个。
>
> （2）每个线程创建的同时会创建一个JVM栈，JVM栈中每个**栈帧存放的为当前线程中局部基本类型的变量**（java中定义的八种基本类型：`boolean、char、byte、short、int、long、float、double`；和reference （32 位以内的数据类型，具体根据JVM位数（64为还是32位）有关，因为一个`solt`(槽）占用32位的内存空间 ）、部分的返回结果，非基本类型的对象在JVM栈上仅存放一个指向堆上的地址；
>
> （3）**每一个方法从被调用直至执行完成的过程就对应着一个栈帧在虚拟机栈中从入栈到出栈的过程**。
>
> （4）栈运行原理：**栈中的数据都是以栈帧（Stack Frame）的格式存在**，栈帧是一个内存区块，是一个数据集，是一个有关方法和运行期数据的数据集，**当一个方法A被调用时就产生了一个栈帧F1**，并被压入到栈中，A方法又调用了B方法，于是产生栈帧F2也被压入栈，B方法又调用了C方法，于是产生栈帧F3也被压入栈…… 依次执行完毕后，先弹出后进......F3栈帧，再弹出F2栈帧，再弹出F1栈帧。
>
> （5）JAVA虚拟机栈的最小单位可以理解为一个个栈帧，**一个方法对应一个栈帧**，一个栈帧可以执行很多指令，如下图：

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-30_142149.png)

> （7）对上图中的动态链接解释下，比如当出现main方法需要调用method1()方法的时候，操作指令就会触动这个动态链接就会找到方法区中对应的method1(),然后把method1()方法压入虚拟机栈中，执行method1栈帧的指令；此外如果指令表示的代码是个常量，这也是个动态链接，也会到方法区中的运行时常量池找到类加载时就专门存放变量的运行时常量池的数据。

#### 本地方法栈`NativeMethodStack`

> （1）先解释什么是本地方法：`jvm`中的本地方法是指方法的修饰符是带有native的但是方法体不是用java代码写的一类方法，这类方法存在的意义当然是填补java代码不方便实现的缺陷而提出的。案例介绍将在 下面22知识点仔细介绍。
>
> （2）作用同java虚拟机栈类似，区别是：虚拟机栈为虚拟机执行Java方法服务，而本地方法栈则是**为虚拟机使用到的Native方法服务**。
>
> （3）是线程私有的，它的生命周期与线程相同，每个线程都有一个。

#### Java 堆`JavaHeap`

> （1）是Java虚拟机所管理的**内存中最大的一块**。
>
> （2）不同于上面3个，**堆是`jvm`所有线程共享的**。
>
> （3）在虚拟机启动的时候创建。
>
> （4）唯一目的就是**存放对象实例**，几乎所有的对象实例以及数组都要在这里分配内存。
>
> （5）**Java堆是GC的主要区域**。
>
> （6）因此很多时候java堆也被称为“GC堆”（Garbage Collected Heap）。从内存回收的角度来看，由于现在收集器基本都采用分代收集算法，所以Java堆还可以细分为：新生代和老年代；新生代又可以分为：Eden 空间、From Survivor空间、To Survivor空间。（23知识点详细介绍）
>
> （7）java堆是计算机物理存储上不连续的、逻辑上是连续的，也是大小可调节的（通过`-Xms`和`-Xmx`控制）。
>
> （8）如果在堆中没有内存完成实例的分配，并且堆也无法再扩展时，将会抛出`OutOfMemoryError`异常。

#### 方法区`Methodarea`

> （1）在虚拟机启动的时候创建。
>
> （2）所有jvm线程共享。
>
> （3）除了和堆一样不需要不连续的内存空间和可以固定大小或者可扩展外，还可以选择不实现垃圾收集。
>
> （4）被装载的class的信息存储在`Methodarea`的内存中。当虚拟机装载某个类型时，它使用类装载器定位相应的class文件，然后读入这个class文件内容并把它传输到虚拟机中。
>
> （5）用于存放已被虚拟机加载的类信息、常量、静态变量、以及编译后的方法实现的二进制形式的机器指令集等数据。
>
> （6）运行时常量池（Runtime Constant Pool）是方法区的一部分。Class文件中除了有类的版本、字段、方法、接口等描述信息外，还有一项信息是常量池（Constant Pool Table），用于存放编译期生成的各种字面量和符号引用，这部分内容将在类加载后进入方法区的运行时常量池中存放。
>
> 方法区补充：指令集是个非常重要概念，因为程序员写的代码其实在`jvm`虚拟机中是被转成了一条条指令集执行的，看下图

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-01_195554.png)

> 首先看看上面各部位位于13图中的那些位置：左侧的foo代码是指令集，可见就是在方法区，程序计数器就不用说了，局部变量区位于虚拟机栈中，右侧最下方的求值栈（也就是操作数栈）我们从动图中明显可以看出存在栈顶这个关键词因此也是位于java虚拟机栈的。
>
> 另外，图中，指令是Java代码经过`javac`编译后得到的JVM指令，PC寄存器指向下一条该执行的指令地址，局部变量区存储函数运行中产生的局部变量，栈存储计算的中间结果和最后结果。
>
> 上图的执行的源代码是：

```java

public class Demo {
 
    public static void foo() {
 
       int a = 1;
 
       int b = 2;
 
       int c = (a + b) * 5;
 
    }
 
}
```

> ​        下面简单解释下执行过程，注意：偏移量的数字只是简单代表第几个指令哦，首先常数1入栈，栈顶元素就是1，然后**栈顶元素移入局部变量区存储**，常数2入栈，栈顶元素变为2，然后栈顶元素移入局部变量区存储；接着1，2依次再次入栈，弹出栈顶两个元素相加后结果入栈，将5入栈，栈顶两个元素弹出并相乘后结果入栈，然后栈顶变为15，最后移入局部变量。**执行return命令如果当前线程对应的栈中没有了栈帧**，**这个Java栈也将会被JVM撤销。**

+ **八大基本类型的在栈中的存放位置**

> 我们平时所说的八大基本类型的在栈中的存放位置是：**运行时数据区--》虚拟机栈--》虚拟机栈的一个栈帧--》栈帧中的局部变量表**；局部变量表存放的数据除了八大基本类型外，还可以存放一个局部变量表的容量的最小单位变量槽（slot）的大小，通常表示为reference;所以是可以放字符串类型的，但是要以 String a="aa";的形式出现，如果是new Object()那就只能实在哎堆中了，**栈里面存的是栈执行堆的地址**。

+ **方法区的内容是一次把一个工程的所有类信息都加载进去再去执行还是边加载边执行呢？**

> 其实单从性能方面也能猜测到是只加载当前使用的类，也就是边加载边执行。例如我们使用tomcat启动一个spring工程，通常启动过程中会加载数据库信息，配置文件中的拦截器信息，service的注解信息，一些验证信息等，其中的类信息就会率先加载到方法区。但如果我们想让程序启动的快一点就会设置懒加载，把一些验证去掉，如一些类信息的加载等真正使用的时候再去加载，这样说明了方法区的内容可以先加载进去，也可以在使用到的时候加载。

#### 类加载器子系统（class loader subsystem）

> (1)根据给定的全限定名类名(如`java.lang.Object`)来装载class文件的内容到`Runtime data area`中的`methodarea`(方法区域)。Java程序员可以extends `java.lang.ClassLoade`r类来写自己的`Classloader`。
>
> (2) 对（1）中的加载过程是：当一个`classloader`启动时，`classloader`的生存地点在`jvm`中的堆，然后它去主机硬盘上去装载`A.class`到`jvm`的`methodarea`(方法区),方法区中的这个字节文件会被虚拟机拿来new A字节码，然后在堆内存生成了一个A字节码的对象，然后A自己码这个内存文件有两个引用，一个指向A的class对象，一个指向加载自己的`classloader`。见下图：

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-01_210947.png)

#### 执行引擎`Executionengine`子系统

> (1)负责执行来自**类加载器子系统（class loader subsystem）中**被加载类中在方法区包含的指令集，通俗讲就是类加载器子系统把代码逻辑（什么时候该if，什么时候该相加，相减）都以指令的形式加载到了方法区，执行引擎就负责执行这些指令就行了。

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-01_214916.png)

> (1)**程序在JVM主要执行的过程是执行引擎与运行时数据区不断交互的过程**，可理解为上面“方法区中的动图”
>
> （2）但是执行引擎拿到的方法区中的指令还是人能够看懂的，这里**执行引擎的工作就是要把指令转成JVM执行的语言**（也可以理解成操作系统的语言），最后操作系统语言再转成计算机机器码。
>
> （3）
>
> **解释器**：一条一条地读取，解释并且执行字节码指令。因为它一条一条地解释和执行指令，所以它可以很快地解释字节码，但是执行起来会比较慢。这是解释执行的语言的一个缺点。字节码这种“语言”基本来说是解释执行的。
> **即时(Just-In-Time)编译器**：即时编译器被引入用来弥补解释器的缺点。执行引擎首先按照解释执行的方式来执行，然后在合适的时候，即时编译器把整段字节码编译成本地代码。然后，执行引擎就没有必要再去解释执行方法了，它可以直接通过本地代码去执行它。执行本地代码比一条一条进行解释执行的速度快很多。编译后的代码可以执行的很快，因为本地代码是保存在缓存里的。
>
> 上图的解释，这里的**字节码解释器也就对应20中的解释器**。简单理解`jit`就是当代码中某些方法复用次数比较高的，并超过一个特定的值就成为了“热点代码”。那么这个这些热点代码就会被编译成本地代码（其实可以理解成缓存）加快访问速度。

### 22.本地方法`nativeMethod`

> （1）本地方法就是带有native标识符修饰的方法；
>
> （2）native修饰符修饰的方法并不提供方法体，但因为其实现体是由非java代码在在外部实现的，因此不能与abstract连用；
>
> （3）存在的意义：不方便用java语言写的代码，使用更为专业的语言写更合适；甚至有些JVM的实现就是用c编写的，所以只能使用c来写，
>
> （4）更多的本地方法最好是与`jdk`的执行引擎的解释器语言一致（执行引擎、解释器：**参考21的执行引擎**）；
>
> （5）Windows、Linux、UNIX、[Dos操作系统](https://www.baidu.com/s?wd=Dos操作系统&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)的核心代码大部分是使用C和C＋＋编写，底层接口用汇编编写．
>
> （6）**为什么native方法修饰的修饰的方法PC程序计数器为undefined**。读懂上面的所有知识点可以就很容易自己理解了。在一开始类加载时，native修饰的方法就被保存在了本地方法栈中，当需要调用native方法时，调用的是一个指向本地方法栈中某方法的地址，然后执行方法直接与操作系统交互，返回运行结果。整个过程并没有经过执行引擎的解释器把字节码解释成操作系统语言，PC计数器也就没有起作用。

### 23.GC垃圾回收机制

> 了解堆内存:
>
> 类加载器读取了类文件后，需要把类、方法、常变量放到堆内存中，以方便执行器执行，堆内存分为三部分

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-01_222945.png)

+ **新生区**

>  **新生区是类的诞生、成长、消亡的区域**，一个类在这里产生，应用，最后被垃圾回收器收集，结束生命。新生区又分为两部分：伊甸区（Eden space）和幸存者区（Survivor pace），**所有的类都是在伊甸区被new出来的**。幸存区有两个：0区（Survivor 0 space）和1区（Survivor 1 space）。当伊甸园的空间用完时，程序又需要创建对象，JVM的垃圾回收器将对伊甸园进行垃圾回收（Minor GC）,将伊甸园中的剩余对象移动到幸存0区。若幸存0区也满了，再对该区进行垃圾回收，然后移动到1区。那如果1去也满了呢？再移动到养老区。若养老区也满了，那么这个时候将产生`Major GC（FullGCC）`，进行养老区的内存清理。若养老区执行Full GC 之后发现依然无法进行对象的保存，就会产生OOM异常`OutOfMemoryError`。
>
> 如果出现`java.lang.OutOfMemoryError: Java heap space`异常，说明Java虚拟机的堆内存不够。原因有二：
>
> a. Java虚拟机的堆内存设置不够，可以通过参数`-Xms、-Xmx`来调整。
>
> b. 代码中创建了大量大对象，并且长时间不能被垃圾收集器收集（存在被引用）。

+ **养老区**

> 养老区用于保存从新生区筛选出来的 JAVA 对象，一般池对象都在这个区域活跃。

+ **永久区**

> 永久存储区是一个常驻内存区域，用于存放JDK自身所携带的 Class,Interface 的元数据，也就是说它存储的是运行环境必须的类信息，被装载进此区域的数据是不会被垃圾回收器回收掉的，关闭 JVM 才会释放此区域所占用的内存。
>
>  如果出现`java.lang.OutOfMemoryError: PermGen space`，说明是Java虚拟机对永久代Perm内存设置不够。原因有二：
>
> a. 程序启动需要加载大量的第三方jar包。例如：在一个Tomcat下部署了太多的应用。
>
> b. 大量动态反射生成的类不断被加载，最终导致Perm区被占满。
>
> 说明：
>
>    Jdk1.6及之前：常量池分配在永久代 。
>
>    Jdk1.7：有，但已经逐步“去永久代” 。
>
>    Jdk1.8及之后：无(`java.lang.OutOfMemoryError: PermGen space`,这种错误将不会出现在JDK1.8中)。

+ **堆内存大小**

> 堆内存大小-Xms -Xmx设置相同，因为-Xmx越大tomcat就有更多的内存可以使用，这就意味着JVM调用垃圾回收机制的频率就会减少（垃圾回收机制被调用是jvm内存不够时自动调用的）可以避免每次垃圾回收完成后JVM重新分配内存。

+ **GC具体什么时候执行**

> 这个是由系统来进行决定的，是无法预测的

### 24.运行时数据区各个模块协作工作的总结

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_095206.png)

+ 先执行main方法

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_095656.png)

+ 当要调用其他方法时

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_102117.png)

### 25.java代码编译（Java　Compiler）过程

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_104816.png)

+ 源代码就是.java文件，JVM字节码就是.class文件
+ 是先加载字节码文件还是先执行main方法?

> 先加载字节码文件到方法区，然后在找到main执行程序。

+ java被编译成了class文件，JVM怎么从硬盘上找到这个文件并装载到JVM里呢？

> 是通过java本地接口（JNI），找到class文件后并装载进JVM，然后找到main方法，最后执行。

### 26.永久代

```java
Student s = new Student("小明"，18);
 
//s 是指针，存放在栈中。
 
new Student("小明"，18) 是对象 ，存放在堆中。
 
//Student 类的信息存放在方法区。
 
//总结 ：对象的实例保存在堆上，对象的元数据（instantKlass）保存在方法区，对象的引用保存在栈上。
```

> 类加载是会先看方法区有没有已经加载过这个类，因此方法区中的类是唯一的。**方法区中的类都是运行时的，都是正在使用的，是不能被GC的**，所以可以理解成永久代。

### 27.Java内存模型

> 读完上面那么多知识点，理解下多线程的一点知识。我们应该知道了**在运行时数据内存区中虚拟机栈、pc寄存器、本地方法栈是每个线程都有的，很明显这些都是独立的不会发生线程不安全的问题**，但是我们平时讨论的线程不安全、要加锁等等情况是怎么回事呢？
>
> 其实，发生线程不安全问题的原因在于cpu，看下图，简单理解cpu

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_115651.png)

> 在CPU内部有一组CPU寄存器，也就是CPU的储存器。CPU操作寄存器的速度要比操作计算机主存快的多。在主存和CPU寄存器之间还存在一个CPU缓存，CPU操作CPU缓存的速度快于主存但慢于CPU寄存器。某些CPU可能有多个缓存层（一级缓存和二级缓存）。计算机的主存也称作RAM，所有的CPU都能够访问主存，而且主存比上面提到的缓存和寄存器大很多。
> 当一个CPU需要访问主存时，会先读取一部分主存数据到CPU缓存，进而在读取CPU缓存到寄存器。当CPU需要写数据到主存时，同样会先flush寄存器到CPU缓存，然后再在某些节点把缓存数据flush到主存。

+ Java内存模型和硬件架构之间的桥接

> ​      正如上面讲到的，Java内存模型和硬件内存架构并不一致。硬件内存架构中并没有区分栈和堆，从硬件上看，不管是栈还是堆，大部分数据都会存到主存中，当然一部分栈和堆的数据也有可能会存到CPU寄存器中，如下图所示，Java内存模型和计算机硬件内存架构是一个交叉关系：

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_115652.png)

+ 当对象和变量存储到计算机的各个内存区域时，必然会面临一些问题，其中最主要的两个问题是：
  1. 共享对象对各个线程的可见性
  2. 共享对象的竞争现象

+ 问题1

> 共享对象的可见性
> 当多个线程同时操作同一个共享对象时，如果没有合理的使用volatile和synchronization关键字，一个线程对共享对象的更新有可能导致其它线程不可见。
>
> 想象一下我们的共享对象存储在主存，一个CPU中的线程读取主存数据到CPU缓存，然后对共享对象做了更改，但CPU缓存中的更改后的对象还没有flush到主存，此时线程对共享对象的更改对其它CPU中的线程是不可见的。最终就是每个线程最终都会拷贝共享对象，而且拷贝的对象位于不同的CPU缓存中。
>
> 下图展示了上面描述的过程。左边CPU中运行的线程从主存中拷贝共享对象obj到它的CPU缓存，把对象obj的count变量改为2。但这个变更对运行在右边CPU中的线程不可见，因为这个更改还没有flush到主存中：

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_115653.png)

> ​      要解决共享对象可见性这个问题，我们可以使用java volatile关键字。 Java’s volatile keyword. volatile 关键字可以保证变量会直接从主存读取，而对变量的更新也会直接写到主存。volatile原理是基于CPU内存屏障指令实现的。

+ 问题2

> 竞争现象
>
> 如果多个线程共享一个对象，如果它们同时修改这个共享对象，这就产生了竞争现象。
> 如下图所示，线程A和线程B共享一个对象obj。假设线程A从主存读取Obj.count变量到自己的CPU缓存，同时，线程B也读取了Obj.count变量到它的CPU缓存，并且这两个线程都对Obj.count做了加1操作。此时，Obj.count加1操作被执行了两次，不过都在不同的CPU缓存中。
>
> 如果这两个加1操作是串行执行的，那么Obj.count变量便会在原始值上加2，最终主存中的Obj.count的值会是3。然而下图中两个加1操作是并行的，不管是线程A还是线程B先flush计算结果到主存，最终主存中的Obj.count只会增加1次变成2，尽管一共有两次加1操作。

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-02_115654.png)

> 要解决上面的问题我们可以使用java synchronized代码块。synchronized代码块可以保证同一个时刻只能有一个线程进入代码竞争区，synchronized代码块也能保证代码块中所有变量都将会从主存中读，当线程退出代码块时，对所有变量的更新将会flush到主存，不管这些变量是不是volatile类型的。

+ volatile和 synchronized区别

> volatile本质是在告诉jvm当前变量在寄存器（工作内存）中的值是不确定的，需要从主存中读取； synchronized则是锁定当前变量，只有当前线程可以访问该变量，其他线程被阻塞住。
>
> volatile仅能使用在变量级别；synchronized则可以使用在变量、方法、和类级别的
>
> volatile仅能实现变量的修改可见性，不能保证原子性；而synchronized则可以保证变量的修改可见性和原子性
>
> volatile不会造成线程的阻塞；synchronized可能会造成线程的阻塞。
>
> volatile标记的变量不会被编译器优化；synchronized标记的变量可以被编译器优化
> 支撑Java内存模型的基础原理

## 8. Java IO 详解

### 1. 概要

#### Java Io 常用的类

| 类                 | 说明           |
| ------------------ | -------------- |
| `File`             | 文件类         |
| `RandomAccessFile` | 随机存取文件类 |
| `InputStream`      | 字节输入流     |
| `OutputStream`     | 字节输出流     |
| `Reader`           | 字符输入流     |
| `Writer`           | 字符输出流     |

> 在整个Java.io包中最重要的就是5个类和一个接口。5个类指的是`File、OutputStream、InputStream、Writer、Reader`；一个接口指的是**Serializable**.掌握了这些IO的核心操作那么对于Java中的IO体系也就有了一个初步的认识了

+ Java I/O主要包括如下几个层次，包含三个部分
  1. **流式部分**――IO的主体部分；
  2. **非流式部分**――主要包含一些辅助流式部分的类，如：File类、`RandomAccessFile`类和`FileDescriptor`等类；
  3. **其他类**--文件读取部分的与安全相关的类，如：`SerializablePermission`类，以及与本地操作系统相关的文件系统的类，如：`FileSystem`类和Win32FileSystem类和`WinNTFileSystem`类。

+ **主要的类如下**
  1. `File`（文件特征与管理）：用于文件或者目录的描述信息，例如生成新目录，修改文件名，删除文件，判断文件所在路径等。
  2.  `InputStream`（二进制格式操作）：抽象类，基于字节的输入操作，是所有输入流的父类。定义了所有输入流都具有的共同特征。
  3. `OutputStream`（二进制格式操作）：抽象类。基于字节的输出操作。是所有输出流的父类。定义了所有输出流都具有的共同特征。
  4. Reader（文件格式操作）：抽象类，基于字符的输入操作。
  5. Writer（文件格式操作）：抽象类，基于字符的输出操作。
  6.  `RandomAccessFile`（随机文件操作）：一个独立的类，直接继承至Object.它的功能丰富，**可以从文件的任意位置进行存取（输入输出）操作**。

+ Java Io 流的体系结构图

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-04_113822.png)

#### 流的概念和作用

>  流：代表任何有能力产出数据的数据源对象或者是有能力接受数据的接收端对象
>
>  流的本质:数据传输，根据数据传输特性将流抽象为各种类，方便更直观的进行数据操作
>
>  流的作用：为数据源和目的地建立一个输送通道
>
>  Java中将输入输出抽象称为流，就好像水管，将两个容器连接起来。流是一组有顺序的，有起点和终点的字节集合，是对数据传输的总称或抽象。即数据在两设备间的传输称为流.
>
>  java的IO是实现输入和输出的基础，可以方便的实现数据的输入和输出操作。在java中把不同的输入/输出源（键盘，文件，网络连接等）抽象表述为“流”(stream)。**流的本质是数据传输，根据数据传输特性将流抽象为各种类，方便更直观的进行数据操作。**

+ **Java IO所采用的模型**

>  Java的IO模型设计非常优秀，它使用Decorator(装饰者)模式，按功能划分Stream，您可以动态装配这些Stream，以便获得您需要的功能。
>
> 例如，您需要一个具有缓冲的文件输入流，则应当组合使用`FileInputStream`和`BufferedInputStream`。 

+ **IO流的分类**

> 根据处理数据类型的不同分为：字符流和字节流
>
> 根据数据流向不同分为：输入流和输出流
>
> 输入流：只能从中读入数据，而不能向其写出数据 
>
> 输出流：只能向其写出数据，而不能向其读入数据
>
> 为什么叫写出和读入，这里涉及到一个方向问题，因为划分输入/输出流时是从程序运行所在的内存的角度来考虑的；将内存中的数据写出到硬盘中的文件，或者是将硬盘中文件的信息读入到内存
>
> java的输入流主要是`InputStream`和`Reader`作为基类，而输出流则是主要由`OutputStream`和`Writer`作为基类。它们都是一些抽象基类，无法直接创建实例。
>
> 按数据来源（去向）分类：
>
> ​     1、`File（文件）： FileInputStream, FileOutputStream, FileReader, FileWriter` 
> ​     2、`byte[]：ByteArrayInputStream, ByteArrayOutputStream` 
> ​     3、`Char[]: CharArrayReader,CharArrayWriter` 
> ​     4、`String:StringBufferInputStream, StringReader, StringWriter` 
> ​     5、`网络数据流：InputStream,OutputStream, Reader, Writer` 

+ ### 字符流和字节流

> 流序列中的数据既可以是未经加工的原始二进制数据，也可以是经一定编码处理后符合某种格式规定的特定数据。因此Java中的流分为两种：
>
> **(1)**  **字节流：**数据流中最小的数据单元是字节
> **(2)**  **字符流：**数据流中最小的数据单元是字符， Java中的字符是Unicode编码，一个字符占用两个字节。
>
> **字符流的由来：** Java中字符是采用Unicode标准，一个字符是16位，即一个字符使用两个字节来表示。为此，JAVA中引入了处理字符的流。因为数据编码的不同，而有了对字符进行高效操作的流对象。本质其实就是基于字节流读取时，去查了指定的码表。

+ **字符流和字节流的区别**

> 节流没有缓冲区，是直接输出的，而字符流是输出到缓冲区的。因此在输出时，字节流不调用`colse()`方法时，信息已经输出了，而字符流只有在调用close()方法关闭缓冲区时，信息才输出。要想字符流在未关闭时输出信息，则需要手动调用flush()方法。
>
> 读写单位不同：字节流以字节（8bit）为单位，字符流以字符为单位，根据码表映射字符，一次可能读多个字节。
>
> 处理对象不同：字节流能处理所有类型的数据（如图片、`avi`等），而字符流只能处理字符类型的数据。
>
> 结论：**只要是处理纯文本数据，就优先考虑使用字符流。除此之外都使用字节流。**

+ ### 输入流和输出流

> 根据数据的输入、输出方向的不同对而将流分为输入流和输出流。
>
> (1) 输入流
>
> 程序从输入流读取数据源。数据源包括外界(键盘、文件、网络…)，即是将数据源读入到程序的通信通道
>
> (2) 输出流
>
> 程序向输出流写入数据。将程序中的数据输出到外界（显示器、打印机、文件、网络…）的通信通道。
>
> **采用数据流的目的就是使得输出输入独立于设备。**
>
> 输入流( Input  Stream )不关心数据源来自何种设备（键盘，文件，网络）。
> 输出流( Output Stream )不关心数据的目的是何种设备（键盘，文件，网络）。
>
> (3) 特性
>
> 相对于程序来说，输出流是往存储介质或数据通道写入数据，而输入流是从存储介质或数据通道中读取数据，一般来说关于流的特性有下面几点：
>
> 1、先进先出，最先写入输出流的数据最先被输入流读取到。
>
> 2、顺序存取，可以一个接一个地往流中写入一串字节，读出时也将按写入顺序读取一串字节，不能随机访问中间的数据。（`RandomAccessFile`**可以从文件的任意位置进行存取（输入输出）操作**）
>
> 3、只读或只写，每个流只能是输入流或输出流的一种，不能同时具备两个功能，输入流只能进行读操作，对输出流只能进行写操作。在一个数据传输通道中，如果既要写入数据，又要读取数据，则要分别提供两个流。 

+ 节点流和处理流

> 节点流(低级流)：直接与数据源相连，读入或写出。直接使用节点流，读写不方便，为了更快的读写文件，才有了处理流。
>
> 处理流(高级流)和节点流一块使用，在节点流的基础上，再套接一层，套接在节点流上的就是处理流。如`BufferedReader`处理流的构造方法总是要带一个其他的流对象做参数。一个流对象经过其他流的多次包装，称为流的链接。

+ 流的原理刨析

> java IO流共涉及40多个类，这些类看上去很杂乱，但实际上很有规则，而且彼此之间存在非常紧密的联系， Java IO流的40多个类都是从如下4个抽象类基类中派生出来的。
>
> **`InputStream/Reader`: 所有的输入流的基类，前者是字节输入流，后者是字符输入流**
>
> **`OutputStream/Writer`: 所有输出流的基类，前者是字节输出流，后者是字符输出流**
>
> 对于`InputStream`和Reader而言，它们把输入设备抽象成为一个”水管“，这个水管的每个“水滴”依次排列。
>
> 字节流和字符流的处理方式其实很相似，只是它们处理的输入/输出单位不同而已。输入流使用隐式的记录指针来表示当前正准备从哪个“水滴”开始读取，每当程序从`InputStream`或者Reader里面取出一个或者多个“水滴”后，记录指针自定向后移动；除此之外，`InputStream`和Reader里面都提供了一些方法来控制记录指针的移动。
>
> 对于`OutputStream`和Writer而言，它们同样把输出设备抽象成一个”水管“，只是这个水管里面没有任何水滴。
>
> 当执行输出时，程序相当于依次把“水滴”放入到输出流的水管中，输出流同样采用隐示指针来标识当前水滴即将放入的位置，每当程序向 `OutputStream` 或者 Writer 里面输出一个或者多个水滴后，记录指针自动向后移动。
>
> **处理流的功能主要体现在以下两个方面**
>
> 性能的提高：主要以增加缓冲的方式来提供输入和输出的效率
>
> 操作的便捷：处理流可能提供了一系列便捷的方法来一次输入和输出大批量的内容，而不是输入/输出一个或者多个“水滴”

+ ### java输入/输出流体系中常用的流的分类表

| **分类**   | **字节输入流**         | **字节输出流**          | **字符输入流**      | **字符输出流**       |
| ---------- | ---------------------- | ----------------------- | ------------------- | -------------------- |
| 抽象基类   | `InputStream`          | `OutputStream`          | *Reader*            | *Writer*             |
| 访问文件   | `FileInputStream`      | `FileOutputStream`      | `FileReader`        | `FileWriter`         |
| 访问数组   | `ByteArrayInputStream` | `ByteArrayOutputStream` | `CharArrayReader`   | `CharArrayWriter`    |
| 访问管道   | `PipedInputStream`     | `PipedOutputStream`     | `PipedReader`       | `PipedWriter`        |
| 访问字符串 |                        |                         | `StringReader`      | `StringWriter`       |
| 缓冲流     | `BufferedInputStream`  | `BufferedOutputStream`  | `BufferedReader`    | `BufferedWriter`     |
| 转换流     |                        |                         | `InputStreamReader` | `OutputStreamWriter` |
| 对象流     | `ObjectInputStream`    | `ObjectInputStream`     |                     |                      |
| 抽象基类   | `FilterInputStream`    | `FilterOutputStream`    | `FilterReader`      | `FilterWriter`       |
| 打印流     |                        | `PrintStream`           |                     | `PrintWriter`        |
| 推回输入流 | `PushbackInputStream`  |                         | `PushbackReader`    |                      |
| 特殊流     | `DataInputStream`      | `DataOutputStreamn`     |                     |                      |

###  2.IO体系的基类

> 字节流和字符流的操作方式基本一致，只是操作的数据单元不同——字节流的操作单元是字节，字符流的操作单元是字符

`InputStream`和`Reader`是所有输入流的抽象基类，本身并不能创建实例来执行输入，但它们将成为所有输入流的模板，所以它们的方法是所有输入流都可使用的方法。
 **在`InputStream`以及Reader里面都包含如下3个方法**。

1. `int read()`; 从输入流中读取单个字节（相当于从水管中取出一滴水），返回所读取的字节数据（字节数据可直接转换为`int`类型）

2. `int read(byte[] b)`从输入流中最多读取`b.length`个字节的数据，并将其存储在字节数组b中，返回实际读取的字节数

3. `int read(byte[] b,int off,int len);` 从输入流中最多读取`len`个字节的数据，并将其存储在数组b中，放入数组b中时，并不是从数组起点开始，而是从off位置开始，返回实际读取的字节数。

**`InputStream`和Reader**提供的一些移动指针的方法：

+ `void mark(int readAheadLimit);` 在记录指针当前位置记录一个标记（mark）。

+ `boolean markSupported();` 判断此输入流是否支持mark()操作，即是否支持记录标记。

+ void reset(); 将此流的记录指针重新定位到上一次记录标记（mark）的位置。

+ long skip(long n); 记录指针向前移动n个字节/字符。

**`OutputStream`和Writer**的用法也非常相似，两个流都提供了如下三个方法

+ `void write(int c);` 将指定的字节/字符输出到输出流中，其中c即可以代表字节，也可以代表字符。

+ `void write(byte[]/char[] buf);` 将字节数组/字符数组中的数据输出到指定输出流中。

+ `void write(byte[]/char[] buf, int off,int len );` 将字节数组/字符数组中从off位置开始，长度为`len`的字节/字符输出到输出流中。

因为字符流直接以字符作为操作单位，所以Writer可以用字符串来代替字符数组，即以String对象作为参数。Writer里面还包含如下两个方法。

+ `void write(String str);` 将`str`字符串里包含的字符输出到指定输出流中。

+ `void write (String str, int off, int len);` 将`str`字符串里面从off位置开始，长度为`len`的字符输出到指定输出流中。

### 3.IO体系的基类文件流的使用

1. 使用`FileInputStream`读取文件：

```java
 @Test
    public void fileInputStreamTest() throws IOException {
        FileInputStream fis = null;
        try {
            // 创建字节输入流
            fis = new FileInputStream(
                    "D:/test/test.txt");
            // 创建一个长度为1024的竹筒
            byte[] b = new byte[1024];
            
            // 用于保存的实际字节数
            int hasRead = 0;
            // 使用循环来重复取水的过程
            while ((hasRead = fis.read(b)) > 0) {
                // 取出竹筒中的水滴（字节），将字节数组转换成字符串进行输出, 后面的gbk是为了处理中文乱码问题
                System.out.print(new String(b, 0, hasRead, "gbk"));
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            fis.close();
        }
    }
```

> 注：上面程序最后使用了`fis.close()`来关闭该文件的输入流，与JDBC编程一样，程序里面打开的文件IO资源不属于内存的资源，垃圾回收机制无法回收该资源，所以应该显示的关闭打开的IO资源。Java 7改写了所有的IO资源类，它们都实现了`AntoCloseable`接口，因此都可以通过自动关闭资源的try语句来关闭这些IO流。

2. 使用`FileReader`读取文件

```java
@Test
    public void fileReaderTest() throws IOException{
        FileReader fis = null;
        try {
            // 创建字节输入流
            fis = new FileReader("D:/test/test.txt");
            // 创建一个长度为1024的竹筒
            char[] b = new char[1024];
            // 用于保存的实际字节数
            int hasRead = 0;
            // 使用循环来重复取水的过程
            while ((hasRead = fis.read(b)) > 0) {
                // 取出竹筒中的水滴（字节），将字节数组转换成字符串进行输出
                System.out.print(new String(b, 0, hasRead));
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            fis.close();
        }
    }
```

> 可以看出使用`FileInputStream`和`FileReader`进行文件的读写并没有什么区别，只是操作单元不同而且。

3. `FileOutputStream`的用法

```java
@Test
    public void fileOutputStreamTest() throws IOException {
        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {
            // 创建字节输入流
            fis = new FileInputStream("D:/test/test.txt");
            // 创建字节输出流
            fos = new FileOutputStream("D:/test/test2.txt");

            byte[] b = new byte[1024];
            int hasRead = 0;
            
            // 循环从输入流中取出数据
            while ((hasRead = fis.read(b)) > 0) {
                // 每读取一次，即写入文件输入流，读了多少，就写多少。
                fos.write(b, 0, hasRead);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            fis.close();
            fos.close();
        }
    }
```

>  使用java的IO流执行输出时，不要忘记关闭输出流，关闭输出流除了可以保证流的物理资源被回收之外，可能还可以将输出流缓冲区中的数据flush到物理节点中里（因为在执行close（）方法之前，自动执行输出流的flush（）方法）。java很多输出流默认都提供了缓存功能，其实我们没有必要刻意去记忆哪些流有缓存功能，哪些流没有，只有正常关闭所有的输出流即可保证程序正常。

1. 缓冲流的使用（`BufferedInputStream/BufferedReader, BufferedOutputStream/BufferedWriter`）：
   字节缓冲流

```java
@Test
    public void bufferedTest() throws IOException {
        FileInputStream fis = null;
        FileOutputStream fos = null;
        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;
        try {
            // 创建字节输入流
            fis = new FileInputStream("D:/test/test.txt");
            // 创建字节输出流
            fos = new FileOutputStream("D:/test/test3.txt");
            // 创建字节缓存输入流
            bis = new BufferedInputStream(fis);
            // 创建字节缓存输出流
            bos = new BufferedOutputStream(fos);

            byte[] b = new byte[1024];
            int hasRead = 0;
            // 循环从缓存流中读取数据
            while ((hasRead = bis.read(b)) > 0) {
                // 向缓存流中写入数据，读取多少写入多少
                bos.write(b, 0, hasRead);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            bis.close();
            bos.close();
        }
    }
```

> 可以看到使用字节缓存流读取和写入数据的方式和文件流`（FileInputStream,FileOutputStream）`并没有什么不同，只是把处理流套接到文件流上进行读写。
>
> 上面代码中我们使用了缓存流和文件流，但是我们只关闭了缓存流。这个需要注意一下，当我们使用处理流套接到节点流上的使用的时候，只需要关闭最上层的处理就可以了。java会自动帮我们关闭下层的节点流。

### 4.转换流的使用

> 下面以获取键盘输入为例来介绍转换流的用法。java使用System.in代表输入。即键盘输入，但这个标准输入流是`InputStream`类的实例，使用不太方便，而且键盘输入内容都是文本内容，所以可以使用`InputStreamReader`将其包装成`BufferedReader`,利用`BufferedReader`的`readLine()`方法可以一次读取一行内容，如下代码所示:

```java
 public void changeStreamTest(){
        try {
            // 将System.in对象转化为Reader对象
            InputStreamReader reader=new InputStreamReader(System.in);
            //将普通的Reader包装成BufferedReader
            BufferedReader bufferedReader=new BufferedReader(reader);
           String buffer=null;
           while ((buffer=bufferedReader.readLine())!=null){
            // 如果读取到的字符串为“exit”,则程序退出
               if(buffer.equals("exit")){
                   System.exit(1);
               }
               //打印读取的内容
               System.out.print("输入内容："+buffer);
           }
        }catch (IOException e){
            e.printStackTrace();
        }finally {
        }
    }
```

> 上面程序将System.in包装成`BufferedReader,BufferedReader`流具有缓存功能，它可以一次读取一行文本——以换行符为标志，如果它没有读到换行符，则程序堵塞。等到读到换行符为止。运行上面程序可以发现这个特征，当我们在控制台执行输入时，只有按下回车键，程序才会打印出刚刚输入的内容。

### 5.对象流的使用

```java
package com.wang.threads;

import java.io.Serializable;

public class UserTest implements Serializable {
    private static final long serialVersionUID = 6522988290199824802L;
    private String username;
    //transient String password;
    private String password;
    public UserTest(){
    }

    public UserTest(String username, String password) {
        super();
        this.username = username;
        this.password = password;
    }
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "UserTest [username=" + username + ", password=" + password
                + "]";
    }
}
```

+ 写对象

```java
 @Test
    public void objectWriterTest() {
        OutputStream outputStream = null;
        BufferedOutputStream buf = null;
        ObjectOutputStream obj = null;
        try {
            // 序列化文件輸出流
            outputStream = new FileOutputStream("D:/test/test.txt");
            // 构建缓冲流
            buf = new BufferedOutputStream(outputStream);
            // 构建字符输出的对象流
            obj = new ObjectOutputStream(buf);
            // 序列化数据写入
            obj.writeObject(new UserTest("A", "123"));// Person对象
            // 关闭流
            obj.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

+ 读对象

```java
@Test
    public void objectReaderTest() {
        try {
            InputStream inputStream = new FileInputStream("D:/test/test.txt");
            // 构建缓冲流
            BufferedInputStream buf = new BufferedInputStream(inputStream);
            // 构建字符输入的对象流
            ObjectInputStream obj = new ObjectInputStream(buf);
            UserTest tempPerson = (UserTest) obj.readObject();
            System.out.println("UserTest对象为：" + tempPerson);
            // 关闭流
            obj.close();
            buf.close();
            inputStream.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
```

> 使用对象流的一些注意事项
> 1.读取顺序和写入顺序一定要一致，不然会读取出错。
> 2.在对象属性前面加transient关键字，则该对象的属性不会被序列化。

### 6.非流式文件类

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-04_230518.png)

> 从上图定义，File类是Object的直接子类，同时它继承了Comparable接口可以进行数组的排序
>
> File类是对文件系统中文件以及文件夹进行封装的对象，可以通过对象的思想来操作文件和文件夹。File类保存文件或目录的各种元数据信息，包括文件名、文件长度、最后修改时间、是否可读、获取当前文件的路径名，判断指定文件是否存在、获得当前目录中的文件列表，创建、删除文件和目录等方法。 
>
> File类共提供了三个不同的构造函数，以不同的参数形式灵活地接收文件和目录名信息

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-04_231441.png)

+ （1）File (String  pathname) 

  > 例:File  f1=new File("FileTest1.txt"); //创建文件对象f1，f1所指的文件是在当前目录下创建的FileTest1.txt

+   (2)  File (String  parent  ,  String child)

  > 例:File f2=new  File(“D:\\dir1","FileTest2.txt") ;//  注意：D:\\dir1目录事先必须存在，否则异常

+   (3)  File (File   parent  , String child)

  > 例:    File  f4=new File("\\dir3");
  >         File  f5=new File(f4,"FileTest5.txt");  //在如果 \\dir3目录不存在使用f4.mkdir()先创建

+ 一个对应于某磁盘文件或目录的File对象一经创建， 就可以通过调用它的方法来获得文件或目录的属性。  
  1. `public boolean exists( )` 判断文件或目录是否存在
  2. `public boolean isFile( )` 判断是文件还是目录 
  3. `public boolean isDirectory( )` 判断是文件还是目录
  4. `public String getName( )` 返回文件名或目录名
  5. `public String getPath( )` 返回文件或目录的路径
  6. `public long length( )` 获取文件的长度
  7. `public String[ ] list ( )` 将目录中所有文件名保存在字符串数组中返回

+ File类中还定义了一些对文件或目录进行管理、操作的方法，常用的方法有
  1. `public boolean renameTo( File newFile );`   重命名文件
  2. `public void delete( );`  删除文件
  3. `public boolean mkdir( );` 创建目录

```java
 public class FileDemo1 {
 public static void main(String[] args) {
 File file = new File("D:" + File.separator + "test.txt");
 if (file.exists()) {  //如果文件存在
 file.delete();        //删除文件
 } else {
 try {
 file.createNewFile();    //创建新文件
 } catch (IOException e) {
 // TODO Auto-generated catch block
 e.printStackTrace();
            }
        }
     }
 }
```

### 7.BIO　NIO　AIO

+ **Java BIO ：** 同步并阻塞，服务器实现模式为一个连接一个线程，即客户端有连接请求时服务器端就需要启动一个线程进行处理，如果这个连接不做任何事情会造成不必要的线程开销，当然可以通过线程池机制改善。
+ **Java NIO ：** 同步非阻塞，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。
+ **Java AIO(NIO.2) ：** 异步非阻塞，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务器应用去启动线程进行处理，

**BIO、NIO、AIO适用场景分析:**

+ BIO方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4以前的唯一选择，但程序直观简单易理解。
+ NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如**聊天服务器**，并发局限于应用中，编程比较复杂，JDK1.4开始支持。
+ AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如**相册服务器**，充分调用OS参与并发操作，编程比较复杂，JDK7开始支持。

## 9.Java socket详解

### 1.socket的基本通信原理

首先socket 通信是基于TCP/IP 网络层上的一种传送方式，我们通常把TCP和UDP称为传输层。

![](C:\Users\Administrator\Desktop\markdown\images\206633-2d6f4a3abcd59745.png)

> 如上图，在七个层级关系中，我们将的**socket属于传输层**，其中UDP是一种面向无连接的传输层协议。UDP不关心对端是否真正收到了传送过去的数据。如果需要检查对端是否收到分组数据包，或者对端是否连接到网络，则需要在应用程序中实现。UDP常用在分组数据较少或多播、广播通信以及视频通信等多媒体领域。在这里我们不进行详细讨论，这里主要讲解的是基于TCP/IP协议下的socket通信。
>
> **socket是基于应用服务与TCP/IP通信之间的一个抽象**，他将TCP/IP协议里面复杂的通信逻辑进行分装，对用户来说，只要通过一组简单的API就可以实现网络的连接。借用网络上一组socket通信图给大家进行详细讲解：

![](C:\Users\Administrator\Desktop\markdown\images\206633-4b2d8622b6d9d48d.png)

> 首先，服务端初始化`ServerSocket`，然后对指定的端口进行绑定，接着对端口及进行监听，通过调用accept方法阻塞，此时，如果客户端有一个socket连接到服务端，那么服务端通过监听和accept方法可以与客户端进行连接。

### 2.socket通信基本示例

+ 常遇到的第一个问题：客户端发送消息后，服务端无法收到消息。

**服务端**

```java
package com.wang.threads;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerSocketTest {
    public static void main(String[] args) {
        try {
               // 初始化服务端socket并且绑定9999端口
            ServerSocket serverSocket =new ServerSocket(9999);
                 //等待客户端的连接
            Socket socket = serverSocket.accept();
                   //获取输入流
            BufferedReader bufferedReader =new BufferedReader(new InputStreamReader(socket.getInputStream()));
            //读取一行数据
            String str = bufferedReader.readLine();
                 //输出打印
            System.out.println(str);

        }catch (IOException e) {

            e.printStackTrace();

        }
    }
}
```



**客户端**

```java
package com.wang.threads;
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class ClientSocket {
    public static void main(String[] args) {
        try {
            Socket socket =new Socket("127.0.0.1",9999);
 BufferedWriter bufferedWriter =new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
String str="你好，这是我的第一个socket";
bufferedWriter.write(str);
}catch (IOException e) {
            e.printStackTrace();
}
    }
}
```

+ 首先启动服务端`ServerSocketTest`,发现正常，等待客户端的的连接

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-05_211308.png)

+ 然后启动客户端`ClientSocket`发现客户端启动正常后，马上执行完后关闭。同时服务端控制台报错

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-05_211339.png)

+ 启动客户端会造成服务端`ServerSocketTest`报错

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-05_211406.png)

+ **报错原因**

> 解决这个问题我们首先要明白，**socket通信是阻塞的**，他会在以下几个地方进行阻塞。**第一个是accept方法**，调用这个方法后，服务端一直阻塞在哪里，直到有客户端连接进来。**第二个是read方法**，调用read方法也会进行阻塞。通过上面的示例我们可以发现，该问题发生在read方法中。有朋友说是Client没有发送成功，其实不是的，我们可以通debug跟踪一下，发现客户端发送了，并且没有问题。而是发生在服务端中，当服务端调用read方法后，他一直阻塞在哪里，因为客户端没有给他一个标识，告诉是否消息发送完成，所以服务端还在一直等待接受客户端的数据，结果客户端此时已经关闭了，就是在服务端报错：`java.net.SocketException: Connection reset`
>
> 那么理解上面的原理后，我们就能明白，客户端发送完消息后，需要给服务端一个标识，告诉服务端，我已经发送完成了，服务端就可以将接受的消息打印出来。
>
> 通常大家会用以下方法进行进行结束：
>
> `socket.close()` 或者调用`socket.shutdownOutput();`方法。调用这俩个方法，都会结束客户端socket。但是有本质的区别。`socket.close()` 将socket关闭连接，那边如果有服务端给客户端反馈信息，此时客户端是收不到的。而`socket.shutdownOutput()`是将输出流关闭，此时，如果服务端有信息返回，则客户端是可以正常接受的。现在我们将上面的客户端示例修改一下啊，**增加一个标识告诉流已经输出完毕**：

+ 客户端2

```java
package com.wang.threads;
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class ClientSocket {
    public static void main(String[] args) {
        try {
            Socket socket =new Socket("127.0.0.1",9999);
 BufferedWriter bufferedWriter =new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
String str="你好，这是我的第一个socket";
bufferedWriter.write(str);
      //刷新输入流
     bufferedWriter.flush();
     //关闭socket的输出流
     socket.shutdownOutput();
}catch (IOException e) {
            e.printStackTrace();
}
    }
}
```

+ 服务端控制台输出正常

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-05_212652.png)

> 服务端在接受到客户端关闭流的信息后，知道信息输入已经完毕，苏哦有就能正常读取到客户端传过来的数据。通过上面示例，我们可以基本了解socket通信原理，掌握了一些socket通信的基本`api`和方法，实际应用中，都是通过此处进行实现变通的。

### 3.while循环连续接受客户端信息

> 上面的示例中`scoket`客户端和服务端固然可以通信，但是客户端每次发送信息后socket就需要关闭，下次如果需要发送信息，需要socket从新启动，这显然是无法适应生产环境的需要。比如在我们是实际应用中QQ，如果每次发送一条信息，就需要重新登陆QQ，我估计这程序不是给人设计的，那么如何让服务可以连续给服务端发送消息？下面我们通过while循环进行简单展示：

+ 服务器端

```java
package com.wang.threads;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerSocketTest {
    public static void main(String[] args) {

        try {

       // 初始化服务端socket并且绑定9999端口

            ServerSocket serverSocket = new ServerSocket(9999);

       //等待客户端的连接

            Socket socket = serverSocket.accept();

       //获取输入流

       // BufferedReader bufferedReader =new BufferedReader(new      InputStreamReader(socket.getInputStream()));
            BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(socket.getInputStream(), "UTF-8"));

       //读取一行数据
       //String str = bufferedReader.readLine();
       //读取一行数据
            String str;
       //通过while循环不断读取信息，
            while ((str = bufferedReader.readLine()) != null) {
           //输出打印
                System.out.println(str);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

+ 客户端

```java
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
public class ClientSocket {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("127.0.0.1", 9999);
            BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
            //通过标准输入流获取字符流
       BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in, "UTF-8"));
            while (true) {
                String str = bufferedReader.readLine();
                bufferedWriter.write(str);
                bufferedWriter.write("\n");
                bufferedWriter.flush();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

+ 客户端用键盘输入

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-05_215641.png)

+ 服务端输出

![](C:\Users\Administrator\Desktop\markdown\images\2020-05-05_215654.png)

> 大家可以看到，通过一个while 循环，就可以实现客户端不间断的通过标准输入流读取来的消息，发送给服务端。*在这里有个细节，大家看到没有，我客户端没有写`socket.close()` 或者调用`socket.shutdownOutput();`服务端是如何知道客户端已经输入完成了？服务端接受数据的时候是如何判断客户端已经输入完成呢？这就是一个核心点，双方约定一个标识，当客户端发送一个标识给服务端时，表明客户端端已经完成一个数据的载入。*而服务端在结束数据的时候，也通过这个标识进行判断，如果接受到这个标识，表明数据已经传入完成，那么服务端就可以将数据度入后显示出来。
>
>  在上面的示例中，客户端端在循环发送数据时候，每发送一行，添加一个换行标识“\n”标识，在告诉服务端我数据已经发送完成了。而服务端在读取客户数据时，通过`while ((str = bufferedReader.readLine())!=null)`去判断是否读到了流的结尾，负责服务端将会一直阻塞在哪里，等待客户端的输入。
>
>  通过`while`方式，我们可以实现多个客户端和服务端进行聊天。但是，下面敲黑板，划重点。由于socket通信是阻塞式的，假设我现在有A和B俩个客户端同时连接到服务端的上，当客户端A发送信息给服务端后，那么服务端将一直阻塞在A的客户端上，不同的通过`while`循环从A客户端读取信息，此时如果B给服务端发送信息时，将进入阻塞队列，直到A客户端发送完毕，并且退出后，B才可以和服务端进行通信。简单地说，我们现在实现的功能，虽然可以让客户端不间断的和服务端进行通信，与其说是一对一的功能，因为只有当客户端A关闭后，客户端B才可以真正和服务端进行通信，这显然不是我们想要的。 下面我们通过多线程的方式给大家实现正常人类的思维。

### 4.多线程下socket编程

