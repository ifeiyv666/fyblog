---
title: Flutter开发之Container Widget
categories:
  - Flutter
tags:
  - Flutter Container
abbrlink: 10010
date: 2019-08-15 14:22:01
---





### Container Widget

>一个方便的小部件, 结合了普通的绘画、定位和大小的小部件。

容器首先用填充物（由装饰中存在的任何边界膨胀）包围子对象，然后对填充范围应用附加约束（如果其中一个为非空，则将宽度和高度合并为约束）。然后容器被从边缘描述的额外的空白空间包围。

在绘画过程中，容器首先应用给定的变换，然后绘制装饰填充填充范围，然后绘制子对象，最后绘制前场装饰，也填充填充填充范围。

没有子对象的容器尽量大，除非传入的约束是无限的，在这种情况下，它们尽量小。有子对象的容器会根据子对象的大小来调整大小。构造函数的width、height和constraints参数重写了这一点。


#### 布局行为介绍(Layout behavior)

>有关框布局模型的介绍，请参阅[BoxConstraints](https://api.flutter.dev/flutter/rendering/BoxConstraints-class.html)。

由于Container结合了许多其他小部件，每个小部件都有自己的布局行为，因此Container的布局行为有点复杂。

摘要：容器尝试按顺序：遵循对齐，将自身大小调整为子对象，以符合宽度，高度和约束，以扩展以适合父对象，尽可能小。

进一步来说：

如果窗口小部件没有子节点，没有高度，没有宽度，没有约束，并且父节点提供无限制约束，则Container尝试尽可能小。

如果窗口小部件没有子节点且没有对齐，但提供了高度，宽度或约束，则在给定这些约束和父节点约束的组合的情况下，Container会尽可能小。

如果窗口小部件没有子节点，没有高度，没有宽度，没有约束，没有对齐，但是父节点提供了有界约束，那么Container会扩展以适应父节点提供的约束。

如果窗口小部件具有对齐，并且父窗口提供无限制约束，则Container会尝试围绕子窗口调整自身大小。

如果窗口小部件具有对齐，并且父窗口提供有界约束，则Container会尝试展开以适合父窗口，然后根据对齐方式将子项置于其自身内部。

否则，窗口小部件具有子级但没有高度，没有宽度，没有约束，也没有对齐，并且Container将约束从父级传递给子级并调整其大小以匹配子级。

边距和填充属性也会影响布局，如这些属性的文档中所述。 （它们的效果仅仅增加了上述规则。）装饰可以隐含地增加填充（例如，BoxDecoration中的边界有助于填充）;请参阅[Decoration.padding](https://api.flutter.dev/flutter/widgets/Container/padding.html)。

**此示例显示一个48x48琥珀色方块（放置在中心小部件内，以防父小部件对容器应采用的大小有自己的意见），并留有一个空白，使其远离相邻小部件：**
![Container](https://upload-images.jianshu.io/upload_images/11100630-9aafd0dda6e7ffd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/567)

```
Center(
  child: Container(
    margin: const EdgeInsets.all(10.0),
    color: Colors.amber[600],
    width: 48.0,
    height: 48.0,
  ),
)
```

**这个例子展示了如何同时使用容器的许多特性。这些约束被设置为适合字体大小加上足够的垂直净空，同时水平展开以适合父级。填充用于确保内容和文本之间有空间。这个颜色使盒子变成蓝色。对齐会使子项在框中居中。最后，变换对整个装置应用轻微的旋转以完成效果:**

![屏幕快照 2019-05-25 下午6.39.27.png](https://upload-images.jianshu.io/upload_images/11100630-8872dd960763226b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
Container(
  constraints: BoxConstraints.expand(
    height: Theme.of(context).textTheme.display1.fontSize * 1.1 + 200.0,
  ),
  padding: const EdgeInsets.all(8.0),
  color: Colors.blue[600],
  alignment: Alignment.center,
  child: Text('Hello World',
    style: Theme.of(context)
        .textTheme
        .display1
        .copyWith(color: Colors.white)),
  transform: Matrix4.rotationZ(0.1),
)
```


**也可以看看：**

*AnimatedContainer，一种在变化时平滑动画属性的变体。
边框，其中包含大量使用Container的示例。
墨水，在材质上绘制装饰，允许InkResponse和InkWell喷溅在它们上面绘画。
布局小部件的目录。*

#### 构造方法（Constructors）
>创建一个小部件, 结合了普通的绘画、定位和大小调整小部件。
```
Container({Key key, 
    AlignmentGeometry alignment,
    EdgeInsetsGeometry padding, 
    Color color, 
    Decoration decoration, 
    Decoration foregroundDecoration, 
    double width, 
    double height, 
    BoxConstraints constraints, EdgeInsetsGeometry margin, 
    Matrix4 transform, 
    Widget child 
})
```

#### 属性（Properties）

- alignment → AlignmentGeometry
   - *对齐内部的子级*

- child → Widget
   - *容器内部的子级*

- constraints → BoxConstraints 
   - *要应用于子级的附加约束*

- decoration → Decoration
   - *子级背后的装饰*
   - *可以设置边框、背景色、背景图片、圆角等属性*
   - *需要注意的是 `deoration`和 `color` 背景颜色不能共存，二者同时只能有一个*
   ```
   decoration: new BoxDecoration(
                  border: new Border.all(width: 2.0, color: Colors.red),
                  color: Colors.grey,
                  borderRadius: new BorderRadius.all(new Radius.circular(20.0)),
                  image: new DecorationImage(
                    image: new NetworkImage('http://b-ssl.duitang.com/uploads/item/201609/26/20160926203611_HXQxk.jpeg'),
                    centerSlice: new Rect.fromLTRB(270.0, 180.0, 1360.0, 730.0),
                  ),
                ),

   ```
   - ![nodecoration]()![nodecoration]()
   - *第一张图设置了背景色，未使用decoration；第二张图设置了decoration，未设置背景色*

- foregroundDecoration → Decoration
   - *在子级前面的装饰*
   - *可以设置边框、背景色、背景图片、圆角等属性*
   - *`foregroundDecoration`和 `color` 背景颜色可以共存，但是`color`有可能被遮挡*
   - *会遮挡child*
   - ![nodecoration]()

- margin → EdgeInsetsGeometry
   - *我的理解就是外边距*

- padding → EdgeInsetsGeometry
   - *我的理解就是内边距*

- transform → Matrix4
   - *在绘制容器之前要应用的转换矩阵*
   
- hashCode → int
   - *此对象的哈希代码*

- key → Key
   - *控制一个小部件如何替换树中的另一个小部件*
   
- runtimeType → Type
  - *对象的运行时类型*

#### 方法（Methods）

- build(BuildContext context) → Widget

   >描述此窗口小部件表示的用户界面部分
   
- debugFillProperties(DiagnosticPropertiesBuilder properties) → void

  >添加与节点关联的其他属性

- createElement() → StatelessElement

  >创建StatelessElement以管理此窗口小部件在树中的位置

- debugDescribeChildren() → List<DiagnosticsNode>

  >返回描述此节点的子节点的DiagnosticsNode对象列表。

- noSuchMethod(Invocation invocation) → dynamic

  >访问不存在的方法或属性时调用

- toDiagnosticsNode({String name, DiagnosticsTreeStyle style }) → DiagnosticsNode

  >返回调试工具和DiagnosticsNode.toStringDeep使用的对象的调试表示形式

- toString({DiagnosticLevel minLevel: DiagnosticLevel.debug }) → String

  >返回此对象的字符串表示形式

- toStringDeep({String prefixLineOne: '', String prefixOtherLines, DiagnosticLevel minLevel: DiagnosticLevel.debug }) → String

  >返回此节点及其后代的字符串表示形式

- toStringShallow({String joiner: ', ', DiagnosticLevel minLevel: DiagnosticLevel.debug }) → String

  >返回对象的单行详细描述

- toStringShort() → String

  >这个小部件的简短文字描述

