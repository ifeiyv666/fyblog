---
title: Swift Responsder
categories:
  - Swift
abbrlink: 10024
date: 2019-06-17 12:57:24
tags:
  - Responsder
---

### 通过响应者链获取对应的第一个符合条件的Responsder

> 传入响应检测的起点`Responsder`，一般用于UIView中查找响应者链中的控制器

```
func nextResponder(currentView:UIView)->UIViewController{
var vc:UIResponder = currentView
while vc.isKind(of: UIViewController.self) != true {
vc = vc.next!
}
return vc as! UIViewController
}

```


