# march-work
Codes of work during march

nginx: [emerg] invalid number of arguments in "location" directive in /etc/nginx/conf.d/default.conf:38


proxy_cache_path /tmp/nginx levels=1:2 keys_zone=cache:1m inactive=24h use_temp_path=off;

# Languages supported
map $http_accept_language $accept_language {
  ~*^en-US en-US;
  ~*^es es;
}

server {
  listen 8080;
  server_name localhost;
  port_in_redirect off;
  include conf.d/gzip.conf;
  include conf.d/common-headers.conf;
  large_client_header_buffers 4 16k;
  root /usr/share/nginx/html;

  # check cookie _dwlan
  if ($cookie__dwlan ~ "^(es|en-US)$" ) {
    set $language $1;
  }

  # if no cookie set language to accept-language http header
  if ($cookie__dwlan ~ "^$") {
    set $language $accept_language;
  }

  # health check
  location /health {
    stub_status on;
    access_log off;
    allow 127.0.0.1;
    allow 10.0.0.0/8;
    deny all;
  }

  # Shell-lite: request to config properties from ConfigMaps
  location ~ ^<%= ENV["relativePath"] %>/(en-US|es)/tot-oappre-helpcenteruisl/config.json {
    alias /etc/san-configmap-darwin/config-sl.json;
  }

  # Microfront: request to config properties from ConfigMaps
  location ~ ^<%= ENV["relativePath"] %>/(en-US|es)/tot-oappre-helpcenterui/config.json {
    alias /etc/san-configmap-darwin/config.json;  
  }

  # Microfront: serve the app
  location ~ ^<%= ENV["relativePath"] %>/(es|en-US) {
    if ($request_method = POST ) {
      return 405;
    }
    include conf.d/common-headers.conf;
    add_header Set-Cookie "_dwlan=$1; SameSite=Lax;Secure;Path=<%= ENV["relativePath"] %>/";
    try_files $uri <%= ENV["relativePath"] %>/$1/index.html?$args;
    index index.html;
  }

  location / {
    return 301 https://$host/$language$request_uri;
  }
}
