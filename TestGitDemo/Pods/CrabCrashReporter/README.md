# CrabCrashReporter

[![CI Status](http://img.shields.io/travis/Fu Mingxin/CrabCrashReporter.svg?style=flat)](https://travis-ci.org/Fu Mingxin/CrabCrashReporter)
[![Version](https://img.shields.io/cocoapods/v/CrabCrashReporter.svg?style=flat)](http://cocoapods.org/pods/CrabCrashReporter)
[![License](https://img.shields.io/cocoapods/l/CrabCrashReporter.svg?style=flat)](http://cocoapods.org/pods/CrabCrashReporter)
[![Platform](https://img.shields.io/cocoapods/p/CrabCrashReporter.svg?style=flat)](http://cocoapods.org/pods/CrabCrashReporter)

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.


## Installation

CrabCrashReporter is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "CrabCrashReporter"
```

## How To Use

Just #import the CrabCrashReporter/CrabCrashReport.h in AppDelegate

```
#import <CrabCrashReporter/CrabCrashReport.h>
```
在AppDelegate.m的didFinishLaunchingWithOptions方法中加入如下初始代码启动Crash监控及上报

```
//YourAppKey为你在平台申请的AppKey,appVersion为该app的版本号,Channel默认为AppStore
[[CrabCrashReport sharedInstance] initCrashReporterWithAppKey:@"YourAppKey" AndVersion:@"appVersion" AndChannel:@"AppStore"];
```       
***【注意】*** 如果你的项目中引用了其它同类产品，我们建议你把它们的错误收集功能关闭，并且将Crab的初始代码放在同类产品后面

## **Optional Config**

- Crash收集开关，默认打开。**[初始化函数之前调用]**

	```
	[[CrabCrashReport sharedInstance] setCrashReportEnabled:NO]; 
	```
- SDK调试开关，默认关闭。**[初始化函数之前调用]**

	```
	[[CrabCrashReport sharedInstance] setDebugEnabled:YES];
	```
- Crab构建号设置，默认0(建议整数)。 **[初始化函数之前调用]**
	
	```
	[[CrabCrashReport sharedInstance] setBuildnumber:@"1"];
	``` 
- 设置回调函数代理对象。**[初始化函数之前调用]**
	
	-  实现回调函数接口

		```
		@interface AppDelegate : UIResponder <UIApplicationDelegate,CrashSignalCallBackDelegate>  
		```
		
	-  设置回调函数代理对象**[必须复写Crash回调函数，否则无法收到Crash信息]**
		
		```
		[[CrabCrashReport sharedInstance] setCrashCallBackDelegate:self];
		```
		
   - 在Crash回调函数中添加Crash附加信息(最多10条)
		
		``` 
		- (void)crashCallBack{
		[[CrabCrashReport sharedInstance] addCrashAttachLog:@"value1" forKey:@"key1"];
		[[CrabCrashReport sharedInstance] addCrashAttachLog:@"value2" forKey:@"key2"];
		[[CrabCrashReport sharedInstance] addCrashAttachLog:@"value3" forKey:@"key3"];
		//do other thing...
		}
		```
	
- 设置App的用户ID或者用户名，能够唯一表示一个用户就行[在用户登录成功之后调用]
	
	```
	[[CrabCrashReport sharedInstance] setAppUsername:@" YourAppUserName"]; 
	```
- Exception开关，默认YES。**[初始化函数之前调用]**
	
	``` 
	[[CrabCrashReport sharedInstance] setColloctCaughtExceptionEnable:NO];
	```
- 收集卡顿的开关，默认YES。**[初始化函数之前调用]**
	
	```
	[[CrabCrashReport sharedInstance] setCatchANREnable:YES];
	```
- 卡顿的超时时长，默认是300。**[初始化函数之前调用]**
	
	```
	[[CrabCrashReport sharedInstance] setANRTimeoutInterval:1000];
	```
- 设置是否只在WIFI环境下上传Crash|ANR|Exception(启动次数除外)，为了节省用户流量，默认只在WIFI下上传。**[初始化函数之前调用]**
	
	```
	[[CrabCrashReport sharedInstance] setUploadCrashOnlyWifi:NO];
	```
	
- 设置SDK debug log最多收集的行数，默认100**[初始化函数之前调用]**
	
	```
	[[CrabCrashReport sharedInstance] setLogcatMaxLines:100];
	```
- 设置SDK 页面跳转路径 最多收集的行数，默认20**[初始化函数之前调用]**
	
	```
	[[CrabCrashReport sharedInstance] setPagePathMaxLines:20];
	```
	
- 设置当App收集一次异常后，下次允许收集异常的间隔时间,默认10000ms**[初始化函数之前调用][3.3.1新增]**
	
	```
	[[CrabCrashReport sharedInstance] setExceptionMonitorTimeoutInterval:20000];
	```


## License

LICENSE  ©2016 Baidu, Inc. All rights reserved
