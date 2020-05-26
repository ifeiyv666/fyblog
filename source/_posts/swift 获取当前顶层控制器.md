---
title: swift 获取当前顶层控制器
categories:
  - Swift
tags:
  - 顶层控制器
abbrlink: 11112
date: 2020-05-25 09:55:17
---



#### swift 获取当前顶层控制器

```swift
var topViewController: UIViewController? {
    var resultVC: UIViewController?
    resultVC = _topViewController(UIApplication.shared.keyWindow?.rootViewController)
    while resultVC?.presentedViewController {
        resultVC = _topViewController(resultVC?.presentedViewController)
    }
    return resultVC
}

func _topViewController(_ vc: UIViewController?) -> UIViewController? {
    if (vc is UINavigationController) {
        return _topViewController((vc as? UINavigationController)?.topViewController)
    } else if (vc is UITabBarController) {
        return _topViewController((vc as? UITabBarController)?.selectedViewController)
    } else {
        return vc
    }
    return nil
}

```

