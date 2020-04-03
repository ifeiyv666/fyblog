---
title: SWIFT 常用方法
categories:
  - Swift
tags:
  - Swift Method
abbrlink: 10019
date: 2019-06-12 10:22:51
---



```swift
//
//  LayoutProperties.swift
//  IfeiyvSwift
//
//  Created by l on 2019/6/12.
//  Copyright © 2019 ifeiyv. All rights reserved.
//

import UIKit
import CommonCrypto

//Mark:------------Layout
struct Screen{
    
    //MARK:屏幕宽度
    static var width:CGFloat{
        return UIScreen.main.bounds.width
    }
    //MARK:屏幕高度
    static var height:CGFloat{
        return UIScreen.main.bounds.height
    }
    //MARK:分辨率 倍率
    static var scale:CGFloat{
        return Screen.width/375.0
    }
}


extension UIView{
    
    //MARK: 设置或者获取UIView的frame
    var fy_frame:CGRect{
        set{
            self.frame = fy_frame
        }
        get{
            return self.frame
        }
    }
    
    //MARK: 设置或者获取UIView的origin
    var fy_origin:CGPoint{
        set{
            self.frame = CGRect(x: fy_origin.x, y: fy_origin.y, width: self.fy_width, height: self.fy_height)
        }
        get{
            return self.frame.origin
        }
    }
    
    //MARK: 设置或者获取UIView的size
    var fy_size:CGSize{
        set{
            self.frame = CGRect(x: self.fy_origin.x, y: self.fy_origin.y, width: fy_size.width, height: fy_size.height)
        }
        get{
            return self.frame.size
        }
    }
    
    
    //MARK: 设置或者获取UIView的宽度
    var fy_width:CGFloat{
        set{
            self.frame = CGRect(x: self.frame.origin.x, y: self.frame.origin.y, width: fy_width, height: self.frame.size.height)
        }
        get{
           return self.bounds.size.width
        }
    }
    
    //MARK: 设置或者获取UIView的宽度
    var fy_height:CGFloat{
        set{
            self.frame = CGRect(x: self.frame.origin.x, y: self.frame.origin.y, width: self.frame.size.width, height: fy_height)
        }
        get{
            return self.bounds.size.height
        }
    }
    
    
    //MARK: 设置或者获取UIView的x坐标
    var fy_x:CGFloat{
        set{
            self.frame = CGRect(x: fy_x, y: self.frame.origin.y, width: self.frame.size.width, height: self.frame.size.height)
        }
        get{
            return self.frame.origin.x
        }
    }
    
    //MARK: 设置或者获取UIView的y坐标
    var fy_y:CGFloat{
        set{
            self.frame = CGRect(x: self.frame.origin.x, y: fy_y, width: self.frame.size.width, height:self.frame.size.height)
        }
        get{
            return self.frame.origin.y
        }
    }

    
    //MARK: 设置或者获取UIView的maxX坐标
    var fy_maxX:CGFloat{
        get{
            return self.fy_x+self.fy_width
        }
    }
    
    //MARK: 设置或者获取UIView的maxY坐标
    var fy_maxY:CGFloat{
        get{
            return self.fy_y+self.fy_height
        }
    }
    
}

extension UIView{
    //MARK: 切圆角
    func corner(byRoundingCorners corners: UIRectCorner, radii: CGFloat) {
        let maskPath = UIBezierPath(roundedRect: self.bounds, byRoundingCorners: corners, cornerRadii: CGSize(width: radii, height: radii))
        let maskLayer = CAShapeLayer()
        maskLayer.frame = self.bounds
        maskLayer.path = maskPath.cgPath
        self.layer.mask = maskLayer
    }
}




enum FYError: Swift.Error {
    case NOFINT
}

extension UINib{
    //MARK: 加载XIB
    public class func readNibView(str: String) throws -> UIView {
        let nib = UINib.init(nibName: str, bundle: nil)
        if let view = nib.instantiate(withOwner: nil, options: nil).first as? UIView {
            return view
        }
        throw FYError.NOFINT
    }
}


//Mark:------------UIColor
extension UIColor{
    
    func fy_RGB(red:CGFloat,green:CGFloat,blue:CGFloat) -> UIColor {
        return fy_RGBA(red: red, green: green, blue: blue, alpha: 1.0)
    }
    func fy_RGBA(red:CGFloat,green:CGFloat,blue:CGFloat,alpha:CGFloat) -> UIColor {
        return UIColor.init(red: red/255.0, green: green/255.0, blue: blue/255.0, alpha: alpha)
    }
    
    func fy_hexColor(hexColor:String,defaultStringColor:String = "000000",alpha:CGFloat = 1.0) -> UIColor {
        var cString: String = hexColor.trimmingCharacters(in: NSCharacterSet.whitespacesAndNewlines)
        
        if cString.count < 6 {
            cString = defaultStringColor
        }
        if cString.hasPrefix("0X") || cString.hasPrefix("0x") {
            cString = String(cString.suffix(from: cString.index(cString.startIndex, offsetBy: 2)))
        }
        if cString.hasPrefix("#") {
            cString = String(cString.suffix(from: cString.index(cString.startIndex, offsetBy: 1)))
        }
        if cString.count != 6 {
            cString = defaultStringColor
        }
        
        var range: NSRange = NSMakeRange(0, 2)
        let rString = (cString as NSString).substring(with: range)
        range.location = 2
        let gString = (cString as NSString).substring(with: range)
        range.location = 4
        let bString = (cString as NSString).substring(with: range)
        
        var r: UInt32 = 0x0
        var g: UInt32 = 0x0
        var b: UInt32 = 0x0
        Scanner(string: rString).scanHexInt32(&r)
        Scanner(string: gString).scanHexInt32(&g)
        Scanner(string: bString).scanHexInt32(&b)
        return fy_RGBA(red: CGFloat(r), green: CGFloat(g), blue: CGFloat(b), alpha: alpha)
    }
    
}

//Mark:------------String
extension String{
    
    static let EMPTY = ""
    /// String使用下标截取字符串
    /// 例: "示例字符串"[0..<2] 结果是 "示例"
    subscript (r: Range<Int>) -> String {
        get {
            let startIndex = self.index(self.startIndex, offsetBy: r.lowerBound)
            let endIndex = self.index(self.startIndex, offsetBy: r.upperBound)
            
            return String(self[startIndex..<endIndex])
        }
    }
    
    //MARK: 返回一个字符串的前n位, 若字符串长不足n，则直接返回当前字符串
    func fy_start(length n: Int) -> String {
        if self.count < n {
            return self
        }
        if n < 0 {
            return self
        }
        let index = self.index(self.startIndex, offsetBy: n)
        return String(self[..<index])
    }
    
    
    //MARK: 返回一个字符串的后n位, 若字符串长不足n，则直接返回当前字符串
    func fy_last(length n: Int) -> String {
        if self.count < n {
            return self
        }
        let index = self.index((self.endIndex), offsetBy: -n)
        return String(self[index...])
    }
    
    //MARK: 删除所有的空格
    func fy_trimAll() -> String {
        return self.replacingOccurrences(of: " ", with: String.EMPTY)
    }
    
    
    //MARK: 判断是否包含数字和字母
    func fy_isPassWord() -> Bool {
        let numberRegex:NSPredicate = NSPredicate(format: "SELF MATCHES %@", "^.*[0-9]+.*$")
        
        let letterRegex:NSPredicate = NSPredicate(format: "SELF MATCHES %@", "^.*[A-Za-z]+.*$")
        
        if numberRegex.evaluate(with: self) && letterRegex.evaluate(with: self){
            return true
        }
        return false
    }
    
    
    //MARK: md5加密
    var fy_md5: String {
        let cStr = self.cString(using: .utf8)
        let digestLen = Int(CC_MD5_DIGEST_LENGTH)
        let buffer = UnsafeMutablePointer<UInt8>.allocate(capacity: digestLen)
        CC_MD5(cStr!,(CC_LONG)(strlen(cStr!)), buffer)
        
        let md5String = NSMutableString()
        for i in 0 ..< digestLen {
            md5String.appendFormat("%02X", buffer[i])
        }
        free(buffer)
        return md5String as String
    }
    
    //MARK: base64编码
    var fy_base64Encoding: String {
        let data = self.data(using: String.Encoding.utf8)
        var base64String = data?.base64EncodedString(options: .lineLength76Characters)
        base64String = base64String?.replacingOccurrences(of: "\r", with: "")
        return base64String ?? ""
    }
    
    //MARK: base64解码
    var fy_base64Decoded: String {
        
        let decodedData = Data(base64Encoded: self, options: Data.Base64DecodingOptions(rawValue: 0))
        return String(data: decodedData!, encoding: String.Encoding.utf8) ?? ""
    }
    
    //MARK: 返回188****8888类型字符串
    func fy_getSecretMobileNo() -> String {
        if self.isEmpty { return self }
        if self.count > 7 {
            return "\(self.fy_start(length: 3))****\(self.fy_last(length:4))"
        }else{
            return self;
        }
    }
    
    
    //MARK: 截取从start开始,长度为lenght的字符串
    ///
    /// - Parameters:
    ///   - start: 开始
    ///   - lenght: 长度
    /// - Returns: 处理结果
    func fy_startIndexToLenght(_ start: Int, lenght: Int) -> String {
        if start > self.count {
            return self
        }
        let startIndex = self.index(self.startIndex, offsetBy: start)
        if self.count < (start + lenght) {
            return String(self.suffix(from: startIndex))
        }
        let endIndex = self.index(self.startIndex, offsetBy: start + lenght)
        return String(self[startIndex..<endIndex])
    }
    
    //MARK: 判断链接中是否存在中文
    func fy_isIncludeChineseIn() -> Bool {
        for(_, value) in self.enumerated() {
            if value >= "\u{4E00}" && value <= "\u{9FA5}" {
                return true
            }
        }
        return false
    }

    //MARK: 判断是否有效邮箱
    ///
    /// - Returns: 结果
    func fy_isPeriodEmail() -> Bool {
        let email = "[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}"
        let regextestEmails = NSPredicate(format: "SELF MATCHES %@", email)
        
        return regextestEmails.evaluate(with: self)
    }
    
    //MARK: 判断是否有效身份证号
    ///
    /// - Returns: Bool
    func fy_isPeriodIdCard() -> Bool {
        
        if self.count != 18 {
            return false
        }
        
        let regex2 = "^(^[1-9]\\d{7}((0\\d)|(1[0-2]))(([0|1|2]\\d)|3[0-1])\\d{3}$)|(^[1-9]\\d{5}[1-9]\\d{3}((0\\d)|(1[0-2]))(([0|1|2]\\d)|3[0-1])((\\d{4})|\\d{3}[Xx])$)$"
        let identityCardPredicate = NSPredicate(format: "SELF MATCHES %@", regex2)
        let flag = identityCardPredicate.evaluate(with: self)
        if !flag {
            // 格式错误
            return flag
        } else {
            // 格式正确，判断合法性
            // 将前十七位加权因子保存在数组里
            let idCardWiArray = ["7", "9", "10", "5", "8", "4", "2", "1", "6", "3", "7", "9", "10", "5", "8", "4", "2"]
            // 这是除以11后，可能产生的11位余数， 验证码，也保存在数组里
            let idCardYArray = ["1", "0", "10", "9", "8", "7", "6", "5", "4", "3", "2"]
            var idCardArr = [Int]()
            var idCardWiSum = 0
            for index in 0..<17 {
                let subStrIndex = fy_startIndexToLenght(index, lenght: 1)
                let idCardWiIndex = idCardWiArray[index]
                // 数组保存所有乘积
                idCardArr.append(Int(subStrIndex)! * Int(idCardWiIndex)!)
            }
            
            // 将所有乘积相加
            for index in 0..<idCardArr.count {
                idCardWiSum += idCardArr[index]
            }
            
            // 计算出校验码所在数组的位置
            let idCardMod = idCardWiSum % 11
            // 得到最后一位身份证号码
            let idCardLast = fy_startIndexToLenght(17, lenght: 1)
            if idCardMod == 2 {
                if idCardLast == "X" || idCardLast == "x" {
                    return true
                } else {
                    return false
                }
            } else {
                if idCardLast == idCardYArray[idCardMod] {
                    return true
                } else {
                    return false
                }
            }
        }
    }
    
    //MARK: 正则匹配6-12位数字和大小写字母组合
    ///
    /// - Returns: Bool
    func fy_checkPassword() -> Bool {
        let password = "^(?![0-9]+$)(?![a-zA-Z]+$)[a-zA-Z0-9]{6,12}"
        let regextestPassword = NSPredicate(format: "SELF MATCHES %@", password)
        return regextestPassword.evaluate(with:self)
    }
    
    //MARK: 判断字符串是否包含其他字符串(必须全部一样)
    func fy_contains(find: String) -> Bool{
        return self.range(of: find) != nil
    }
    
    //MARK: 字符串转换成整型
    func fy_toInt() -> Int? {
        return Int(self)
    }
    
    //MARK: 识别有效手机号
    func fy_verifyPhoneNumber() -> Bool {
        let mobile = "^1((3[0-9]|4[5-68-9]|5[0-35-9]|6[6]|7[0-9]|8[0-9]|9[89])\\d{8}$)"
        let regextestmobile = NSPredicate(format: "SELF MATCHES %@",mobile)
        return regextestmobile.evaluate(with: self)
    }
    
    //MARK: 识别是否有效座机号 eg: 021-8688995
    func fy_landlineNumber() -> Bool {
        let strNum = "^(0\\d{2,3}-?\\d{7,8}$)"
        let checktest = NSPredicate.init(format: "SELF MATCHES %@", strNum)
        let isPhone = checktest.evaluate(with: self)
        
        let strNum1 = "^(\\d{7,8}$)"
        let checktest1 = NSPredicate.init(format: "SELF MATCHES %@", strNum1)
        let isPhone1 = checktest1.evaluate(with: self)
        
        if isPhone || isPhone1 {
            return true
        } else {
            return false
        }
    }

    
}





extension Array{
    //MARK: 数组转JSON字符串
    func arrayToString() -> String? {
        if let data = try? JSONSerialization.data(withJSONObject: self, options: JSONSerialization.WritingOptions.init(rawValue: 0)) {
            if let jsonStr = String.init(data: data, encoding: String.Encoding.utf8) {
                return jsonStr
            }
        }
        return nil
    }
}

```


