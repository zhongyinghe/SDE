让nginx支持PATHINFO模式的配置:
================
```
server {  
    listen       80; 
    server_name  localhost;
    
    
    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;
    set $root /usr/share/nginx/html;
    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm index.php;
	
	if ( -f $request_filename) {
		break;
	}

	if ( !-e $request_filename) {
		rewrite ^(.*)$ /index.php/$1 last;
		break;
	}
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #隐藏入口文件的设置
    location /tp5/public/ {
    	if (!-e $request_filename){
    		rewrite ^/tp5/public/(.*)$ /tp5/public/index.php/$1 last;
    	}
    }
    location ~ \.php($|/) {
        #root  /usr/share/nginx/html;
        fastcgi_pass   127.0.0.1:9000;
	fastcgi_split_path_info ^((?U).+.php)(/?.+)$;
	fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_index  index.php;
	fastcgi_param  PATH_TRANSLATED  $document_root$fastcgi_path_info;
        fastcgi_param  SCRIPT_FILENAME  $root$fastcgi_script_name;
        include        fastcgi_params;
    }

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
```

