# ngx_http_pipelog_module

This module allows to send HTTP access log to an external program via pipe.

Installation
===

***Clone the code***
    
    git clone git://github.com/pandax381/ngx_http_pipelog_module.git

***Build nginx with ngx_http_pipelog_module***

    ./configure --add-module=/path/to/ngx_http_pipelog_module
    make && sudo make install

Note: This module has been tested with nginx 1.5.6 and 1.4.3

Directives
===

***pipelog_format***
  
    pipelog_format name string ...

  * syntax is same as log_format of HttpLogModule.
  * default value is *combined*.

***pipelog***

    pipelog command [format [nonblocking] [if=condition]];
 
    pipelog off;
    
  * default value is *off*. 

Example
===

      pipelog_format main '$remote_addr - $remote_user [$time_local] "$request" '
                        '$status $body_bytes_sent "$http_referer" '
                        '"$http_user_agent" "$http_x_forwarded_for"';
      
      pipelog "cat >> /var/log/nginx/access.log" main;
