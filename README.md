---
# Pixiv Illustration Collection
-------------
一个提供有限的pixiv日排行与高级会员搜索的站点

![](https://img.shields.io/github/stars/OysterQAQ/Pixiv-Illustration-Collection.svg) ![](https://img.shields.io/github/forks/OysterQAQ/Pixiv-Illustration-Collection.svg) ![](https://img.shields.io/badge/license-AGPLv3-blue.svg)


### Link:https://pixivic.com

### Bright Point:
- 前后端完全分离
- 三图床混合优化图片加载体验
- 匿名回复邮件提醒(昵称与邮件由cookie与url携带进行自动填充)
- Nginx反向代理(作为跳板优化延迟与tomcat集群动静分离)
- 原生js
- PC端移动端单独适配(Nginx UA判断跳转)
- 爬虫业务与web业务服务端分别分布
#### v2.0的预计变化

> 功能的增加

- 增加周排行，月排行
- 漫画类型的查看
- gif图片的显示与下载(仅提供600*600尺寸)
- 查看更详细的画作信息
- 查看画师信息

> 技术栈迭代

- jdk: 11(编程风格的变化与一些流式操作带来的并行化好处)
- web: spring web reactive
- db: mongodb
- httpclient: jdk11 httpclient (本地爬虫)、webclient(服务端实时请求)
- image processor: graphics magick(call by gm4java)(主要是gif的合成与过大图片的压缩)

> 体验优化

- 本地爬虫使用https请求替代ssl远程连接服务端数据库
- 将根据p站原生的内容分级调整图床(非动态图片级数大于5上传uploadcc，小于5上传新浪图床，动态图片上传imgur)，将减少新浪图床的和谐造成的不便
- 更快的web体验
- 将部署多台图片反代服务器(目前准备两台)


### 伺服器:
- 本地arm服务器:作为爬虫服务器,每日五点爬取pixiv三天前的日排行数据
- Aws lightsail:反向代理图片请求过程中添加referer请求头,绕过防盗链
- Uovz香港:反向代理pixiv搜索api,加速访问,延迟提升500ms
- 息壤 北京:作为主web服务器之一,nginx tomcat动静分离
- 阿里云 深圳:作为主web服务器之一,nginx tomcat动静分离

### 架构图:
![Image text](https://ws4.sinaimg.cn/large/006346uDgy1fwkh7hxmtjj31pr15t7dn.jpg)

### 使用方法
更改conf.xml文件与druid配置文件即可

### TODO
重构:
* web:spring reacive web
* crawler:jdk11 httpclient

## License
AGPL v3