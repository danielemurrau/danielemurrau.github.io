
Linux Proxy
=====

|Proxy Environment Variables
Variable|	Description
http_proxy|	Proxy server for HTTP Traffic.
https_proxy|	Proxy server for HTTPS traffic
ftp_proxy|	Proxy server for FTP traffic
no_proxy|	Patterns for IP addresses or domain names that shouldn’t use the proxy

>Without username/pass:

$ export http_proxy=http://server-ip:port/

$ export http_proxy=http://127.0.0.1:3128/

$ export http_proxy=http://proxy-server.mycorp.com:3128/

>With username/pass:

$ export http_proxy=http://foo:bar@server-ip:port/

$ export http_proxy=http://foo:bar@127.0.0.1:3128/

$ export http_proxy=http://USERNAME:PASSWORD@proxy-server.mycorp.com:3128/


>Set proxy for all systrem users:

vi /etc/profile

export http_proxy=http://proxy-server.mycorp.com:3128/



