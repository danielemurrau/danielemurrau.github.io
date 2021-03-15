Linux Proxy
=====
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



