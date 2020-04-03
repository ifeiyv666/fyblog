---
title: Swift判断字符串中是否含有中文
categories:
  - Swift
tags:
  - Swift字符串
abbrlink: 10022
date: 2020-01-15 10:48:26
---


```swift
var str = "l我o是v中e文123456789"

func judgeStringIncludeChineseWord(string: String) -> Bool {
    
    for (_, value) in string.characters.enumerated() {

        if ("\u{4E00}" <= value  && value <= "\u{9FA5}") {
            return true
        }
    }
    
    return false
}

let result = judgeStringIncludeChineseWord(string: str) 


```