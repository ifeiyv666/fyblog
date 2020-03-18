
---
title: Swift 分享邀请码图片合成
categories:
  - Swift
tags:
  - 图片合成
abbrlink: 10020
date: 2019-12-15 18:43:21
---




```
    class func creteImage(bgImage: UIImage, iconImage: UIImage,iconFrame:CGRect,qrCodeImage:UIImage,codeFrame:CGRect,inviteCodeImg:UIImage,frame:CGRect) -> UIImage
    {
        // 1.开启图片上下文
//        UIGraphicsBeginImageContext(bgImage.size)
        UIGraphicsBeginImageContextWithOptions(bgImage.size,false,UIScreen.main.scale)
        // 2.绘制背景图片
        bgImage.draw(in: CGRect(origin: CGPoint.zero, size: bgImage.size))
        // 3.绘制头像
        iconImage.draw(in: iconFrame)
        
        qrCodeImage.draw(in: codeFrame)
        
        inviteCodeImg.draw(in: frame)
        // 4.取出绘制号的图片
        let newImage = UIGraphicsGetImageFromCurrentImageContext()
        // 5.关闭上下文
        UIGraphicsEndImageContext()
        // 6.返回合成号的图片
        return newImage!
    }
```


```
    //MARK: -传进去字符串,生成二维码图片
   class func setupQRCodeImage(_ text: String) -> UIImage {
        //创建滤镜
        let filter = CIFilter(name: "CIQRCodeGenerator")
        filter?.setDefaults()
        //将url加入二维码
        filter?.setValue(text.data(using: String.Encoding.utf8), forKey: "inputMessage")
        //取出生成的二维码（不清晰）
        if let outputImage = filter?.outputImage {
            //生成清晰度更好的二维码
            let qrCodeImage = Util.setupHighDefinitionUIImage(outputImage, size: 140)
            return qrCodeImage
        }
        
        return UIImage()
    }
    
    //MARK: - 生成高清的UIImage
   class func setupHighDefinitionUIImage(_ image: CIImage, size: CGFloat) -> UIImage {
        let integral: CGRect = image.extent.integral
        let proportion: CGFloat = min(size/integral.width, size/integral.height)
        
        let width = integral.width * proportion
        let height = integral.height * proportion
        let colorSpace: CGColorSpace = CGColorSpaceCreateDeviceGray()
        let bitmapRef = CGContext(data: nil, width: Int(width), height: Int(height), bitsPerComponent: 8, bytesPerRow: 0, space: colorSpace, bitmapInfo: 0)!
        
        let context = CIContext(options: nil)
        let bitmapImage: CGImage = context.createCGImage(image, from: integral)!
        
        bitmapRef.interpolationQuality = CGInterpolationQuality.none
        bitmapRef.scaleBy(x: proportion, y: proportion);
        bitmapRef.draw(bitmapImage, in: integral);
        let image: CGImage = bitmapRef.makeImage()!
        return UIImage(cgImage: image)
    }

```

```
    class func getImageFromView(view:UIView) ->UIImage{
//        UIGraphicsBeginImageContext(view.bounds.size)
        UIGraphicsBeginImageContextWithOptions(view.bounds.size,false,UIScreen.main.scale)
        view.layer.render(in: UIGraphicsGetCurrentContext()!)
        
        let image = UIGraphicsGetImageFromCurrentImageContext()
        
        UIGraphicsEndImageContext()
        
        return image!
    }
```