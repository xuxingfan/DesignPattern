### 问题的提出
在类的应用中，有些类是容易创建对象的，直接调用构造方法即可，例如Student obj=new Student("1001","张三",20); Circle obj1=new Circle(10.0f)这两个类的特点是成员变量是基本类型或者是字符串，或者是封装类。但是有些累是不易直接创建对象的，成员变量是自定义类型，代码如下：

```java
public class Product{
    Unit1 u1;
    Unit2 u2;
    Unit3 u3;
}

```
可以看出，Product有Unit1、Unit2、Unit3三个单元组成，产生Product对象不能简单地有Product obj=new Product(Unit1,Unit2,Unit3)生成，必须先产生具体的对象u1、u2、u3才能获得Product对象，简单的实现如下：

```java
public class Product{
    Unit1 u1;
    Unit2 u2;
    Unit3 u3;
    
    public void createUnit1(){
        //TODO   u1=.....; 
    }
    public void createUnit2(){
        //TODO   u2=.....; 
    }
    public void createUnit3(){
        //TODO   u3=.....; 
    }
    
    public void composite(){
        //u1+u2+u3
    }
}

public class Test{
    public static void main(String []args){
        Product p=new Product();
        p.createUnitl();
        p.createUnit2();
        p.createUnit3();
        p.composite();
    }

}
```

上面的代码虽然解决复制对象的创建问题，层次清晰，但本方法仅解决了一类Product对象的创建问题，如果有多类Product对象，那么代码就会变成如下：

```java
public class Product{
    Unit1 u1;
    Unit2 u2;
    Unit3 u3;
    
    public void createUnit1(){
        //TODO   u1=.....; 
    }
    public void createUnit2(){
        //TODO   u2=.....; 
    }
    public void createUnit3(){
        //TODO   u3=.....; 
    }
    
    public void composite(){
        //u1+u2+u3
    }
    
    
    public void createUnitA1(){
        //TODO   u1=.....; 
    }
    public void createUnitA2(){
        //TODO   u2=.....; 
    }
    public void createUnitA3(){
        //TODO   u3=.....; 
    }
    
    public void compositeA(){
        //u1+u2+u3
    }
}

public class Test{
    public static void main(String []args){
        int type=1;
        Product p=new Product();
        if(type==1){
            p.createUnitl();
            p.createUnit2();
            p.createUnit3();
            p.composite();
        }
        if(tyle==2){
            p.createUnitAl();
            p.createUnitA2();
            p.createUnitA3();
            p.compositeA();
        }
        
    }

}
```
可以看出，随着Product产品种类的增多，必须修改已有的源码。

### 生成器模式
生成器模式也称建造者模式。生成器模式的意图旨在将一个复杂的构建与他的表现形式分离。在软件设计中，面临一个非常复杂的对象构建工作，这个复杂的对象通常可以分成几较小的子对象，但是子对象的创建可能随时面临变化。生成器的思路是产品类和创建产品的类分离，产品类仅一个，创建产品的类有n个。


```java
public class Unit1{
    
}
public class Unit2{
    
}
public class Unit3{
    
}
public class Proudct{
    Unit1 u1;
    Unit2 u2;
    Unit3 u3;
}

```
定义n个生成器Build类

```java
public interface IBuild{
    plubic void createUnit1();
    plubic void createUnit2();
    plubic void createUnit3();
    public Product composite();
}

public class BuildProduct1 implements IBuild{
    Product p=new Product(); 
    
    plubic void createUnit1(){
         //TODO p.u1=....
    }
    plubic void createUnit2(){
         //TODO p.u2=....
    }
    plubic void createUnit3(){
         //TODO p.u3=....
    }
    public Product composite(){
        //p.u1+p.u2+p.u3;
        return p;
    }
}

public class BuildProduct2 implements IBuild{
    Product p2=new Product(); 
    
    plubic void createUnit1(){
         //TODO p2.u1=....
    }
    plubic void createUnit2(){
         //TODO p2.u2=....
    }
    plubic void createUnit3(){
         //TODO p2.u3=....
    }
    public Product composite(){
        //p2.u1+p2.u2+p2.u3;
        return p2;
    }
}

//调度类
public class Director{
    private IBuild build;
    
    public Director(IBuild build){
        this.build=build;
    }
    
    public Product build(){
        build.createUnit1();
        build.createUnit2();
        build.createUnit3();
        return build.composite();
    }
    
    public static void main(String [] args){
        IBuild build=new BuildProduct1();
        Director d=new Director(build);
        Product p=d.build();
        
    }
}
```
通过上面的代码可知，如果需求发生变化时，只需要添加相应的生成器类即可。

### 进一步改进
上面的方法只能构建相同流程(createUnit1,createUnit2,createUnit3)的类，如果需要一个对象的需要3个过程，另一个对象需要4个过程，这时候，我们进一步优化如下：

```java

public interface IBuild{
    public Product create();
}

public class BuildProduct1 implements IBuild{
    Product p=new Product();
    
    plubic void createUnit1(){
         //TODO p2.u1=....
    }
    plubic void createUnit2(){
         //TODO p2.u2=....
    }
    plubic void createUnit3(){
         //TODO p2.u3=....
    }
    public Product composite(){
        //p2.u1+p2.u2+p2.u3;
        return p2;
    }
    
    public Product create(){
        createUnit1();
        createUnit2();
        createUnit3();
        return composite();
    }
    
}

public class BuildProduct2 implements IBuild{
    Product p=new Product();
    
    plubic void createUnit1(){
         //TODO p2.u1=....
    }
    plubic void createUnit2(){
         //TODO p2.u2=....
    }
    plubic void createUnit3(){
         //TODO p2.u3=....
    }
    
     plubic void createUnit4(){
         //TODO p2.u3=....
    }
    
    public Product composite(){
        //p2.u1+p2.u2+p2.u3+u4;
        return p2;
    }
    
    public Product create(){
        createUnit1();
        createUnit2();
        createUnit3();
        createUnit4();
        return composite();
    }
    
}

```
### 进一步思考
可以把IBuild定义成泛型接口，如下面的程序所示，具体生成器就可以生成不仅仅是Product产品

```java
public interface IBuilder<T>{
    public T create();
}

```

## 生成器的另外一种实现方式

```java
public abstract class Product{
    Unit1 u1;
    Unit2 u2;
    Unit3 u3;
    
    abstract void createUnit1();
    abstract void createUnit2();
    abstract void createUnit3();
    abstract void composite();
}

public class BuildProduct1 extends Product{
    void createUnit1(){
         //u1=....
    }
    void createUnit2(){
         //u2=....
    }
    void createUnit3(){
        //u3=....
    }
    void composite(){
        //u1+u2+u3
    }
}

public class Director{
    Product p=;
    
    public Director(Product p){
        this.p=p;
    }
    void build(){
        p.createUnit1();
        p.createUnit2();
        p.createUnit3();
        p.composite();
    }
}

```

总之，对于生成器模式，主要原则是对象的构建过程与表示分离。







