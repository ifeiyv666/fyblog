---
title: Swift中String转类名Class
categories:
  - Swift
tags:
  - Swift
  - Class
abbrlink: 10023
date: 2019-06-17 11:24:32
---



### String->Class

>Swift中引入了命名空间的概念，转Class需要拼接命名空间

```
    
    //这是一个简单的通过字符串类名，转Class然后初始化后跳转的一个小例子
    @objc func OnClick(){
    
        //控制器字符串名称
        let vcNameString = "OneViewController"
        //获取命名空间也就是项目名称
        let clsName = Bundle.main.infoDictionary!["CFBundleExecutable"] as? String
        
        //拼接
        let className=clsName! + "." + vcNameString
        
        //字符串转Class 需要注意的是这里的`UIViewController`强转必须带上`.Type`,否则转换不成功
        let classT = NSClassFromString(className)! as! UIViewController.Type
        
        
        URLRouter.shared.pushViewController(viewController:classT.init()  , animated: true)
    }//成功完成跳转
    
    
```

<!-- more -->

- ***注意***
    1. Swift中引入了命名空间的概念，转Class需要拼接命名空间
    2. 这里的`UIViewController`强转必须带上`.Type`,否则转换不成功
