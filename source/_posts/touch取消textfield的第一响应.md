---
title: touch取消textfield的第一响应
categories:
  - Swift
abbrlink: 10025
date: 2019-06-17 13:07:29
tags:
  - Responsder
  - touch
---


```swift
    override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {
        
        for touch:AnyObject in touches {
            let t:UITouch = touch as! UITouch
            //检测当前触摸的view是否是textField
            if t.view == pwdField || t.view == pwdField || t.view == phoneField{
                t.view?.becomeFirstResponder()
            }else{
                phoneField.resignFirstResponder()
                pwdField.resignFirstResponder()
                verificationField.resignFirstResponder()
                self.resignFirstResponder()
            }
        }
        
    }
```