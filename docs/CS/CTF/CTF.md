# Web

## HTTP协议

请求方式  
302跳转  
Cookie  
基础认证  
响应包源代码  

## 信息泄露

目录遍历  
PHPINFO  

备份文件下载  
网站源码  
bak文件  会在修改某个文件的时候先复制一份，将其命名为xxx.bak
vim缓存  vim缓存文件第一次生成.swp文件  
.DS_Store  DS_Store是MacOS保存文件夹的自定义属性的隐藏文件。通过.DS_Store可以知道这个目录里面所有文件的清单。  

Git泄露  
SVN泄露  
HG泄露  

## 密码口令

弱口令  
字典爆破  
默认口令  
社会工程  

## SQL注入

整数型注入  
字符型注入  
报错注入  
布尔盲注  
时间盲注  
MySQL结构  
Cookie注入  
UA注入  
Refer注入  
二次注入  
Where后注入  
AND/OR注入  
ORDER BY 注入  
UPDATE注入  
INSERT注入  
过滤空格  
综合训练 SQLI-LABS  

## XSS

反射型  
存储型  
DOM反射  
DOM跳转  
过滤空格  
过滤关键词  

## 文件上传

无验证  
前端验证  
.htaccess  
MIME绕过  
00截断  
后缀大小写绕过  
点绕过  
空格绕过  
双写后缀  
文件头检查  
突破getimagesize()  
突破exif_imagetype()  
二次渲染  

## RCE

无过滤执行  
过滤空格
eval执行
文件包含
php://input  
读取源代码
远程包含
命令注入
过滤cat  
过滤空格
过滤目录分隔符
过滤运算符
综合过滤练习  

## SSRF

内网访问  
伪协议读取文件  
端口扫描  

POST请求  
上传文件  
FastCGI协议  
Redis协议  
  
URL Bypass  
数字IP Bypass    
302跳转 Bypass  
DNS重绑定 Bypass    