## <p align="center">DEMO中IOS打包遇到的问题汇总</p>##

###遇到的问题索引###
- 手机IOS版本太新，Xcode支持的最新版本低于手机版本
- IOS真机调试时，Xcode提示：**Development cannot be enabled while your device is locked**
- IOS真机调试时，Xcode提示：**Processing Symbol Files in Xcode**
- Xcode

###问题的解决方法###
- 更新Xcode到最新版本，但自动更新费时费力，可以手动更新，或者单独更新某个版本的手机调试包（例如IOS10.3），手动更新的办法：进入到目录/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport， 然后从https://pan.baidu.com/s/1jHO0ouy 中下载到调试包，最后重启Xcode，就可以了。
- 提示原因是由于第一次连接该iphone，不小心点击了不信任选项导致的。这个时候要清除iphone的隐私设置，重新插拔数据线才可以。清除隐私设置的方法：点击 设置 --> 通用 --> 重置  --> 重置位置和隐私。
- 提示原因是因为刚开始连接iphone的时候回弹出来一些窗口，这些窗口可以看到你手机的照片等等，这些窗口和Xcode处理系统Symbol Files有关，如果立马关闭，将会导致Symbol Files 处理出现问题，之后再点击调试就会出现该提示：解决方法是，重新插拔数据线，弹出来的窗口不用关闭，直接点Xcode，等Xcode处理完Symbol Files 。 
















