\---

title: MAC录制鼠标事件脚本

categories:

 \- Mac

tags:

 \- 脚本录制

 \- 鼠标事件

abbrlink: 10112

date: 2020-03-31 09:10:21

\---

#### 录制鼠标事件脚本

![test007](images/test007.gif)

用到自己封装好的工具  [MAC代码模拟鼠标和键盘事件](https://ifeiyv.cn/tags/代码模拟键盘/)

>   **var** timeStamp:CLongLong = -1  //保存上次时间戳
>
>    **var** isStart:Bool = **false**  //保存是否开始录制脚本
>
>   **var** events:[CGEvent] = [CGEvent]() //保存所有鼠标事件
>
>   **var** times:[Int] = [Int]() //保存鼠标事件事件间隔（完美时间还原脚本）

##### 1.录制脚本

```swift
override func viewDidLoad() {
        super.viewDidLoad()
       
        monitor =  NSEvent.addGlobalMonitorForEvents(matching:[.mouseMoved,.leftMouseDown,.leftMouseUp,.leftMouseDragged,.rightMouseDown,.rightMouseUp,.rightMouseDragged,.scrollWheel]) { [weak self](event) in
            self?.label.cell?.title = "x=\(String(format: "%.0f", event.locationInWindow.x))\ny=\(String(format: "%.0f", ScreenHeight - event.locationInWindow.y))"
            if(self!.isStart){//是否开始录制脚本
                self!.events.append(event.cgEvent!)
                if(self!.events.count > 1){
                    self!.times.append(Int(Date().milliStamp - self!.timeStamp))
                    self!.timeStamp = Date().milliStamp
                }else{
                    self!.times.append(10)
                    self!.timeStamp = Date().milliStamp
                }
            }
        }

    }
```



##### 2.播放脚本

```swift
func  playEvent(){
      var index = 0
      for event in events {
          if(index > times.count - 1){
             Thread.sleep(forTimeInterval: TimeInterval(0.01))
          }else{
             Thread.sleep(forTimeInterval: TimeInterval( Double(times[index]) / 1000.0))
          }
      index += 1;
      event.post(tap: .cghidEventTap)
   }
}
```







