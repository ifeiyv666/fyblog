---
title: iOS 13 DarkMode适配
#top: 最近更新
categories:
  - iOS
tags:
  - DarkMode
  - Swift
abbrlink: 10016
date: 2020-03-13 12:44:21
---

#### 封装颜色管理类


```swift

//
//  FyColor.swift
//  FyColor
//
//  Created by l on 2020/3/13.
//  Copyright © 2020 ifeiyv. All rights reserved.
//
import UIKit

class FyColors{
    
    ///深色模式适配  手动控制适配模式 启用 关闭(如非必要，可移除相关代码)
    static let isOpenDarkModel:Bool  = true
    
    
    //MARK: eg文字颜色
    //文字颜色  如果有多种文字颜色可以设置多个 eg: labelTextColor
    public class var labelTextColor: UIColor {
        return darkModeColor(dark:UIColor.white,light:UIColor.black)
    }
    //文字颜色  如果有多种文字颜色可以设置多个 eg:  buttonTextColor
    public class var buttonTextColor: UIColor {
        return darkModeColor(dark:UIColor.white,light:UIColor.black)
    }
    
    //文字颜色  如果有多种文字颜色可以设置多个 eg:  fieldTextColor
    public class var fieldTextColor: UIColor {
        return darkModeColor(dark:UIColor.white,light:UIColor.black)
    }
    
    //MARK: eg背景颜色
    //背景颜色  如果有多种文字颜色可以设置多个 eg: labelBgColor
    public class var labelBgColor: UIColor {
        return darkModeColor(dark:UIColor.black,light:UIColor.white)
    }
    //背景颜色  如果有多种文字颜色可以设置多个 eg:  buttonBgColor
    public class var buttonBgColor: UIColor {
        return darkModeColor(dark:UIColor.black,light:UIColor.white)
    }
    
    //背景颜色  如果有多种背景颜色可以设置多个 eg:  viewBgColor
    public class var viewBgColor: UIColor {
        return darkModeColor(dark:UIColor.black,light:UIColor.white)
    }
    
    //.........................................
    //根据需求增加相对应的颜色即可
    //darkModeColor(dark:UIColor.white,light:UIColor.black)
    //实际开发中不可能只有 UIColor.white，UIColor.black 两种颜色。
    //根据产品需求增加和修改对应的颜色
    
    
    //检测当前是否是深色模式
    class func isDarkStyle() -> Bool{
        if(!isOpenDarkModel){
            return false
        }
        if #available(iOS 13.0, *){
            let currentMode = UITraitCollection.current.userInterfaceStyle
            if(currentMode == .dark){
                return  true
            }
        }
        return false
    }
    // 适配 动态颜色
    class func darkModeColor(dark:UIColor,light:UIColor) ->UIColor{
        if(!isOpenDarkModel){
            return light
        }
        if #available(iOS 13.0, *){
            return UIColor{(trainCollection) -> UIColor in
                if trainCollection.userInterfaceStyle == .dark{
                    return dark
                }else{
                    return light
                }
            }
        }
        return light
    }
}



```


##### 使用方式：(深色模式切换时，系统会重新渲染颜色，自动在设置好的两种颜色中进行切换)

 ```swift
    label.textColor = FyColors.labelTextColor
   
    label.backgroundColor = FyColors.labelBgColor
    
     //或者在此方法监听深色模式进行手动切换
    override func traitCollectionDidChange(_ previousTraitCollection: UITraitCollection?) {
        super.traitCollectionDidChange(previousTraitCollection)
    }
 ```