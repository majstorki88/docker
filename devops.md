# DevOps Technical Task

**Goal**: Load-balance requests to simple web servers counting user visits.

## Task

Create a simple, `Docker` based web-application which counts user visits and can be scaled horizontally. 
There should be `n` web-server instances (where `n` can be static) behind a load-balancer, which handles and forwards requests to `web` servers.

- Web server should handle HTTP `GET` requests to `/`.
- For each GET request to `/`, increment `visits` counter.
- Response should return `cumulative` number of `visits` (total across all instances) and `hostname` of the container application server is running on.

For example:

Given a `curl` request like:

```bash
curl http://localhost:80
```

Your web server should return response similar to:

```
I've been visited 41 times, and my hostname is df95bd5e3f71
```

With number of visits incrementing each time request is made. If there were 3 instances of web servers running, the requests would look like this:

```bash 
$ curl http://localhost:80
I've been visited 42 times, and my hostname is 9c4450275c0a

$ curl http://localhost:80
I've been visited 43 times, and my hostname is f042de9946c8

$ curl http://localhost:80
I've been visited 44 times, and my hostname is df95bd5e3f71

$ curl http://localhost:80
I've been visited 45 times, and my hostname is 9c4450275c0a
      
# and so on...
```

If you have a request log, it should look something like this:

```
web_1    | 172.22.0.4 - - [18/Jul/2017 15:00:21] "GET / HTTP/1.1" 200 -
web_2    | 172.22.0.4 - - [18/Jul/2017 15:00:49] "GET / HTTP/1.1" 200 -
web_3    | 172.22.0.4 - - [18/Jul/2017 15:01:05] "GET / HTTP/1.1" 200 -
web_1    | 172.22.0.4 - - [18/Jul/2017 15:02:54] "GET / HTTP/1.1" 200 -
web_2    | 172.22.0.4 - - [18/Jul/2017 15:04:19] "GET / HTTP/1.1" 200 -
```
 
Finally, your setup should be similar to this:

```
                             client
                                +
                                |
                                |
                       +--------v--------+
                       |                 |
                       |  load balancer  |
                       |                 |
                       +--------+--------+
                                |
                                |
        +------------------------------------------------+
        |                       |                        |
        |                       |                        |
+-------v--------+     +--------v--------+     +---------v-------+
|                |     |                 |     |                 |
|     web-1      |     |      web-2      |     |      web-3      |
|                |     |                 |     |                 |
+----------------+     +-----------------+     +-----------------+
```
 
### Notes

- We only ask that you use `Docker` and that your `web` application server is running as a container, but rest of the setup is entirely up to you.
- Choice of web servers and load-balancers is also up to you.
- You don't have to complete this test 100%, and please ask for help or clarification if you're stuck - ad@allthingstalk.com, dv@allthingstalk.com