---
title: 直播系列三、IJKPlayer拉流
categories:
  - iOS
tags:
  - 直播
abbrlink: 10028
date: 2019-11-08 11:32:57
---




[https://www.jianshu.com/p/65fb80dff4d6](https://www.jianshu.com/p/65fb80dff4d6)

合并真机和模拟器的framework
```
lipo -create 真机framework路径 模拟器framework路径 -output 合并的文件路径
```

```
import UIKit

class playerViewController: UIViewController {

    var iPlayer:IJKFFMoviePlayerController? 
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        let options:IJKFFOptions = IJKFFOptions.byDefault()
        let url:URL = URL.init(string: "rtmp://live.hkstv.hk.lxdns.com/live/hks")!
 
        
        self.iPlayer = IJKFFMoviePlayerController.init(contentURL: url, with: options)
        var arm1 = UIViewAutoresizing.init(rawValue: 0)
        arm1.insert(UIViewAutoresizing.flexibleWidth)
        arm1.insert(UIViewAutoresizing.flexibleHeight) 
        self.iPlayer?.view.autoresizingMask = arm1
        self.iPlayer?.view.backgroundColor = UIColor.white
        self.iPlayer?.view.frame = CGRect.init(x: 0, y: 0, width: UIScreen.main.bounds.size.width, height: 300)
        self.iPlayer?.scalingMode = .aspectFit
        self.iPlayer?.shouldAutoplay = true
        self.view.autoresizesSubviews = true
        self.view.addSubview((self.iPlayer?.view)!)
        
        // Do any additional setup after loading the view, typically from a nib.
    }
    
    
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        self.iPlayer?.prepareToPlay() //准备
        self.iPlayer?.play() //播放
    }
    
    
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        self.iPlayer?.pause()//暂停
//        self.iPlayer?.shutdown() //销毁
    }

}
```