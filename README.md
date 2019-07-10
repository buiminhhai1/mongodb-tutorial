# mongodb-tutorial
Tutorial mongodb - documents.

I. Connection methods.
 1. connect();
 systax: connect(url, user, password);
 (Mục đích: tạo ra một kết nối đến một thể hiển của MONGODB và trả về liên kết tới database.)
 Creates a connection to a MongoDB instance and returns the reference to the database.
 Can instead by Mongo() objects and getDB() mothod.
 
 Detail for parameter
 url: String - Specifies the connection string. 
      systax: <hostname>:<port>/<database>,
              <hostname>/<database>
              <database>
user: String - Optional. Specifies an existing username with access privileges for this database. If user is specified, you must include the password parameter as well.

password: String - Optional unless the user parameter is specifies.               

Example:
db = connect("localhost:27017/myDatabase");

2. Mongo()
Creates a new connection object. 

systax: Mongo(host)

Description: JavaScript constructor to instantiate a database connection from the mongo shell or from a JavaScript file.

Parameter: 
host: String - Optional. The host, either in the form of <host> or <host>:<port>.
  
Instantiation Options
- Use the contructor without a parameter to instantiate a connection to the localhost interface on the default port; 27017
- Pass the <host> parameter to the constructor to instantiate a connection to the <host> and the default port.
- Pass the <host>:<port> parameter to the constructor to instantiate a connection to the host and the <port>.

3. Mongo.getDB();
Returns a database object.

systax: Mongo().getDB(<database>);
  
Description:
Provides access to database objects from the mongo shell or from a JavaScript file.

Parameter: 
database: String - The name of the database to access.

Example: 
The following example instantiates a new connection to the MongoDB instance running on the localhost interface and returns a references to "myDatabase"

db = new Mongo().getDB("myDatabase");
