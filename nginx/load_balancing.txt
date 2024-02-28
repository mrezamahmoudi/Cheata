HTTP Load Balancing

Problem
You need to distribute load between two or more HTTP servers.

Solution
Use NGINX’s HTTP module to load balance over HTTP servers using the upstream
block:

upstream backend {
	server 10.10.12.45:80 weight=1;
	server app.example.com:80 weight=2;
	server spare.example.com:80 backup;
}
server {
	location / {
		proxy_pass http://backend;
	}
}

This configuration balances load across two HTTP servers on port 80, and defines
one as a backup, which is used when the primary two are unavailable. The weight
parameter instructs NGINX to pass twice as many requests to the second server, and
the weight parameter defaults to 1.
--------------------
Discussion
The HTTP upstream module controls the load balancing for HTTP. This module
defines a pool of destinations—any combination of Unix sockets, IP addresses, and
DNS (Domain Name Service) records, or a mix. The upstream module also defines
how any individual request is assigned to any of the upstream servers.
Each upstream destination is defined in the upstream pool by the server directive.
The server directive is provided a Unix socket, IP address, or a fully qualified domain
name (FQDN), along with a number of optional parameters. The optional parameters
give more control over the routing of requests. These parameters include the weight
of the server in the balancing algorithm; whether the server is in standby mode,
available, or unavailable; and how to determine if the server is unavailable. NGINX
Plus provides a number of other convenient parameters, like connection limits to
the server, advanced DNS resolution control, and the ability to slowly ramp up
connections to a server after it starts.

=============================================================================================================================
Passive Health Checks

Problem
You need to passively check the health of upstream servers.

Solution
Use NGINX health checks with load balancing to ensure that only healthy upstream

servers are utilized:

upstream backend {
	server backend1.example.com:1234 max_fails=3 fail_timeout=3s;
	server backend2.example.com:1234 max_fails=3 fail_timeout=3s;
}

This configuration passively monitors upstream health by monitoring the response
of client requests directed to the upstream server. The example sets the max_fails
directive to three, and fail_timeout to 3 seconds. These directive parameters work
the same way in both stream and HTTP servers.
--------------------
Discussion
Passive health checking is available in the open source version of NGINX, and is
configured by using the same server parameters for HTTP, TCP, and UDP load
balancing. Passive monitoring watches for failed or timed-out connections as they
pass through NGINX as requested by a client. Passive health checks are enabled by
default; the parameters mentioned here allow you to tweak their behavior. The default
max_fails value is 1, and the default fail_timeout value is 10s. Monitoring for
health is important on all types of load balancing, not only from a user-experience
standpoint, but also for business continuity. NGINX passively monitors upstream
HTTP, TCP, and UDP servers to ensure that they’re healthy and performing.
Also See
HTTP Health Checks Admin Guide
TCP Health Checks Admin Guide
UDP Health Checks Admin Guide

=============================================================================================================================
TCP Load Balancing

Problem
You need to distribute load between two or more TCP servers.

Solution
Use NGINX’s stream module to load balance over TCP servers using the upstream block:

stream {
	upstream mysql_read {
		server read1.example.com:3306 weight=5;
		server read2.example.com:3306;
		server 10.10.12.34:3306 backup;
	}
	server {
		listen 3306;
		proxy_pass mysql_read;
	}
}

The server block in this example instructs NGINX to listen on TCP port 3306 and
balance load between two MySQL database read replicas, and lists another server as a
backup that will be passed traffic if the primaries are down.
This configuration is not to be added to the conf.d folder, as that folder is included
within an http block; instead, you should create another folder named stream.conf.d,

open the stream block in the nginx.conf file, and include the new folder for stream
configurations. An example follows.

In the /etc/nginx/nginx.conf configuration file:

user nginx;
worker_processes auto;
pid /run/nginx.pid;

stream {
	include /etc/nginx/stream.conf.d/*.conf;
}

A file named /etc/nginx/stream.conf.d/mysql_reads.conf may include the following

configuration:
upstream mysql_read {
	server read1.example.com:3306 weight=5;
	server read2.example.com:3306;
	server 10.10.12.34:3306 backup;
}
server {
	listen 3306;
	proxy_pass mysql_read;
}
--------------------
Discussion
The main difference between the http and stream context is that they operate at
different layers of the OSI model. The http context operates at the application layer,
7, and stream operates at the transport layer, 4. This does not mean that the stream
context cannot become application-aware with some clever scripting, but that the
http context is specifically designed to fully understand the HTTP protocol, and the
stream context, by default, simply routes and load balances packets.
TCP load balancing is defined by the NGINX stream module. The stream module,
like the HTTP module, allows you to define upstream pools of servers and configure
a listening server. When configuring a server to listen on a given port, you must
define the port it will listen on, or optionally, an address and a port. From there,
a destination must be configured, whether it be a direct reverse proxy to another
address or an upstream pool of resources.
A number of options that alter the properties of the reverse proxy of the TCP
connection are available for configuration. Some of these include SSL/TLS validation
limitations, timeouts, and keepalives. Some of the values of these proxy options can
be (or contain) variables, such as the download rate and the name used to verify an
SSL/TLS certificate.
The upstream for TCP load balancing is much like the upstream for HTTP, in that it
defines upstream resources as servers, configured with Unix socket, IP, or FQDN, as
well as server weight, maximum number of connections, DNS resolvers, connection
ramp-up periods, and if the server is active, down, or in backup mode.
NGINX Plus offers even more features for TCP load balancing. These advanced
features can be found throughout this book. Health checks for all load balancing will
be covered later in this chapter.

=============================================================================================================================
UDP Load Balancing

Problem
You need to distribute load between two or more UDP servers.

Solution
Use NGINX’s stream module to load balance over UDP servers using the upstream
block defined as udp:

stream {
	upstream ntp {
		server ntp1.example.com:123 weight=2;
		server ntp2.example.com:123;
	}
	server {
		listen 123 udp;
		proxy_pass ntp;
	}
}
This section of configuration balances load between two upstream network time
protocol (NTP) servers using the UDP protocol. Specifying UDP load balancing is as
simple as using the udp parameter on the listen directive.
If the service over which you’re load balancing requires multiple packets to be sent
back and forth between client and server, you can specify the reuseport parameter.
Examples of these types of services are OpenVPN, Voice over Internet Protocol
(VoIP), virtual desktop solutions, and Datagram Transport Layer Security (DTLS).
The following is an example of using NGINX to handle OpenVPN connections and

proxy them to the OpenVPN service running locally:

stream {
	server {
		listen 1195 udp reuseport;
		proxy_pass 127.0.0.1:1194;

	}
}



--------------------
Discussion
You might ask, “Why do I need a load balancer when I can have multiple hosts in
a DNS A or service record (SRV record)?” The answer is that not only are there
alternative balancing algorithms with which we can balance, but we can load balance
over the DNS servers themselves. UDP services make up a lot of the services that we
depend on in networked systems, such as DNS, NTP, QUIC, HTTP/3, and VoIP. UDP
load balancing might be less common to some, but it’s just as useful in the world of
scale.
You can find UDP load balancing in the stream module, just like TCP, and configure
it mostly in the same way. The main difference is that the listen directive specifies
that the open socket is for working with datagrams. When working with datagrams,
there are some other directives that might apply where they would not in TCP, such
as the proxy_response directive, which specifies to NGINX how many expected
responses can be sent from the upstream server. By default, this is unlimited until the
proxy_timeout limit is reached. The proxy_timeout directive sets the time between
two successive read-or-write operations on client or proxied server connections
before the connection is closed.
The reuseport parameter instructs NGINX to create an individual listening socket
for each worker process. This allows the kernel to distribute incoming connections
between worker processes to handle multiple packets being sent between client and
server. The reuseport feature works only on Linux kernels 3.9 and higher, DragonFly
BSD, and FreeBSD 12 and higher.
