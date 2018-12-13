---
layout:     post
title:      理解JAVA单例模式
subtitle:   理解JAVA单例模式
date:       2018-12-05
author:     SweetHomicide
header-img: img/homicide/home-bg.jpg
catalog: true
tags:
    - 设计模式
    - 单例模式
    - 线程安全 
---


# 理解JAVA单例模式 
### **什么是单例模式**
> 顾名思义, 单例就是保证类单一的唯一的一个实例? 
### **如何保证类的实例是单例**
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
### **单例模式优缺点**
 
<font color=#0099ff size=3 face="黑体"> 
> 优点  
> 1. 首先肯定是节省内存资源，不管多频繁的通过暴露的方法创建实例，都能保证创建的对象在系统内存中是同一实例对象；    
> 2. 灵活性，由于所有实例的创建都由该类控制，所有该类可以灵活的更改实例化过程  
> 3. 实例的受控访问,单例类可以轻松的控制唯一实例的受控访问

>   缺点  
> 1. 单例模式没有接口，不容易扩展  
> 2. 使用时不能用反射模式创建单例，否则会实例化一个新的对象  
> 3. 使用懒单例模式时注意线程安全问题 
</font>
 
# **实现单例模式的多种方式**

### **饿单例**
	package index;
	public class Superman {
	    //空的构造器
	    private Superman(){}
	    
	    //实例化对象
	    private static Superman supermanInstance = new Superman();
	    
	    //获取实例化对象的静态函数getSupermanInstance()
	    public static Superman getSupermanInstance(){
	        return supermanInstance;
	    }
	}  
> 饿单例在类加载的时候就被提前new了出来，一开始就实例化了一个supermanInstance对象,不管你程序需要不要调用这个对象，它都已经准备好了;
> 没有进行延迟加载，为了减小程序负载大多数情况下需要懒加载,所以这种实现单例的方式不是最佳选择。


### **懒单例**
#### **非线程安全 单线程写法**
	package index;
	public class Superman {
	    //空的构造器
	    private Superman(){}
	
	    //实例化对象;只声明 不使用new进行实例化
	    private static Superman supermanInstance = null;
	
	    //获取实例化对象的静态函数getSupermanInstance()
	    public static Superman getSupermanInstance(){
	        if(supermanInstance==null){ //如果为null的情况再进行实例化
	            supermanInstance = new Superman();
	        }
	        return  supermanInstance;
	    }
	}  
> 声明一个对象不去实例化它，当程序需要实例化的时候调用静态工厂方法 getSupermanInstance(),方法中对声明的对象进行判断，如果是null的话再去实例化它，
> 这种写法可以达到延迟加载的效果，但它是非线程安全的，若在多线程中有两个线程同时调用静态工厂方法 getSupermanInstance() 就有可能重复的创建该类的实例
> 破坏了单例的唯一性；

#### **线程安全 多线程写法**  
	package index;
	public class Superman {
	    //空的构造器
	    private Superman(){}
	
	    //实例化对象;只声明 不使用new进行实例化
	    private static volatile Superman supermanInstance = null;
	
	    //给静态工厂方法加同步锁
	    public static synchronized Superman getSupermanInstance(){
	        if(supermanInstance==null){
	            supermanInstance = new Superman();
	        }
	        return  supermanInstance;
	    }
	}  

> 对非线程安全的代码块进行改造,给其静态工厂方法加同步锁synchronized,如果有多个线程同时调用该方法,其他线程必须等待上一个线程执行完该方法后才可以调用 getSupermanInstance()
> 这个静态工厂函数，所以它是线程安全的,但是这样的写法会导致在多线程中，因为同步锁synchronized机制，当多个线程调用该方法时会排队等待获取锁,才能够调用，因为单例模式只需要实例化一次
> 对象就可以了,所以大多数情况这个对象已经被实例化过,无需在使线程进行等待;针对这样的性能问题可以使用下面的方式进行优化
  
#### **线程安全 多线程写法 双重检查锁(DCL) Double-check lock**    
	package index;
	public class Superman {
	    //空的构造器
	    private Superman(){}
	
	    //实例化对象;只声明 不使用new进行实例化
	    private static volatile Superman supermanInstance = null;
	
	    public static Superman getSupermanInstance(){
	        if(supermanInstance==null){
	            synchronized (Superman.class){  
	                if (supermanInstance == null){
	                    supermanInstance = new Superman();
	                }
	            }
	        }
	        return  supermanInstance;
	    }
	}
	
> 经过改造静态工厂,使其进行双重条件判断实例对象,当两个线程同时调用该方法时无需再进行等待同步锁,也就说可以同时调用这个方法,
> 当都进入第一个条件判断时会碰到同步代码块synchronized (Superman.class)只能有一个先进入执行，先进入的线程会碰到第二个判断，
> 如果为null才会进行实例化,当先进入的线程已经实例化对象后，后来的线程获得同步锁进入到第二个判断，此时supermanInstance这个实例已经
> 被第一个线程创建，所以后来的线程无需在进行new操作，跳出同步块获得第一个线程创建的实例，这样可以有效的提高多线程并发度，因为单例创建一次对象后无需再次创建，所以这种写法既解决了
> 多线程同步等待，也解决了两个线程同时调用会创建多个对象的问题。  

#### **静态内部类实现方式** 
	package index;
	public class Superman {
	    //空的构造器
	    private Superman(){}
	
	    //私有的静态内部类
	    private static class SuperWoman{
	        private static Superman superman = new Superman();
	    }
	
	    public static Superman getSupermanInstance(){
	        //调用内部类里的实例对象
	        return  SuperWoman.superman;
	    }
	}
> 利用静态类只会加载一次的特性，实现单例类的初始化，通过类加载机制保证了该类对象的唯一实例，只有内部类SuperWoman被调用的时候才会加载内部类SuperWoman中的实例对象superman
> 所以这种方式实现的单例模式也属于懒加载 延迟加载 ，且实现方式比较简单。还有一种最简单方式如下 


#### **枚举单例** 
	package index;
	public enum  Superman {
	    INSTANCE;
	    
	}  
> 使用方式 : 直接用枚举类名调用INSTANCE关键字
 		
	package index;
	public class TestSingleton {
	
	    public static void main(String[] args) {
	        Superman superman1 = Superman.INSTANCE;
	        Superman superman2 = Superman.INSTANCE;
	        if(superman1==superman2){
	            System.out.println("是该类的同一实例对象");
	        }else {
	            System.out.println("非该类的同一实例对象");
	        }
	    }
	}

> 这种方式应该是最简单的实现单例模式的方式了,且保证了线程安全、防止使用Java反射机制强行调用构造函数、保证反序列化一些问题。   、


以上就是鄙人对Java单例模式的理解，如有不对的地方望大家急时指出





