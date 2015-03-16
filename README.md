# Examples for Fastcgi Container

[Fastcgi Container](<https://github.com/lpre/Fastcgi-Container) is a framework for development of high performance web applications in C++.

# License 

[GPL v.3.0](LICENSE)

# Requirements

* A C++11 compliant compiler with complete support of C++11 regex (e.g., GCC 4.9 meets the minimum feature set required to build the package)
* GNU build system (Autotools)

# Dependencies

* [Fastcgi Container](<https://github.com/lpre/Fastcgi-Container)

# Docs

* [API](https://github.com/lpre/Fastcgi-Container/docs/API.md) (coming soon)
* [C++ Page Compiler](https://github.com/lpre/Fastcgi-Container/page-compiler/docs/page_compiler.md)

# Examples

The following examples are provided:

* Simple request handler
* Simple request filter
* Simple servlet
* Form authentication filter
* Simple athorization realm

## Build

The project is using GNU Autotools. To build it, execute the following commands in the root directory of the project:

	./autogen.sh
	./configure
	make

## Configuring examples to run with HTTPD server 

Copy built shared libraries from `example/.libs` as well as configuration file `example/fastcgi.conf` into working directory (e.g. `~/tmp/fscgi`). Modify configuration file as appropriate.

Configure available HTTPD server to connect with Fastcgi Container. 

For example, to run examples via Unix socket with Apache2 HTTPD using modules `mod_poxy` and `mod_proxy_fcgi`, add the following entries into Apache configuration file:

	ProxyPass /myapp/ unix:///tmp/fastcgi3-example.sock|fcgi://localhost/
 
To run examples via tcp socket, add the following entries into Apache configuration file:

	ProxyPass /myapp/ fcgi://localhost:8080/

If you want to run examples in clustered environment, enable the Apache module `mod_proxy_balancer` and add the following entries into Apache configuration:

	ProxyPass /myapp/ balancer://myappcluster/ stickysession=JSESSIONID|jsessionid
	<Proxy balancer://myappcluster/>
    	BalancerMember fcgi://localhost:8080
    	BalancerMember fcgi://localhost:8081
	</Proxy>

Note that you will need to configure two or more instances of Fastcgi Container either on different hosts or on the same host with different ports.

For more information, see Apache documentation:
 
* [mod_proxy](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html)
* [mod_proxy_fcgi](http://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html)
* [mod_proxy_balancer](http://httpd.apache.org/docs/2.4/mod/mod_proxy_balancer.html)
 
## Running examples

Start HTTPD server as appropriate (e.g. `sudo /etc/init.d/apache start`).

Start Fastcgi Container with exmple configuration (here the container is started under the current user; in production start it as appropriate):

	cd ~/tmp/fscgi
	fastcgi3-container --config=./fastcgi.conf
 
Open any web browser and type the following address in URL bar:

	http://127.0.0.1/myapp/servlet 

or 
	
	http://127.0.0.1/myapp/myapp/test?a1=22

 
	