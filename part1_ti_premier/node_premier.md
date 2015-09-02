简单说，Node是服务器端(server-side)的Javascript，使用C++开发。

Node基于Google的V8引擎，使用时间驱动(event-driven), 非阻塞性I/O(non-blocking I/O)模型。
因为Node的跟底层的 Unix的API(low-level Unix API)做了绑定(binding)，这些API包括对底层的进程(process)，文件，网络，socket，HTTP的操作。

所以，Node使得原先开发浏览器应用个程序员，可以很快的上手服务器端开发。

另外，还有一个基于Java(Java-based)的Javascript解释器，Rhino，可以获得所有Java API的能力。
有兴趣的同学，可以研究一下。
