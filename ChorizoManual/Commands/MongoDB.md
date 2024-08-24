Install instructions

$ curl -O [https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.4.7.tgz](https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.4.7.tgz)

$ tar xvf mongodb-linux-x86_64-3.4.7.tgz

To use:
navigate to where binary is present

$ cd mongodb-linux-x86_64-3.4.7/bin

$ ./mongo mongodb://<target IP>:27017

List dabases

$ show dbs;

~select database

$ use <db_name>;

~listing out collections in database

$ show collections

~dump contents of the document, adding pretty for output formatting

$db.<collectionname>.find().pretty();