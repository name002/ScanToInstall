[mac 使用apache开启https功能，实现ios局域网内测（一）](http://www.cnblogs.com/Xujg/p/6077242.html)

#遇到问题
问题1
```
➜  ios sudo apachectl configtest
AH00526: Syntax error on line 22 of /private/etc/apache2/extra/httpd-vhosts.conf:
Invalid command '//#', perhaps misspelled or defined by a module not included in the server configuration
```
解决/private/etc/apache2/extra/httpd-vhosts.conf中
```
# match a ServerName or ServerAlias in any <VirtualHost> block.
#
 <VirtualHost *:808>
    DocumentRoot "/Users/admin/Documents/apacheforipa"//路径换成自己的
    ServerName localhost
    ErrorLog "/private/var/log/apache2/sites-error_log"
    CustomLog "/private/var/log/apache2/sites-access_log" common
    <Directory />
        Options Indexes FollowSymLinks MultiViews
        AllowOverride None
        Require all granted
#        Order deny,allow
#        Allow from all
    </Directory>
</VirtualHost> 
```
问题2
```
sudo apachectl configtest
AH00526: Syntax error on line 92 of /private/etc/apache2/extra/httpd-ssl.conf:
SSLSessionCache: 'shmcb' session cache not supported (known names: ). Maybe you need to load the appropriate socache module (mod_socache_shmcb?).
```
解决办法：
打开httpd.conf，找到 LoadModule socache_shmcb_module modules/mod_socache_shmcb.so，把前面的注释去掉。

问题3
iOS10.2之前版本能够安装APP，之后的报"无法连接192.168.xx.xx"
解决办法：
将plist放到受信任的https域名下
[iOS企业版(Enterprise) App发布，Safari打开URL显示无法连接"xxx"解决办法](http://blog.csdn.net/u012138272/article/details/77541947)
![https域名下存放plist.png](http://upload-images.jianshu.io/upload_images/2061411-0473419afc437d62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#引用
[mac 使用apache开启https功能，实现ios局域网内测（一）](http://www.cnblogs.com/Xujg/p/6077242.html)

