# ChatGPT-Web

#### 介绍
{**以下是 Gitee 平台说明，您可以替换此简介**

chatgpt-web.html 对应java后端
chatgpt-web-Py.html 对应python后端

#### 软件架构
软件架构说明


#### 安装教程

1.  xxxx
2.  xxxx
3.  xxxx

#### 使用说明

可以当作静态页面用，直接放在nginx的html下，配置好路径即可启动nginx后访问
记得把页面请求后端地址改成自己的后端，或者放弃后端，直连chatgpt接口。


nginx参考配置如下：

#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
worker_connections  1024;
}


http {
include       mime.types;
default_type  application/octet-stream;


    sendfile        on;

    keepalive_timeout  600;
		fastcgi_connect_timeout 600;
		fastcgi_send_timeout 600;
		fastcgi_read_timeout 600;
		proxy_connect_timeout 600;
		proxy_send_timeout 600;
		proxy_read_timeout 600;
		send_timeout 600;
        #注意！！！
        #流式响应，必须记得关闭nginx缓存。
		proxy_buffering off;

    server {

		    listen       1443 default ssl;
    	  listen       [::]:1443 default ssl;
				server_name  127.0.0.1;
				
		    #ssl_certificate     anxinServerCA.cer;

		    #ssl_certificate_key anxinServerCA.pvk;
		    
				ssl_certificate     8295139__runjian.com.pem;
					 
				ssl_certificate_key 8295139__runjian.com.key;
		    
				ssl_session_cache    shared:SSL:1m;
					 
				ssl_session_timeout  5m;
					 
				ssl_ciphers  HIGH:!aNULL:!MD5;
					 
				ssl_prefer_server_ciphers  on;
				
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

				location / {
        		proxy_pass   http://127.0.0.1:801;
		        proxy_http_version 1.1;
		        proxy_set_header Connection "";
   	 		}
   	 		
   	 		location /api/ {
						proxy_pass http://127.0.0.1:8080/api/;
		        proxy_http_version 1.1;
		        proxy_set_header Connection "";
				}
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

    server {

		    listen       8011 default ssl;
    	  listen       [::]:8011 default ssl;
				server_name  127.0.0.1;
				
		    #ssl_certificate     anxinServerCA.cer;

		    #ssl_certificate_key anxinServerCA.pvk;
		    
				ssl_certificate     8295139__runjian.com.pem;
					 
				ssl_certificate_key 8295139__runjian.com.key;
		    
				ssl_session_cache    shared:SSL:1m;
					 
				ssl_session_timeout  5m;
					 
				ssl_ciphers  HIGH:!aNULL:!MD5;
					 
				ssl_prefer_server_ciphers  on;
				
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

				location / {
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "Upgrade";
		        proxy_http_version 1.1;
		        proxy_set_header Connection "";
            root   html;
            index  chatgpt-web-Py.html;
   	 		}
   	 		
				location /user {
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "Upgrade";
        		proxy_pass   http://127.0.0.1:8020;
		        proxy_http_version 1.1;
		        proxy_set_header Connection "";
   	 		}
    }

    server {

		    listen       8012 default ssl;
    	  listen       [::]:8012 default ssl;
				server_name  127.0.0.1;
				
		    #ssl_certificate     anxinServerCA.cer;

		    #ssl_certificate_key anxinServerCA.pvk;
		    
				ssl_certificate     8295139__runjian.com.pem;
					 
				ssl_certificate_key 8295139__runjian.com.key;
		    
				ssl_session_cache    shared:SSL:1m;
					 
				ssl_session_timeout  5m;
					 
				ssl_ciphers  HIGH:!aNULL:!MD5;
					 
				ssl_prefer_server_ciphers  on;
				
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

				location / {
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "Upgrade";
		        proxy_http_version 1.1;
		        proxy_set_header Connection "";
            root   html;
            index  chatgpt-web-PyA.html;
   	 		}
   	 		
				location /userA {
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "Upgrade";
        		proxy_pass   http://127.0.0.1:8021;
		        proxy_http_version 1.1;
		        proxy_set_header Connection "";
   	 		}
    }
server {

		    listen       801 default;
    	  listen       [::]:801 default;
				server_name  _;
				
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "Upgrade";
		        proxy_http_version 1.1;
		        proxy_set_header Connection "";
            root   html;
            index  chatgpt-web.html;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
}

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


#### 特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  Gitee 官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解 Gitee 上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是 Gitee 最有价值开源项目，是综合评定出的优秀开源项目
5.  Gitee 官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  Gitee 封面人物是一档用来展示 Gitee 会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
