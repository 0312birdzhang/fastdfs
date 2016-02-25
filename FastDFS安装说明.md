#FastDFS 5.05安装文档
##安装参考
>[FastDFS的安装与配置](http://support.supermap.com.cn/DataWarehouse/WebDocHelp/6.1.3/iserverOnlineHelp/Server_Service_Management/CacheConfig/FastDFS_install_config/FastDFSconfig.htm)


##下载libfastcommon跟fastdfs
[https://github.com/happyfish100/libfastcommon/archive/V1.0.7.tar.gz](https://github.com/happyfish100/libfastcommon/archive/V1.0.7.tar.gz)

[https://github.com/happyfish100/fastdfs/archive/V5.05.tar.gz](https://github.com/happyfish100/fastdfs/archive/V5.05.tar.gz)

##安装
####1.安装libfastcommon
```
tar -xvf V1.0.7.tar.gz
cd libfastcommon-1.0.7
sudo ./make.sh
sudo ./make.sh install

```
###2.安装fastdfs
```
tar -xvf V5.05.tar.gz
cd fastdfs-5.05
sudo ./make.sh
sudo ./make.sh install
```

##修改配置
fastdfs安装完的配置文件都在<code>/etc/fdfs/</code>目录下
```
[root@CentOS-192-168-1-226 fdfs]# ll
总用量 56
-rw-r--r-- 1 root root  1465 2月  25 11:54 client.conf
-rw-r--r-- 1 root root   858 2月  25 11:46 http.conf
-rw-r--r-- 1 root root 31172 2月  25 11:46 mime.types
-rwxr-xr-x 1 root root  7391 2月  25 11:46 storage.conf
-rwxr-xr-x 1 root root  6363 2月  25 11:57 tracker.conf
```

##运行
####1.运行tracker服务
<code>/usr/local/bin/fdfs_trackerd /etc/fdfs/tracker.conf</code>
如果是linux则可以用服务运行<code>service fdfs_trackerd start</code>

####2.运行storage服务
<code>/usr/local/bin/fdfs_storaged /etc/fdfs/storage.conf</code>
如果是linux则可以用服务运行<code>service fdfs_storaged start</code>

####3.运行测试程序
测试方法：
```
/usr/local/bin/fdfs_test <client_conf_filename> <operation>
/usr/local/bin/fdfs_test1 <client_conf_filename> <operation>
```
示例：
```
/usr/local/bin/fdfs_test conf/client.conf upload /usr/include/stdlib.h
```

####4.运行监控程序
调用方法：
```
/usr/local/bin/fdfs_monitor <conf_filename>
```
示例：
```
/usr/local/bin/fdfs_monitor /etc/fdfs/storage.conf
```
####5.停止服务器
调用方式：
```
/usr/local/bin/stop.sh <conf_filename>
```
示例：
```
/usr/local/bin/stop.sh /etc/fdfs/storage.conf
```


##常见问题

| Question  | Answer |
| :------------: |:---------------:|
| file: ../common/sockopt.c, line: 742, bind port 22122 failed, errno: 98, error info: Address already in use. |  |
|error while loading shared libraries: libevent-1.4.so.2: cannot open shared object file: No such file or directory|ln -s /usr/local/lib/libevent-1.4.so.2 /usr/lib64/libevent-1.4.so.2|
|tracker_query_storage fail, error no: 28, error info: No space left on device|修改 tracker.conf 文件中的 reserved_storage_space = 1%|
