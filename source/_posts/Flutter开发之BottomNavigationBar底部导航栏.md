---
title: Flutter开发之BottomNavigationBar底部导航栏
categories:
  - Flutter
tags:
  - Flutter BottomNavigationBar
abbrlink: 10009
date: 2019-08-14 15:11:47
---





### BottomNavigationBar

  > 显示在应用程序的底部，用于在少量视图中进行选择，通常在三到五之间。

底部导航栏通常与`Scaffold`结合使用，它作为`Scaffold.bottomNavigationBar`参数提供。

底部导航栏的类型更改其项目的显示方式。如果未指定，则当少于四个项时它会自动设置为`BottomNavigationBarType.fixed`，否则为`BottomNavigationBarType.shifting`。

`BottomNavigationBarType.fixed`，当少于四个项目时的默认值。如果选中的项目为非null，则使用`selectedItemColor`渲染所选项目，否则使用主题的`ThemeData.primaryColor`。如果`backgroundColor`为`null`，则导航栏的背景颜色默认为`Material`背景颜色`ThemeData.canvasColor`（基本上是不透明的白色）。

`BottomNavigationBarType.shifting`，当有四个或更多项时的默认值。如果`selectedItemColor`为`null`，则所有项目都以白色呈现。导航栏的背景颜色与所选项目的`BottomNavigationBarItem.backgroundColor`相同。在这种情况下，假设每个项目将具有不同的背景颜色，并且背景颜色将与白色形成鲜明对比。

**此示例显示BottomNavigationBar，因为它在Scaffold小部件中使用。 BottomNavigationBar有三个BottomNavigationBarItem小部件，currentIndex设置为索引0.所选项目为琥珀色。 _onItemTapped函数更改所选项的索引，并在Scaffold的中心显示相应的消息:**

![IMG](https://flutter.github.io/assets-for-api-docs/assets/material/bottom_navigation_bar.png) 


**源码：**

```dart
int _selectedIndex = 0;
static const TextStyle optionStyle = TextStyle(fontSize: 30, fontWeight: FontWeight.bold);
static const List<Widget> _widgetOptions = <Widget>[
  Text(
    'Index 0: Home',
    style: optionStyle,
  ),
  Text(
     'Index 1: Business',
     style: optionStyle,
  ),
  Text(
     'Index 2: School',
     style: optionStyle,
  ),
];

void _onItemTapped(int index) {
  setState(() {
    _selectedIndex = index;
  });
}

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('BottomNavigationBar Sample'),
    ),
    body: Center(
      child: _widgetOptions.elementAt(_selectedIndex),
    ),
    bottomNavigationBar: BottomNavigationBar(
      items: const <BottomNavigationBarItem>[
        BottomNavigationBarItem(
          icon: Icon(Icons.home),
          title: Text('Home'),
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.business),
          title: Text('Business'),
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.school),
          title: Text('School'),
        ),
      ],
      currentIndex: _selectedIndex,
      selectedItemColor: Colors.amber[800],
      onTap: _onItemTapped,
    ),
  );
}
```


#### 构造方法（Constructors）


>创建一个底部导航栏，通常用作Scaffold的Scaffold.bottomNavigationBar参数。

```dart
    BottomNavigationBar({
        Key key, 
        @required List<BottomNavigationBarItem> items, 
        ValueChanged<int> onTap, 
        int currentIndex: 0, 
        double elevation: 8.0, 
        BottomNavigationBarType type, 
        Color fixedColor, 
        Color backgroundColor, 
        double iconSize: 24.0, 
        Color selectedItemColor, 
        Color unselectedItemColor, 
        double selectedFontSize: 14.0, 
        double unselectedFontSize: 12.0, 
        bool showSelectedLabels: true, 
        bool showUnselectedLabels 
    })
```

#### 属性（Properties）

- `backgroundColor → Color`
   
> 背景颜色
   
- `currentIndex → int`
   
> 当前活动`BottomNavigationBarItem`的项目索引(一般就是当前选中的那个项目索引)
   
- `elevation → double`
   
> 此底部导航栏的Z坐标
   
- `fixedColor → Color`
   
> 选中项目颜色的值（只读）
   
- `iconSize → double`
   
> 所有`BottomNavigationBarItem`图标的大小
   
- `items → List<BottomNavigationBarItem>`
   
> 定义在底部导航栏中排列的按钮项的外观
   
- `onTap → ValueChanged<int>`
   
> 点击其中一个项目时响应事件
   
- `selectedFontSize → double`
   
> 选中时`BottomNavigationBarItem`标签的字体大小
   
- `selectedItemColor → Color`
   
>选中时`BottomNavigationBarItem.icon`和`BottomNavigationBarItem.label`的颜色
   
- `showSelectedLabels → bool`
   
> 是否为未选择的`BottomNavigationBarItems`显示标签
   
- `showUnselectedLabels → bool`
   
> 是否为选定的`BottomNavigationBarItem`显示标签
   
- `type → BottomNavigationBarType`
   
> 定义`BottomNavigationBar`的布局和行为
   
- `unselectedFontSize → double`
   
> 未选中`BottomNavigationBarItem`标签的字体大小
   
- `unselectedItemColor → Color`
   
> 未选中的`BottomNavigationBarItem.icon`和`BottomNavigationBarItem.labels`的颜色
   
- `hashCode → int`
   
> 对象的哈希值（只读）
   
- `key → Key`
   
>控制一个小部件如何替换树中的另一个小部件
   
- `runtimeType → Type`
   
   >表示对象的运行时类型(只读)