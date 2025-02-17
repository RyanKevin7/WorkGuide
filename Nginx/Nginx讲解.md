### Nginx简介

> Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，在BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实上nginx的并发能力在同类型的网页服务器中表现较好。并发能力: 50,000

#### **1.  为什么使用Nginx**

> **高性能**：Nginx是一个高性能的HTTP和反向代理服务器，能够处理大量的并发连接和请求，适合高流量的网站。
>
> **高可靠性**：Nginx使用事件驱动和异步处理方式，能够在保持高性能的同时，提供高可靠性的服务。
>
> **灵活性**：Nginx支持多种配置方式，可以通过配置文件灵活地调整其行为，满足不同的需求。
>
> **扩展性**：Nginx可以通过模块扩展其功能，支持负载均衡、缓存、SSL加密等多种功能。
>
> **低资源消耗**：Nginx是一个轻量级的服务器，占用的系统资源较少，适合在资源有限的环境中部署。
>
> **跨平台**：Nginx支持多种操作系统，包括Linux、Unix、MacOS等，具有很好的跨平台兼容性。
>
> **社区支持**：Nginx有一个活跃的开源社区，提供了大量的文档、教程和模块，方便用户学习和使用。
>
> **安全性**：Nginx提供了一些基本的安全功能，如防止DDoS攻击、防止SQL注入等，可以提高网站的安全性。
>
> **易于维护**：Nginx的配置文件简单明了，易于理解和维护，降低了运维的难度。
>
> **支持多种协议**：Nginx不仅支持HTTP和HTTPS协议，还支持其他协议如SMTP、POP3等，可以作为多种服务的代理服务器。




![img](https://i-blog.csdnimg.cn/direct/b4744f12ca1b41cb93d165f55d2d560b.png)

#### **2. 安装Nginx**

  > nginx可以独立安装在一台服务器–也可以和项目在同一个服务器。

  **安装Nginx的依赖插件**

  > yum install -y gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl-devel

**下载nginx**

> 源码。 编译—安装
>
> [nginx: download(https://nginx.org/en/download.html)



**创建一个目录作为nginx的安装路径**

> mkdir /usr/nginx

**解压**

>  tar -zxvf nginx-1.26.1.tar.gz

**进入解压后的目录**

>  cd nginx-1.26.1

**指定nginx的安装路径**

> ./configure --prefix=/usr/nginx

**编译和安装**

> nginx make install

**nginx目录结构**

![img](https://i-blog.csdnimg.cn/direct/f80eaefadd8249128b88069e01b177e4.png)

**启动nginx**

> nginx 启动
> nginx -s stop 关闭
> nginx -s reload 重新加载配置文件

**访问nginx 80**

> http://nginx所在的ip:nginx的端口/

![img](https://i-blog.csdnimg.cn/direct/38599db1acae43a3a375cb9b3586b5e0.png)

**nginx配置文件**

```
#user  nobody; 
#工作的线程数
worker_processes  1;
?
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;
?
#pid ? ? ?  logs/nginx.pid;
?
?
events {
 ?  # 每个工作对象允许的连接数
 ?  worker_connections  1024;
}
?
?
http {
 ?  include ? ? ? mime.types;
 ?  default_type  application/octet-stream;
?
 ?  #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
 ?  # ? ? ? ? ? ? ? ?  '$status $body_bytes_sent "$http_referer" '
 ?  # ? ? ? ? ? ? ? ?  '"$http_user_agent" "$http_x_forwarded_for"';
?
 ?  #access_log  logs/access.log  main;
?
 ?  sendfile ? ? ?  on;
 ?  #tcp_nopush ? ? on;
?
 ?  #keepalive_timeout  0;
 ?  keepalive_timeout  65;
?
 ?  server {
 ? ? ? listen 81;
 ? ? ? server_name localhost;
 ? ? ? location /{
 ? ? ? ? ? root static;
 ? ? ? ? ? index main.html;
 ? ? ? ? ?
 ? ? ? }
 ?  }
?
 ?  #gzip  on;
 ?  server {
 ? ? ?  listen ? ? ? 80; # 监听的端口号
 ? ? ?  server_name  localhost; # 监听的主机名.域名
?
 ? ? ?  #charset koi8-r;
?
 ? ? ?  #access_log  logs/host.access.log  main;
?
?
 ? ? ?  # 资源/ 
 ? ? ?  location / {
 ? ? ? ? ?  root ? html; #根目录
 ? ? ? ? ?  index  index.html main.html; # 资源
 ? ? ?  }
?
 ? ? ?  #error_page  404 ? ? ? ? ? ?  /404.html;
?
 ? ? ?  # redirect server error pages to the static page /50x.html
 ? ? ?  #
 ? ? ?  error_page ? 500 502 503 504  /50x.html;
 ? ? ?  location = /50x.html {
 ? ? ? ? ?  root ? html;
 ? ? ?  }
?
 ? ? ?  # proxy the PHP scripts to Apache listening on 127.0.0.1:80
 ? ? ?  #
 ? ? ?  #location ~ .php$ {
 ? ? ?  # ?  proxy_pass ? http://127.0.0.1;
 ? ? ?  #}
?
 ? ? ?  # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
 ? ? ?  #
 ? ? ?  #location ~ .php$ {
 ? ? ?  # ?  root ? ? ? ? ? html;
 ? ? ?  # ?  fastcgi_pass ? 127.0.0.1:9000;
 ? ? ?  # ?  fastcgi_index  index.php;
 ? ? ?  # ?  fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
 ? ? ?  # ?  include ? ? ?  fastcgi_params;
 ? ? ?  #}
?
 ? ? ?  # deny access to .htaccess files, if Apache's document root
 ? ? ?  # concurs with nginx's one
 ? ? ?  #
 ? ? ?  #location ~ /.ht {
 ? ? ?  # ?  deny  all;
 ? ? ?  #}
 ?  }
?
?
 ?  # another virtual host using mix of IP-, name-, and port-based configuration
 ?  #
 ?  #server {
 ?  # ?  listen ? ? ? 8000;
 ?  # ?  listen ? ? ? somename:8080;
 ?  # ?  server_name  somename  alias  another.alias;
?
 ?  # ?  location / {
 ?  # ? ? ?  root ? html;
 ?  # ? ? ?  index  index.html index.htm;
 ?  # ?  }
 ?  #}
?
?
 ?  # HTTPS server
 ?  #
 ?  #server {
 ?  # ?  listen ? ? ? 443 ssl;
 ?  # ?  server_name  localhost;
?
 ?  # ?  ssl_certificate ? ?  cert.pem;
 ?  # ?  ssl_certificate_key  cert.key;
?
 ?  # ?  ssl_session_cache ?  shared:SSL:1m;
 ?  # ?  ssl_session_timeout  5m;
?
 ?  # ?  ssl_ciphers  HIGH:!aNULL:!MD5;
 ?  # ?  ssl_prefer_server_ciphers  on;
?
 ?  # ?  location / {
 ?  # ? ? ?  root ? html;
 ?  # ? ? ?  index  index.html index.htm;
 ?  # ?  }
 ?  #}
?
}
```

### **Nginx的核心功能**

**反向代理**：‌Nginx可以作为反向代理服务器，‌将客户端的请求转发到后端服务器，‌实现负载均衡和故障转移。‌
**负载均衡**：‌通过配置多个后端服务器，‌Nginx可以智能地分配请求到不同的服务器，‌以提高系统的整体性能和可靠性。‌
**动静分离**：‌Nginx可以作为静态内容服务器，‌处理动态网页中的静态部分，‌实现动静分离，‌提高网站访问速度。‌
**正向代理**：‌虽然Nginx主要作为反向代理使用，‌但它也支持正向代理功能，‌允许用户通过代理服务器访问外部网络资源。‌


#### **1. 反向代理**

**反向代理服务器**

>  代理的为服务器端。对于客户来说不知道服务器的信息。例如: nginx

![img](https://i-blog.csdnimg.cn/direct/5ead8c714b704cfd92d55c7296a218a2.png)

项目部署图

![img](https://i-blog.csdnimg.cn/direct/9c1e2c680b2c4476a08fc7eacba6edd2.png)

> 这是我的端口：
>
> 准备web项目—103。
>
> 准备nginx----101



**启动web项目**

![img](https://i-blog.csdnimg.cn/direct/83b4658f09c24af4a92d9ed6a50938d6.png)

**配置nginx**

> server {
> listen 82;
> server_name localhost;
> location /{
> 	 //代理的服务器地址
> proxy_pass http://192.168.111.132:8080;
> }
> }



**启动nginx**

> ./opt/nginx/sbin/nginx



#### **2. 负载均衡**
  > 负载均衡（Load Balance [4]）其意思就是把请求分摊到多个操作单元上进行执行，例如Web服务器、FTP服务器、企业关键应用服务器和其它关键任务服务器等，从而共同完成工作任务。

> web项目必须搭建的为集群模式。

![img](https://i-blog.csdnimg.cn/direct/9b64c4a74bb94f1389288cd680df4857.png)

> web服务器项目至少搭建2台以上。192.168.111.132 8081 8082
> nginx服务器



**springboot项目**

![img](https://i-blog.csdnimg.cn/direct/33a00fd1b7134d698d360a6f2e54365f.png)

**解压**

>  java -jar xxx.jar

![img](https://i-blog.csdnimg.cn/direct/4cca97630fb2402a96f973a3ace7c8a1.png)

**配置nginx完成负载均衡**

![img](https://i-blog.csdnimg.cn/direct/2d146a55826c4059a528edbcba2c8e9f.png)

**重新加载nginx配置**

>  /usr/nginx/sbin/nginx -s reload

**测试**

>  http://192.168.111.188:83/getInfo



**负载均衡的策略**

默认为轮询。

权重策略: 服务器硬件配置不同时。

![img](https://i-blog.csdnimg.cn/direct/587a6fcb7671481c87805be1b01c4ee6.png)

ip_hash策略: 根据访问者客户的ip固定访问对应的web服务器。

![img](https://i-blog.csdnimg.cn/direct/672786d0ef9246bfb15e0cf82fc03504.png)

花钱买第三方策略插件:

#### **3. 动静分离**

> 动：动态资源[接口] 静:静态资源 [css js image]。
>
> 分离: 之前我们把静态资源和动态资源全部放在web服务器下。 把静态资源放入nginx服务器下。动态资源web服务器下

![img](https://i-blog.csdnimg.cn/direct/a3292eedb93d4467a0f609e0a5995f60.png)

**准备web项目**

![img](https://i-blog.csdnimg.cn/direct/e5a150105e374256890540ba36c442c0.png)

**把静态资源放到nginx中**

![img](https://i-blog.csdnimg.cn/direct/d904562aae0f44c1bf12c43ebca0a57c.png)

**配置nginx**

![img](https://i-blog.csdnimg.cn/direct/eb4a81ff323342fcb03f62b8a573d7f2.png)

**测试**

![img](https://i-blog.csdnimg.cn/direct/93115fbc406742ccb76ac3206e9f050d.png)

#### **4. 正向代理**

> 代理的为客户端，对于服务器不知道真实客户的信息。例如:翻墙软件。

![img](https://i-blog.csdnimg.cn/direct/c5a512b9a6be49038dc00764ee60d1da.png)







原文链接：https://blog.csdn.net/m0_74823094/article/details/144300868