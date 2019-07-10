# Mongodb-tutorial and Express-tutorial
Tutorial mongodb - documents.

# I. Connection methods.
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
# II. Response methods.
1. res.download(): Prompt a file to be downloaded.
2. res.end(): End the responese process.
3. res.json(): Send a JSON response.
4. res.jsonp(): Send a JSON response with JSONP support
5. res.redirect(): Redirect a request.
6. res.render(): Render a view template
7. res.send(): Send a response of various types.
8. res.sendFile(): Send a file as an octet stream.
9. res.sendStatus(): Set the response state code and send its string representation as the response body.

# III. Collection Methods
1. db.collection.find();
systax: db.collection.find(query, projection);
Description: Selects documents in a collection or view and returns a cursor to the selected

Parameters: 
- query: document - Optional. Specifies selection filter using query operations. To return all document in a collection, omit this parameter or pass an empty document ({});
- projection document: document - Optional. Specifies the fields to return in the documents that match the query filter. To return all fields in the matching documents, omit this parameter.

Behavior: 
- Projection: example
{field1: <value>, field2: <value2>, ...}
 
Cursor Handling
Executing db.collection.find() in the mongo shell automatically iterates the cursor to display up to the first 20 documents
 


