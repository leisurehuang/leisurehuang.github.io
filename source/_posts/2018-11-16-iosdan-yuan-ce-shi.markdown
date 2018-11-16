---
layout: post
title: "iOS单元测试"
date: 2018-11-16 16:57:33 +0800
comments: true
categories: iOS
---
### 什么是单元测试？
**单元测试**（unit testing），是指对软件中的最小可测试单元进行检查和验证。是用来对一个模块、一个函数或者一个类来进行正确性检验的测试工作

### 为什么要做单元测试：
- 单元测试的成本更低。
- 重构的有效保证




### 原则：

#### 1，Tests One thing
- Single “Unit” of functionality
Pass/Fail
小, 快, 独立

#### 不测什么
UI, system, framework, library
File, Network, DB

#### 测什么？
- Business Logic  
    验证结果是否正确
    验证边界条件和异常情况

- API Logic（对外提供的接口，而非网络API）


#### 怎么写？
- 使用XCTest框架
- 使用 **Give When Than** 进行条件，执行，验证。

代码：

		class FirstViewController: UIViewController {
   			var nilObject:String?
   		
    		override func viewDidLoad() {
        		super.viewDidLoad()
    		}

    		func actionInt() ->Int{
       	 return 11
    		}
    
    		func actionString() ->String{
        		return "hello"
    		}
    
    		func actionBool() ->Bool{
       	 return true
    		}
    	}
    	
 测试方法：   	

    	func testActionIntMethod() {
        	let i = FirstViewController().actionInt()
        	XCTAssertEqual(i, 11)
        	XCTAssert(i == 11, "the int number is 11")
    	}
    	
    	func testActionStringMethod() {
        	let str = FirstViewController().actionString()
        	XCTAssertEqual(str, "hello")
        	XCTAssert(str == "hello", "the string is hello")
	    }
    
    	func testActionBoolMethod() {
        	let bol = FirstViewController().actionBool()
        	XCTAssertEqual(bol, true)
    	}
    
   		func testFirstViewControllerInit() {
        	let vc = FirstViewController()
       	XCTAssertNotNil(vc)
   	 	}
   	 	
    	func testFirstViewControllerObjectInit() { 
        	let nilObject = FirstViewController().nilObject
        	XCTAssertNil(nilObject)
    	}




### 从MVC -> MVVM

- MVC结构中，将所有的业务和处理逻辑堆积在ViewController中，而进行单元测试书写时，界面的显示效果，网络处理的结果，都成了测试输入的条件。
- 而MVVM中，界面刷新，服务调用，对象模型，都被抽离到单独的模块，ViewModel中，仅保留单纯的逻辑代码，通过Mock对对象模型等的模拟，可以很清爽的进行测试的书写和验证。




### 为什么使用Quick& Nimble

- **BDD**行为驱动开发是一种敏捷软件开发的技术  
- 在书写性和可读性上更好，容易进行测试结果的验证查看

具体请看[官方介绍](https://github.com/Quick/Nimble)


Demo:[地址](https://github.com/leisurehuang/UnitTestForSwift)

### 测试结果的可视化
使用命令行：

    xcodebuild test -scheme UnitTestForSwift -destination name="iPhone 6" -configuration Debug | tee xcodebuild.log | xcpretty -t -r html --output ./report.html