# haproxy
an haproxy compile for 2.4 with support of kubernetes lua and acl maps 
scraps
setsebool -P haproxy_connect_any 1

Note: for logging:
 vim /etc/rsyslog.conf

module(load="imudp") # needs to be done just once
input(type="imudp" port="514")
 cd /etc/rsyslog.d/
 vi haproxy.conf

local2.=info     /var/log/haproxy-access.log    # For Access Log
local2.notice    /var/log/haproxy-info.log      # For Service Info - Backend, loadbalancer

Note:if you compile haproxy 2.4X while compiling repalce:
EXTRA_OBJS="contrib/prometheus-exporter/service-prometheus.o"
with:
USE_PROMEX=1

Note: the 2.4 LUA integration requires LUA 5.3+ 
Need to get that and compile it from

curl -R -O http://www.lua.org/ftp/lua-5.4.3.tar.gz

-final successful command to compile: 
make TARGET=linux-glibc USE_LUA=1 USE_OPENSSL=1 USE_PROMEX=1 USE_PCRE=1 PCREDIR= USE_ZLIB=1 USE_SYSTEMD=1 LUA_LIB=/opt/lua-5.4.3/src LUA_INC=/opt/lua-5.4.3/src 
