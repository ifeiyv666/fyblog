---
title: Swift 简单链表实现
categories:
  - Swift
abbrlink: 10024
date: 2019-06-17 15:21:08
tags:
  - 链表
  - swift
---

#### Swift 简单链表实现

> 链表中的元素在内存中不是顺序存储的，查找慢，插入、删除只需要对元素指针重新赋值，效率高；数组元素在内存上连续存放，可以通过下标查找元素；插入、删除需要移动大量元素，比较适用于元素很少变化的情况


```

import UIKit

//链表节点
public class Node{
    
    var value: T //节点存储数据
    weak var next: Node? //节点链接到的下一个节点
    
    weak var previous: Node?//节点链接到的上一个节点
     
    init(value: T) {
      self.value = value
    }
}

//自定义链表
public class NodeList:CustomStringConvertible{
    //链表起点节点
    private var head:Node?
    
    //链表终点节点
    private var tail:Node?

    //链表内数据是否为空
    public var isEmpty:Bool{
        return head == nil
    }
    //返回第一个节点
    public var first:Node?{
        return head
    }
    //返回最后一个节点
    public var last:Node?{
        return tail
    }
    
    //添加一个链接节点数据
    public func append(value:T){
        let newNode = Node(value: value)
        if let tailNode = tail{
            newNode.previous = tailNode
            tailNode.next = newNode
        }else{
            head = newNode
        }
        tail = newNode
    }
    
    //删除节点
    public func remove(node:Node) -> T{
        
        //保存要删除节点的上一个和下一个节点
        let prev = node.previous
        let next = node.next
        
        //如果要删处节点的上一节点不为空
        if let prev = prev {
            //上一个节点链接到的下一个节点，修改为要删除的下一个节点
            prev.next = next
        }
            //如果要删处节点的上一节点为空，说明要删除的是链表起点节点
        else {
            //把下一个节点改为起点节点
            head = next
        }
        
        //要删出的上一个节点，链接到上一个节点
        next?.previous = prev
        if next == nil {
            //next为nil说明要删除的是最后一个，把倒数以前倒数第二个，置为最后一个
            tail = prev
        }
        
        node.previous = nil
        node.next = nil
        return node.value

    }
    //删除所有节点数据
    public func removeAll() {
      head = nil
      tail = nil
    }
    
    //取对应索引的节点
    public func nodeAt(index: Int) -> Node? {
      if index >= 0 {
        var node = head
        var i = index
        while node != nil {
          if i == 0 { return node }
          i -= 1
          node = node!.next
        }
      }
      return nil
    }
    
    //输出节点数据
    public var description: String{
        var text = ""
        var node = head
        while node != nil {
            text += "\(node!.value)"
            
            node = node!.next
            if node != nil {
                text += ","
            }
        }
        return "[" + text + "]"
    }
}


```


