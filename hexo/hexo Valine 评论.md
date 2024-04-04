在 LeanCloud 注册一个账号并登录 https://console.leancloud.cn/apps
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402204003.png)

![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402204054.png)
创建完成后，进入应用的界面
找到设置中 **“应用凭证”**
我们需要用到 AppID、AppKey、服务器地址。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402204229.png)
打开 hexo 主题配置文件。
以 butterfly 为例
先将 Valine 启用
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402204420.png)
再在他下面找到 valine 的配置项
将上面的 AppID、AppKey、服务器地址 分别填入 appID, appKey, serverURL
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402204543.png)
保存之后
```shell
hexo clean
hexo g
hexo s
```
三连。
进入网站测试
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402204659.png)
