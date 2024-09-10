# find 命令

##  find命令是Linux系统中非常强大的工具，用于搜索文件和目录。

#### 按名称搜索
 `find /path/to/seach -name "filename"`
#### 搜索文件 ：
  `find /path/to/seach -type f -name "filename"`
#### 搜索目录 ： 
   `find /path/to/seach -type d -name "filename"`
#### 按时间搜索：  最近7天内修改的文件
   `find /path/to/seach -mtime -7 `
#### 搜索大于100M的文件
   `find /path/to/seach -type d -size +100M`
>[!note] 
> 其中 `/path/to/seach`代表路径，根据实际情况修改
`/`为根目录， `.`是当前目录 `-type f` 是搜索文件，`-type d` 是搜索目录，`-type l`表示链接，
 `-type b`  表示设备块。
>
      
