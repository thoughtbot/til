
HTTP allows the communication between two applications over a network. Usually
one application is a web browser and another is a web server. A message sent
from a browser has to travel down a series of network layers to make its way
*to* the web server, before a response is ever sent *from* the web server. 

The transport layer protocol is the layer below HTTP. Majority of HTTP traffic
travels over **TCP (Transmission Control Protocol)**. When a URL is entered in the
browser, the browser extracts the host name and opens a TCP socket by specifying
the server address derived from the host name.

Once a socket is open, the application can begin writing data into the socket.
The browser only worries about how to properly format the HTTP request message
into the socket. The TCP layer accepts the data and then guarantees the delivery
of the message to the other server. "Guarantees" because TCP will automatically
resend any information that might get lost in transit. TCP is responsible
for flow control, error detection, and overall reliability. 

After the TCP layer, comes the **IP (Internet Protocol) layer**. There are many
components that the HTTP message has to go through to finally make its way to
the server. IP is responsible for moving the HTTP message through the various
gateways, routers, switches, and other devices throughout the world that move
information from one network to another. IP does not guarantee deliver because
that is the responsibility of TCP.

Every device must have an IP address in order for it to work. It looks like
this: 108.192.43.21. IP also breaks the HTTP data into packets that travel over
the network. These IP packets travel over a network. This is the responsibility
of the **data link layer**.

A common choice for the data link layer is Ethernet. The Ethernet is focused on
1's, 0's, and electromagnetic signals. Eventually the signal reaches the other
machine through the network card, and the process is revered: data link layer
delivers packets to IP, IP hands over data to TCP, TCP reassembles the data into
the original HTTP message and hands it off to the server (something like
Apache). 

HTTP over TCP/IP is a wonderful piece of engineering.


