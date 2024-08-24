curl <website> (can add -v or -vvv) 

-I  capital i shows only the header 

-I lowercase I shows header and response 

$ curl -I <WEBSITE> 

cURL 

|   |   |
|---|---|
|Command|Description|
|curl -h|cURL help menu|
|curl inlanefreight.com|Basic GET request|
|curl -s -O inlanefreight.com/index.html|Download file|
|curl -k [https://inlanefreight.com](https://inlanefreight.com)|Skip HTTPS (SSL) certificate validation|
|curl inlanefreight.com -v|Print full HTTP request/response details|
|curl -I [https://www.inlanefreight.com](https://www.inlanefreight.com)|Send HEAD request (only prints response headers)|
|curl -i [https://www.inlanefreight.com](https://www.inlanefreight.com)|Print response headers and response body|
|curl [https://www.inlanefreight.com](https://www.inlanefreight.com) -A 'Mozilla/5.0'|Set User-Agent header|
|curl -u admin:admin [http://<SERVER_IP>:<PORT>/](http://<SERVER_IP>:<PORT>/)|Set HTTP basic authorization credentials|
|curl [http://admin:admin@<SERVER_IP>:<PORT>/](http://admin:admin@<SERVER_IP>:<PORT>/)|Pass HTTP basic authorization credentials in the URL|
|curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' [http://<SERVER_IP>:<PORT>/](http://<SERVER_IP>:<PORT>/)|Set request header|
|curl '[http://<SERVER_IP>:<PORT>/search.php?search=le](http://<SERVER_IP>:<PORT>/search.php?search=le)'|Pass GET parameters|
|curl -X POST -d 'username=admin&password=admin' [http://<SERVER_IP>:<PORT>/](http://<SERVER_IP>:<PORT>/)|Send POST request with POST data|
|curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' [http://<SERVER_IP>:<PORT>/](http://<SERVER_IP>:<PORT>/)|Set request cookies|
|curl -X POST -d '{"search":"london"}' -H 'Content-Type: application/json' [http://<SERVER_IP>:<PORT>/search.php](http://<SERVER_IP>:<PORT>/search.php)|Send POST request with JSON data|

APIs 

|   |   |
|---|---|
|Command|Description|
|curl [http://<SERVER_IP>:<PORT>/api.php/city/london](http://<SERVER_IP>:<PORT>/api.php/city/london)|Read entry|
|curl -s [http://<SERVER_IP>:<PORT>/api.php/city/](http://<SERVER_IP>:<PORT>/api.php/city/) \| jq|Read all entries|
|curl -X POST [http://<SERVER_IP>:<PORT>/api.php/city/](http://<SERVER_IP>:<PORT>/api.php/city/) -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'|Create (add) entry|
|curl -X PUT [http://<SERVER_IP>:<PORT>/api.php/city/london](http://<SERVER_IP>:<PORT>/api.php/city/london) -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'|Update (modify) entry|
|curl -X DELETE [http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City](http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City)|Delete entry|

From <[https://academy.hackthebox.com/module/35/section/247](https://academy.hackthebox.com/module/35/section/247)>  

$ curl -X POST -d '{"search":"Denver"}' -b 'PHPSESSID=r4nuurljr9acq4s8ra2uithbkb' -H 'Content-Type: application/json' [http://10.10.10.10:8000/search.php]

|   |   |   |
|---|---|---|
|Operation|HTTP Method|Description|
|Create|POST|Adds the specified data to the database table|
|Read|GET|Reads the specified entity from the database table|
|Update|PUT|Updates the data of the specified database table|
|Delete|DELETE|Removes the specified row from the database table|

From <[https://academy.hackthebox.com/module/35/section/227](https://academy.hackthebox.com/module/35/section/227)>  

-s silences any fluff outside of JSON query 

| jq     outputs in JSON format 

$curl-s [http://<SERVER_IP>:<PORT>/api.php/city/le](http://<SERVER_IP>:<PORT>/api.php/city/le) | jq