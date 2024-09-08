## 1. Samba安装

``` shell
apt install samba
```
## 2. 创建用户

  > 创建一个用于访问共享的账户“smbuser”并设置密码

```
useradd -s /sbin/nologin smbuser
smbpasswd -a smbuser
```
## 3. 创建共享文件夹
> 创建一个共享文件夹并设定相应权限，这里设定权限为777 
```
mkdir /opt/share/
chmod 777 /opt/share
```
 ## 4. 修改配置文件
 ```
vim /etc/samba/smb.conf
```
> 在最后增加以下内容
```
 [smbuser]
 # 自定义的共享设置 
    #共享描述
    comment = smbuser guest share 

    #共享目录-也就是前面创建的共享目录
    path = /opt/share

    #允许guest用户访问
    public = yes    

    #允许smbuser 在共享目录下写入
    writable = yes 

     #默认创建目录权限 rwxrwxr_x
    directory mask = 0775  

    #默认创建文件权限 rwxrwxr_x
    create mask = 0775 

    #允许访问该共享的用户
    valid users = smbuser,root  

    #可写入共享的用户列表
    write list = smbuser,root  

    #该指定共享目录可浏览
    browseable = yes   

    #该指定共享资源可使用
    available = yes     

    # 设置共享目录的管理员，具有完全权限-一般如非必要不要开启管理员权限
    admin users = smbuser
```
## 5. 重启服务
```
systemctl restart smb
systemctl restart nmb
```
<!-- ##{"script":"<script src='https://blog.meekdai.com/Gmeek/plugins/GmeekTOC.js'></script>"}## -->