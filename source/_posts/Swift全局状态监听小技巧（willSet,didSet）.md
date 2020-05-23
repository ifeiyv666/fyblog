---
title: Swift全局状态监听小技巧（**willSet**,didSet）
categories:
  - Swift
tags:
  - Swift
  - didSet
  - willSet
abbrlink: 11111
date: 2020-05-23 17:53:13

---



#### Swift全局状态监听小技巧（willSet,didSet）



##### 封装：便于统一管理，方便使用

```swift
enum FyAppObserverName:String{
    case isLogin  = "isLogin"   //是否是登录状态
    case isVip    = "isVip"    //是否是Vip
    case timeLength = "timeLength"  //时长
}

class FyAppStatusManger:NSObject{
    static let shared = FyAppStatusManger.init()
    var valueChanged:((_ observerName:FyAppObserverName,_ oldValue:Any?,_ newValue:Any?) ->())?
    
    override init(){
        super.init()
    }
    
    //需要监听变化的值
    var isLogin:Bool = false{
        didSet{
            valueChanged?(.isLogin, oldValue, isLogin)
        }
    }
    
    var isVip:Bool = false{
        didSet{
            valueChanged?(.isVip, oldValue, isLogin)
        }
    }
    
    var timeLength:Int  = 0{
        didSet{
            valueChanged?(.timeLength, oldValue, isLogin)
        }
    }
    
}

```

##### 使用：

```swift
FyAppStatusManger.shared.valueChanged =  {(observerName,oldValue ,newValue) in
            //可以在app需要的地方调用，需求监听的状态可以根据实际情况自由搭配
    switch observerName{
    case .isLogin:
      //登录状态发生改变
       	break
     case .isVip:
      //会员状态发生改变
          break
      default:
          break
    }          
}
```



