CAPTURE FILTERS: 

|   |   |
|---|---|
|Usage (Filter by)|Syntax|
|IP|ip.add == 0.0.0.0|
|Destination IP|ip.dest == 10.0.0.0|
|Source IP|ip.src == 0.0.0.0|
|IP range|ip.addr >= 0.0.0.0 and ip.addr <= 0.0.0.10|
|Multiple Ips|ip.addr == 0.0.0.0 and ip.addr == 0.0.0.1|
|Filter out IP address|!(ip.addr == 0.0.0.0)|
|port|tcp.port == 22|
|destination port|tcp.dstport == 23|
|IP address and port|ip.addr == 0.0.0.0 and tcp.port ==22|
|URL|http.host == "host name"|
|time stamp|frame.time >= "September 6, 2021 16:25:00"|
|flags (syn/ack)|tcp.flag.syn==1 or 0 for non|

DISPLAY FILTERS: 

|   |   |   |
|---|---|---|
|Description|Operator|Syntax|
|Equal|eq or ==|ip.dest == 0.0.0.0|
|Not Equal|ne or !=|ip.dest != 0.0.0.0|
|Greater Than|gt or >|frame.len > 10|
|Less than|lt or <|frame.len < 10|
|Greater than or Equal|ge or >=|frame.len >= 10|
|Less than or Equal|le or <=|frame.len <= 10|