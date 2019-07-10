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
 
 2. db.collection.findOneAndUpdate();
 systax: db.colection.findOneAndUpdate(filter, update, options);
 Updates a single document based on the filter and sort criteria.
 
 The findOneAndUpdate() method has the following form: 
 db.collection.findOneAndUpdate(
   <filter>,
   <update>,
   {
     projection: <document>,
     sort: <document>,
     maxTimeMS: <number>,
     upsert: <boolean>,
     returnNewDocument: <boolean>,
     collation: <document>,
     arrayFilters: [ <filterdocument1>, ... ]
   }
)

Parameters:
- filter: document - The selection criteria for the update. The same query select find() method are available.Specify an empty document {} to update the first document the collection.
- update: document - the update docment. Must contain only update operation.
- projection: document - Optional. A subset of fields to return. to return all fields in the returned document, omit this parameter.
- sort: document - Optional. Specifies a sorting order for the documents matching filter.
- upsert: boolean - Optional. When true, findOneAndUpdate() either: 
   + Creates a new document if no documents match the filter. Returns null after inserting the new document, unless returnNewDocument is true.
   + Update a single document that matches the filter.
  To avoid multiple upserts, ensure that the filter fields are uniquely indexed.
   Defaults to false.
 - returnNewDocment: boolean - Optional. when true, returns the updated document instead of the original document.Default to false.
 - collation: document - Optional, Specifies the collation to use for the operation. Collation allows users to specify language-specific rules for string comparison, such as rules for lettercase and accent marks.
 - arrayFilters: array - Optional. An array of filter documents that determindes which array elements to modify for an update operation on an array field.
   
Example:
### Update A document. 
```python
The grades collection contains documents similar to the following: 
{ _id: 6305, name : "A. MacDyver", "assignment" : 5, "points" : 24 },
{ _id: 6308, name : "B. Batlock", "assignment" : 3, "points" : 22 },
{ _id: 6312, name : "M. Tagnum", "assignment" : 5, "points" : 30 },
{ _id: 6319, name : "R. Stiles", "assignment" : 2, "points" : 12 },
{ _id: 6322, name : "A. MacDyver", "assignment" : 2, "points" : 14 },
{ _id: 6234, name : "R. Stiles", "assignment" : 1, "points" : 10 }
```
The following operation finds the first document where name: R.stiles and increaments the score by 5;

```python
db.scores.findOneAndUpdate(
   { "name" : "R. Stiles" },
   { $inc: { "points" : 5 } }
)
```
The operation returns the original document before the update: 
```python
{ _id: 6319, name: "R. Stiles", "assignment" : 2, "points" : 12 }
```
### Sort And Update A Document
the grads collection contains documents similar to the following: 
```python
{ _id: 6305, name : "A. MacDyver", "assignment" : 5, "points" : 24 },
{ _id: 6308, name : "B. Batlock", "assignment" : 3, "points" : 22 },
{ _id: 6312, name : "M. Tagnum", "assignment" : 5, "points" : 30 },
{ _id: 6319, name : "R. Stiles", "assignment" : 2, "points" : 12 },
{ _id: 6322, name : "A. MacDyver", "assignment" : 2, "points" : 14 },
{ _id: 6234, name : "R. Stiles", "assignment" : 1, "points" : 10 }
```
The following operation updates a document where name : "A.Macdyver". The operation sorts the matching documents by points ascending to update the matching docment with the least points.

```python
db.scores.findOneAndUpdate({
 "name": "A. MacDuver"},
 {$inc: {"point" : 5}},
 {sort: {"point": 1}}
})
```
The operation returns the orginal document before the update
```python
{ _id: 6322, name: "A. MacDyver", "assignment" : 2, "points" : 14 }
```
### 3. db.collection.insertOne()
systax: db.collection.insertOne(doc, options, callback) => {Promise}
Inserts a single document into mongoDB. if documents passed in do not contain the _id_ field, one will be added to each of the documents missing by the driver, mutating the document. This behavior can be overriden by setting the forceServerObjectId flag.

Parameters:
- doc: object - Document to insert.
- option: object - Default is null, Optional settings. 
- callback: collection~insertOnewriteOpCallback - Optional. the command result callback.

### 4.db.collection.findOneAndDelete()
systax: findOneAndDelete(filter, options, callback); -> {Promise}
Find a document and delete it in one otomic operation, requires a write lock for the duratior of the operation.

Parameters: 
- filter: object - Document selection filter.
- options: object - Default is null, Optional settings.
- callback: - optional - the collection result callback.

```python
var MongoClient = require('mongodb').MongoClient,
  test = require('assert');
MongoClient.connect('mongodb://localhost:27017/test', function(err, db) {
  // Get the collection
  var col = db.collection('find_one_and_delete');
  col.insertMany([{a:1, b:1}], {w:1}, function(err, r) {
    test.equal(null, err);
    test.equal(1, r.result.n);

    col.findOneAndDelete({a:1}
      , { projection: {b:1}, sort: {a:1} }
      , function(err, r) {
        test.equal(null, err);
        test.equal(1, r.lastErrorObject.n);
        test.equal(1, r.value.b);

        db.close();
    });
  });
});
