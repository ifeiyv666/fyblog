---
title: Flutter开发之Image Widget
categories:
  - Flutter
tags:
  - Flutter Image
abbrlink: 10011
date: 2019-08-16 11:16:41
---



### Image Widget

>显示图像的小部件,支持以下图像格式: JPEG、PNG、GIF、动画 GIF、WebP、动画 WebP、BMP 和 WBMP

**为图像可以指定的各种方式提供了几个构造函数:**

- new Image, 通过 ImageProvider获取图像
- new Image.asset, 使用key值从资源包获取图像
- new Image.network, 通过URL网络请求获取图像
- new Image.file, 从文件中获取图像.
- new Image.memory, 从 Uint8List中 获取图像.



#### 构造方法（Constructors）

>Image 创建一个显示图像的小部件
```
Image({
    Key key, 
    @required ImageProvider image, 
    String semanticLabel, 
    bool excludeFromSemantics: false, 
    double width, double height, 
    Color color, 
    BlendMode colorBlendMode, 
    BoxFit fit, 
    AlignmentGeometry alignment: Alignment.center, ImageRepeat repeat: ImageRepeat.noRepeat, 
    Rect centerSlice, 
    bool matchTextDirection: false, 
    bool gaplessPlayback: false, 
    FilterQuality filterQuality: FilterQuality.low 
})
```

>创建一个小部件,显示从资源包里获得的 ImageStream,图像的键是由名称参数给出的
```
Image.asset(String name, { 
    Key key, 
    AssetBundle bundle, 
    String semanticLabel, 
    bool excludeFromSemantics: false, 
    double scale, 
    double width, 
    double height, 
    Color color, 
    BlendMode colorBlendMode, 
    BoxFit fit, 
    AlignmentGeometry alignment: Alignment.center, ImageRepeat repeat: ImageRepeat.noRepeat, 
    Rect centerSlice, 
    bool matchTextDirection: false, 
    bool gaplessPlayback: false, 
    String package, 
    FilterQuality filterQuality: FilterQuality.low 
        
})
```
>创建一个小部件, 显示从文件中获得的 ImageStream
```
Image.file(File file, { 
    Key key, 
    double scale: 1.0, 
    String semanticLabel, 
    bool excludeFromSemantics: false, 
    double width, 
    double height, 
    Color color, 
    BlendMode colorBlendMode, 
    BoxFit fit, 
    AlignmentGeometry alignment: Alignment.center, ImageRepeat repeat: ImageRepeat.noRepeat, 
    Rect centerSlice, 
    bool matchTextDirection: false, 
    bool gaplessPlayback: false, 
    FilterQuality filterQuality: FilterQuality.low 
})
```

>创建一个小部件,显示从Uint8List中获得的ImageStream
```
Image.memory(Uint8List bytes, { 
    Key key, 
    double scale: 1.0, 
    String semanticLabel, 
    bool excludeFromSemantics: false, 
    double width, 
    double height, 
    Color color, 
    BlendMode colorBlendMode, 
    BoxFit fit, 
    AlignmentGeometry alignment: Alignment.center, ImageRepeat repeat: ImageRepeat.noRepeat, 
    Rect centerSlice, 
    bool matchTextDirection: false, 
    bool gaplessPlayback: false, 
    FilterQuality filterQuality: FilterQuality.low
})
```

>创建一个小部件, 显示从网络获得的ImageStream
```
Image.network(String src, { 
    Key key, 
    double scale: 1.0, 
    String semanticLabel, 
    bool excludeFromSemantics: false, 
    double width, 
    double height, 
    Color color, 
    BlendMode colorBlendMode, 
    BoxFit fit, 
    AlignmentGeometry alignment: Alignment.center, ImageRepeat repeat: ImageRepeat.noRepeat, 
    Rect centerSlice, 
    bool matchTextDirection: false, 
    bool gaplessPlayback: false, 
    FilterQuality filterQuality: FilterQuality.low,
    Map<String, String> headers 
})
```

#### 属性（Properties）

- alignment → AlignmentGeometry
   - *设置图像的对齐方式*

- centerSlice → Rect
   - *九片图像的中心切片*
   - *中心切片内的图像区域将水平和垂直拉伸，以使图像适合其目标*
   - *中心切片上方和下方的图像区域将仅水平拉伸，中心切片左侧和右侧的图像区域将仅垂直拉伸* 

- color → Color
   - *如果非 null, 则使用颜色混合模式将此颜色与每个图像像素混合*

- colorBlendMode → BlendMode
   - *用于将颜色与此图像相结合*

- excludeFromSemantics → bool
   - *是否从语义中排除此图像*

- filterQuality → FilterQuality
   - *用于设置图像的FilterQuality*

- fit → BoxFit
   - *图片填充的方式*
      * `contain` 在目标框中尽可能大的显示完整图像
          ![box_fit](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_contain.png)
      * `cover`   在目标框中尽可能小的覆盖整个目标框
          ![box_fit](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_cover.png)      
      * `fill`  通过拉伸纵横比来填充整个目标框
          <br>![box_fit](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_fill.png) 
      * `fitHeight` 在目标框中高度填充满，不论宽度是否溢出
          ![box_fit](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_fitHeight.png) 
      * `fitWidth`  在目标框中宽度填充满，不论高度是否溢出
          ![box_fit](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_fitWidth.png) 
      * `none` 对齐目标框内的源（默认情况下，居中）并丢弃位于框外的源的任何部分。源图像未调整大小。
           ![box_fit](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_none.png) 
      * `scaleDown` 对齐目标框中的源 (默认情况下, 居中), 并在必要时缩小源的比例, 以确保源适合框中。
        <br>![box_fit](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_scaleDown.png) 


- gaplessPlayback → bool
   - *当图像更换时是继续显示旧图像 (true), 还是短暂不显示任何内容 (false)*

- height → double
   - *如果非空, 则要求图像具有此高度*

- image → ImageProvider
   - *要显示的图像*

- matchTextDirection → bool
   - *是否将图像绘制到文本方向的方向*

- repeat → ImageRepeat
   - *如何绘制图像不包括的布局边界的任何部分*
      * `noRepeat` 让盒子的未覆盖部分保持透明,不重复
      * `repeat`   在 x 和 y 方向上重复图像, 直到框被填满
      * `repeatX` 按 x 方向重复图像, 直到水平方向填充满
      * `repeatY` 按 Y 方向重复图像, 直到垂直方向填充满

- semanticLabel → String
   - *对图像的语义描述*

- width → double
   - *如果非空, 则要求图像具有此宽度*

- hashCode → int
   - *此对象的哈希代码*

- key → Key
   - *控制一个小部件如何替换树中的另一个小部件*
   
- runtimeType → Type
  - *对象的运行时类型*


#### 方法（Methods）

>在树中的给定位置为这个小部件创建可变状态。
- createState() → _ImageState

>添加与节点管理相关联的其他属性
- debugFillProperties(DiagnosticPropertiesBuilder properties) → void

>创建StatelessElement以管理此窗口小部件在树中的位置
- createElement() → StatelessElement

>返回描述此节点的子节点的DiagnosticsNode对象列表。

- debugDescribeChildren() → List<DiagnosticsNode>

>访问不存在的方法或属性时调用
- noSuchMethod(Invocation invocation) → dynamic


>返回调试工具和DiagnosticsNode.toStringDeep使用的对象的调试表示形式
- toDiagnosticsNode({String name, DiagnosticsTreeStyle style }) → DiagnosticsNode

>返回此对象的字符串表示形式

- toString({DiagnosticLevel minLevel: DiagnosticLevel.debug }) → String


>返回此节点及其后代的字符串表示形式
- toStringDeep({String prefixLineOne: '', String prefixOtherLines, DiagnosticLevel minLevel: DiagnosticLevel.debug }) → String

>返回对象的单行详细描述

- toStringShallow({String joiner: ', ', DiagnosticLevel minLevel: DiagnosticLevel.debug }) → String

>这个小部件的简短文字描述

- toStringShort() → String

  

