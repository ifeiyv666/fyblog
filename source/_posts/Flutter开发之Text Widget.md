---
title: Flutter开发之Text Widget
categories:
  - Flutter
tags:
  - Flutter Text
abbrlink: 10015
date: 2019-08-21 21:43:55
---





### Text Widget

>“文本”小组件显示单个样式的文本字符串。字符串可能会跨越多行，也可能全部显示在同一行上，具体取决于布局约束。

```
Text(
   //显示的文本
  'Hello, $_name! How are you?',
  //对齐的方式
  textAlign: TextAlign.center,
  
  overflow: TextOverflow.ellipsis,
  
  //文本样式
  style: TextStyle(fontWeight: FontWeight.bold),
)
```

>下面使用Text.rich构造函数，Text小部件可以显示具有不同样式TextSpans的段落。下面的示例显示每个单词具有不同样式的“Hello beautiful world”。

```
const Text.rich(
  TextSpan(
    text: 'Hello', // default text style
    children: <TextSpan>[
      TextSpan(text: ' beautiful ', style: TextStyle(fontStyle: FontStyle.italic)),
      TextSpan(text: 'world', style: TextStyle(fontWeight: FontWeight.bold)),
    ],
  ),
)
```

#### 交互

要使Text对触摸事件做出反应，请使用GestureDetector.onTap处理程序将其包装在GestureDetector小部件中。

在材料设计应用程序中，请考虑使用FlatButton，或者如果不合适，至少使用InkWell而不是GestureDetector。

要使文本的各个部分具有交互性，请使用RichText并将TapGestureRecognizer指定为文本相关部分的TextSpan.recognizer。


>[RichText](https://api.flutter.dev/flutter/widgets/RichText-class.html)，它可以让您更好地控制文本样式。
[DefaultTextStyle](https://api.flutter.dev/flutter/widgets/DefaultTextStyle-class.html)，用于设置Text小部件的默认样式。

#### 构造方法


```
    
   Text(String data, { 
              Key key, 
              TextStyle style, 
              StrutStyle strutStyle,
              TextAlign textAlign,
              TextDirection textDirection,
              Locale locale, 
              bool softWrap, 
              TextOverflow overflow, 
              double textScaleFactor, 
              int maxLines, 
              String semanticsLabel 
   })
```

```
    Text.rich(TextSpan textSpan, { 
                       Key key, 
                       TextStyle style,
                       StrutStyle strutStyle,
                       TextAlign textAlign,
                       TextDirection textDirection, 
                       Locale locale, 
                       bool softWrap, 
                       TextOverflow overflow, 
                       double textScaleFactor, 
                       int maxLines, 
                       String semanticsLabel 
        
    })
```

#### 属性

- data → String   
   - *要显示的文字*

- locale → Locale
   - *用于在可以以不同方式呈现相同Unicode字符时选择字体，具体取决于区域设置*
   - *很少需要设置此属性。默认情况下，其值继承自包含Localizations.localeOf（context）的应用程序*
   - *有关更多信息，请参见[RenderParagraph.locale](https://api.flutter.dev/flutter/widgets/Text/locale.html)。*

- maxLines→int
   - *文本要跨越的可选最大行数，必要时包装。如果文本超过给定的行数，则会根据溢出将其截断*

- overflow→TextOverflow
   - *如何处理视觉溢出*
   - TextOverflow枚举
      * clip→const TextOverflow
剪切溢出的文本以修复其容器。
const TextOverflow（0）
      * ellipsis→const TextOverflow
将溢出的文本淡化为透明。
const TextOverflow（1）
      * ellipsis→const TextOverflow
使用省略号表示文本已溢出。
const TextOverflow（2）
      * visible→const TextOverflow
在其容器外部渲染溢出的文本。
const TextOverflow（3）
      * values→const List <TextOverflow>
此枚举中值的常量列表，按其声明顺序排列。
const List <TextOverflow>

- semanticsLabel→String
   - *此文本的替代语义标签*
   - *如果存在, 这个小部件的语义将包含此值, 而不是实际的文本。这将覆盖任何直接应用于 TextSpans 的语义标签*
   - *这对于用全文值替换缩写或短文很有用: `Text(r'$$', semanticsLabel: 'Double dollars')`*

- softWrap→bool
   - *文本是否应该在软换行符处中断*
   - *如果是false, 文本中的字形将被定位为无限的水平空间*

- strutStyle→StrutStyle
   - *要使用的strut风格。 Strut样式定义了strut，它设置了最小垂直布局度量*
   - *允许省略或提供 null 将禁用strut. 为 StrutStyle 的任何属性提供 null 将导致使用默认值*
   - *强烈建议至少指定一个字体. 有关详细信息, 请参见 [StrutStyle](https://api.flutter.dev/flutter/painting/StrutStyle-class.html)。*
   - eg:
   
    ```
       const Text(
            'Hello, world!\nSecond line!',
            style: TextStyle(
            fontSize: 10,
            fontFamily: 'Raleway',
        ),
      strutStyle: StrutStyle(
            fontFamily: 'Roboto',
            fontSize: 30,
            height: 1.5,
      ),
    ),
    ```

- style→TextStyle
   - *如果为非null，则为此文本使用的样式*
   - *如果样式的 "继承" 属性为 true, 则该样式将与最接近的封闭默认文本样式合并*
   - *否则, 该样式将替换最接近的封闭的默认文本样式*

- textAlign→TextAlign
   - *文本应如何水平对齐*
   - *TextAlign 枚举*
      * left → const TextAlign 文本左对齐 const TextAlign(0)
      * right → const TextAlign 文本右对齐 const TextAlign(1)
      * center→ const TextAlign 文本中心对齐 const TextAlign(2)
      * justify → const TextAlign 拉伸以柔和的换行符结束的文本行, 以填充容器的宽度. 以硬线符结束的线条与起始边缘对齐。const TextAlign(3)
      * start → const TextAlign  文本开始处对齐 从左到右即为左边，从右到左即为右边 const TextAlign(4)
      * end → const TextAlign 文本结束处对齐 从左到右即为右边，从右到左即为左边 const TextAlign(5)
      * values → const List<TextAlign> 此枚举中值的常量列表，按其声明顺序排列。

- textDirection→TextDirection
   - *文本的方向性*
   - *这也就解释为什么出现TextAlign.start和TextAlign.end等textAlign值*
   - *eg: 例如，如果数据是英语短语后跟希伯来语短语，则在TextDirection.ltr上下文中，英语短语将位于左侧，希伯来语短语位于其右侧，而在TextDirection.rtl上下文中，英语短语将 在右边，左边是希伯来语。*

- textScaleFactor→double
   - *每个逻辑像素的字体像素数*
   - *例如，如果文本比例因子为1.5，则文本将比指定的字体大小大50％*
   - *作为textScaleFactor赋予构造函数的值。 如果为null，将使用从环境MediaQuery获取的MediaQueryData.textScaleFactor，如果范围内没有MediaQuery，则使用1.0。*

- textSpan→TextSpan
   - *要显示为TextSpan的文本*

- hashCode→int
   - *此对象的哈希码*

- key→Key
   - *控制一个小部件如何替换树中的另一个小部件*

- runtimeType→Type
   - *表示对象的运行时类型*


#### 方法

- build（BuildContext context）→Widget
   - *描述此窗口小部件表示的用户界面部分*

- debugFillProperties（DiagnosticPropertiesBuilder properties）→void
   - *添加与节点关联的其他属性*

- createElement（）→StatelessElement
   - *创建StatelessElement以管理此窗口小部件在树中的位置。 [...]*

- debugDescribeChildren（）→ List<DiagnosticsNode>
   - *返回描述此节点的子节点的DiagnosticsNode对象列表。 [...]*

- noSuchMethod（Invocation invocation）→dynamic
   - *访问不存在的方法或属性时调用。 [...]*

- toDiagnosticsNode（{String name，DiagnosticsTreeStyle style}）→DiagnosticsNode
   - *返回调试工具和DiagnosticsNode.toStringDeep使用的对象的调试表示形式。 [...]*

- toString（{DiagnosticLevel minLevel：DiagnosticLevel.debug}）→字符串
   - *返回此对象的字符串表示形式*

- toStringDeep（{String prefixLineOne：''，String prefixOtherLines，DiagnosticLevel minLevel：DiagnosticLevel.debug}）→String
   - *返回此节点及其后代的字符串表示形式。 [...]*

- toStringShallow（{String joiner：'，'，DiagnosticLevel minLevel：DiagnosticLevel.debug}）→String
   - *返回对象的单行详细描述。 [...]*

- toStringShort（）→String
   - *这个小部件的简短文字描述*

### Operators运算符

- operator ==(dynamic other) → bool
   - *等值运算符。 [...]*