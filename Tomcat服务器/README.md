## 服务器

对于tomcat服务器用于java web应用程序，而apache服务器本身只支持处理静态的HTML资源。

## nginx gzip 


| 方法 | 描述 |
| ------ | ------ |
| gzip on; | 开启Gzip |
| gzip_min_length | 不压缩临界值，大于1K的才压缩，一般不用改 |
| gzip_buffers  | buffer |
| gzip_http_version | 用了反向代理的话，末端通信是 HTTP/1.0；默认是 HTTP/1.1 |
| gzip_comp_level | 压缩级别，1-10，数字越大压缩的越好，时间也越长,越浪费 CPU 计算资源 |
| gzip_types | 进行压缩的文件类型，JavaScript有两种写法 application/javascript |
| gzip_vary | 跟Squid等缓存服务有关，on 的话会在 Header 里增加 "Vary: Accept-Encoding" |
| gzip_disable | IE6 对 Gzip 不怎么友好，不给它Gzip了 |

- 图片启用 GZip压缩 会适得其反，因为不仅浪费了CPU，还增大了体积，势必影响服务器性能，影响网站速度;

- **需要与 webpack GZip 配合使用；**

```php
server {
    listen       80;
    server_name  localhost;

    #gzip 调优
    gzip  on;
    gzip_disable “MSIE[1 - 6].(?!.* SV1) ”;
    gzip_http_version 1.0;
    gzip_vary on;
    gzip_proxied any;
    gzip_min_length 1k;
    gzip_buffers 4 16k;
    gzip_comp_level 6;
    gzip_types text / plain text / css text / xml text / javascript application / json application / x - javascript application / xml application / xml + rss application / javascript;
}
```