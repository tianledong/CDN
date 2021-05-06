Team members: Siyuan Chen, Tianle Dong

Our high level approach is that we first designed the structures of the DNS server and the HTTP server. We divided these
two servers into several components and assigned them with corresponding features. Then we listed the potential problems
and prepared several backup plans for those problems. Besides, we designed several optimization plans so that we could
apply them into our servers once the basic functions work. We also performed some stress tests to evaluate the performance
of our servers.

To enhance our servers' performance, we used several different techniques. First, we use a LRU structure as the cache
to store files that have already been downloaded once. Since the storage space on each EC2 server is limited to 10MB, we
remove the earliest files if the storage space is going to break the 10MB limit. What's more, we use a free IP Geolocation
api to get the distance between the client IP and each EC2 hosts' IPs so that we can return the suitable EC2 server with
the shortest geometric distance. Also, we use a cache to store the IPs that have sent queries to our DNS server, and next
time the same IPs send queries to the DNS server we can directly send back the best servers to them.

The biggest challenge is that our DNS server got timeout frequently at the first place. That's because we implemented
the response packet in a wrong way. Besides, we chose an IP geolocation api that returns inaccurate coordinates so that
we couldn't return the closest server to the client. We also struggled designing tests for our servers to ensure that
the servers can handle large amount of requests. If we had enough time, we would implement a multi-threaded http server
to deal with requests that arrives simultaneously. We would try to use active measurement, like scamper, to find the best
EC2 server as well if time allowed.

Tianle implemented the cache structure and the DNS server's find-best-host parts, and Siyuan implemented the deploy/run/stop
CDN scripts and the structure of servers.
