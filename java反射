# 反射
在常规的程序设计中，我们使用类和调用类的方法，都是新建实例，然后通过实例直接调用方法的。
例如：
    

```java
public class A{
    void func(){
    	
    }
    public static void main(String []args){
        A a=new A();
        a.func();
    }
}
```


当我们的类里面有多方法，和字段时，每次要把所有的方法调用一遍，那么上面的实现方式就显得不那么智能了。那么我们是否可以根据类名，列出类里的所有方法，并且调用他们呢。当然可以-反射，在jdk中java.lang.reflect就实现了反射，主要由以下类来实现java反射机制。

- Class类:代表一个类。
- Constructor类:类的构造方法
- Field类：代表类的成员变量（类的属性）
- Method类：代表类的方法。

运用上面4个类，能实现解析系统类和自定义类的结构，并且能够创建对象和执行方法。


```java
public class A{
	int m;
	public A(int m){}
	private void func1(){
	}
	private void func2(){
	}
	public static void main(String []args)throws Exception{
	    Class classInfo=Class.forName("A");
	    System.out.println("类A的构造函数如下所示");
	    Constructor cons[]=classInfo.getConstructors();
	    cons.for....//输出构造方法
	    System.out.println("类A的所有属性如下所示");
	    Filed fileds[]=classInfo.getFileds();
	    fileds.for...//输出类属性
	    System.out.println("类A的所有方法如下所示");
	    Method methods[]=classInfo.getMethods();
	    methods.for...//输出类方法
	}
}
```

TODO

## 构造方法的调用
上面的程序仅仅解析了A类的结构，并没有生成A的实例，下面将用反射机制生成实例

```java
public class A{
    int m;
    String s;
    public A(){};
    public A(int m){
        this.m=m;
    }
    public A(int m,String s){
        this.m=m;
        this.s=s;
    }
    public static void main(String []args){
        Class classInfo=Class.forName("A");
        //方法1
        Constructor cons[]=classInfo.getConstructors();
        cons[2].newInstance();
        cons[1].newInstance(new Object[]{10});
        cons[0].newInstance(new Object[]{"hello",10});
        
        //方法2
        Constructor c=classInfo.getConstructor();
        c.newInstance();
        
        c=classInfo.getConstructor(new Class[]{Integer.class});
        c.newInstance(new Object[]{10});
        
        c=classInfo.getConstructor(new Class[]{String.class,Integer.class});
        c.newInstance(new Object[]{"hello",10});
    }
}
```
从上面的代码可以看出，使用反射机制生成实例有两种方法，一种是通过无参方法getConstructors()获取构造函数数组，分别调用newInstance()方法创建实例，另外一种是通过getConstructor(new Class()[]{参数})获取构造函数，然后调用newInstance()产生实例。加深对getConstructor()的理解，原型定义如下：


```java
public Constructor<T> getConstructor(Class<?>...parameterTypes)
```
注意：在构造方法编译时，类似栈结构，先进后出，所以A()先进栈，对应数据cons[2],以此类推


## 成员方法的调用


```java
public class A{
    int m;
    String s;
    public void func1(){};
    public void func2(int m){
        this.m=m;
    }
    public void func3(int m,String s){
        this.m=m;
        this.s=s;
    }
    public static void main(String []args){
        Class classInfo=Class.forName("A"); 
        Constructor cons=classInfo.getConstructor();
        Object o=cons.newInstance();
        
        Method f1=classInfo.getMethod("func1");
        f1.invoke(obj);
        
        Method f2=classInfo.getMethod("func2",Integer.class);
        f2.invoke(obj,new Object[]{10});
        
        Method f3=classInfo.getMethod("func3",String.class,Integer.class);
        f3.invoke(obj,new Object[]{"hello",10});
       
    }
}
```
方法反射主要是利用Class的getMehtod方法，得到Method对象，然后使用Method的invoke方法完成反射方法的执行。

只要知道类名，方法名称，方法参数值，运用反射机制就能执行方法。

