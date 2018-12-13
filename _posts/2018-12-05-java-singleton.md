# 理解JAVA单例模式
 
### **什么是单例模式?**
> 顾名思义, 单例就是保证类单一的唯一的一个实例? 
### **如何保证类的实例是单例?**
> 众所周知Java是面向对象的语言，一个对象要被使用之前需要被正确的实例化，Java中的类就是一个对象，每个类都有构造方法，
> 如果没有显示的为类定义构造方法，则Java编译器会默认提供一个空的构造方法，实例化类有多种方法,经常使用的new关键字创建类的实例其实也就是调用了这个类的空的构造方法;
> 也可以使用Java反射机制、clone方法、将一个对象实例化后，进行序列化，再反序列化等创建类的实例化对象。   
> 下面通过代码理解一下：

		 
	package index;
	/**
 	* 为了直观到new调用类的空构造器
 	* 故此类显式的定义一个空的构造器
 	* 若不显式定义则Java虚拟机会默认提供一个空的构造器
 	*/
	public class Superman {
	    //空的构造器
	    public Superman(){
	        System.out.println("I'm Superman");
	    }
	}

> 测试 
 	   
    package index;
	public class TestSingleton {
	    
	    public static void main(String[] args) {
	        //使用new创建2个Superman的实例对象
	        Superman superman1 = new Superman();
	        Superman superman2 = new Superman();
	        if(superman1==superman2){
	            System.out.println("是该类的同一实例对象");
	        }else {
	            System.out.println("非该类的同一实例对象");
	        }
	    }
	    
	}
		
![](https://i.imgur.com/7tSQ9kF.png)
> 通过上面代码的输出结果,可以说明new了两次Superman这个类；调用了两次它的构造函数，通过条件判断创建的两个实例对象是不同的；也就是说当
> 该类在项目中需要多个地方使用的话,通过new这种方式创建的实例对象是不同的。每次创建对象都需要在内存中进行分配,特别是频繁的创建和销毁对象。  
> 将上面的代码改造一下：
    
     public class Superman {
	    //构造器私有化
	    private Superman(){}
	    //实例化对象
	    private static Superman supermanInstance = new Superman();
	    //获取实例化对象的静态函数getSupermanInstance()
	    public static Superman getSupermanInstance(){
	        return supermanInstance;
	    }
	}    
	
> 测试   
  		 
	package index;
	public class TestSingleton {
			
	    public static void main(String[] args) {
			//因为该类的空的构造器已经private私有化了 所以不能使用new实例化对象
	        //通过该类的实例化对象的静态函数getSupermanInstance()获取该类的实例
	        Superman superman1 = Superman.getSupermanInstance();
	        Superman superman2 = Superman.getSupermanInstance();
	        if(superman1==superman2){
	            System.out.println("是该类的同一实例对象");
	        }else {
	            System.out.println("非该类的同一实例对象");
	        }
	    }
	}    
![](https://i.imgur.com/Hx2gD89.png)

> 上面的这种模式获取一个类的实例对象就是Java设计模式之中的单例模式;两私一公(一个私有构造函数和一个私有的静态实例化对象加一个静态的公开获取实例的方法)，
> 不管需要实例化多少对象都可以保证是该类的唯一实例对象。 
### **为什么要用单例模式?**
> **至于为什么要用单例模式，总结一下优缺点：**   
> 优点  
> 1. 首先肯定是节省内存资源，不管多频繁的通过暴露的方法创建实例，都能保证创建的对象在系统内存中是同一实例对象；    
> 2. 灵活性，由于所有实例的创建都由该类控制，所有该类可以灵活的更改实例化过程
> 3. 实例的受控访问,单例类可以轻松的控制唯一实例的受控访问
> 缺点  
> 1. 


 
