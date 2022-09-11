
<h3>Mongo DB</h3>

First Part
<a href="https://medium.com/@taylan.ulun/introduction-to-mongodb-for-anyone-part-1-e5180f4065e8"> <img src="https://img.shields.io/badge/Medium-12100E?style=for-the-badge&logo=medium&logoColor=white" /> </a>&nbsp;&nbsp; 

Second Part
<a href="https://medium.com/@taylan.ulun/introduction-to-mongodb-for-anyone-part-2-44c48c8985ce"> <img src="https://img.shields.io/badge/Medium-12100E?style=for-the-badge&logo=medium&logoColor=white" /> </a>&nbsp;&nbsp; 



**Chapter 1**

  

1.  What is MongoDB? —> **NoSQL Document Database**

  

**Database**: Structured way to store and access data.

**A NoSQL Database:** Related tables of data. This means you are storing data in an organized way, but not in rows and columns.

MongoDB is a NoSQL document database. This means data in MongoDB is stored as **documents**.

This documents in turn stored in what we call **collections** of documents.

That's why MongoDB is categorized as a NoSQL document database.

  

2. What is document?

  

A way to organize and store the data as a set of field-value pairs.

{

	<field> : <value>
	<field> : <value>

	“name” : “Taylan”
	“title” : “Engineer”
}

Field = Unique identifier, and value is data related to a given identifier.

Collection would contain many documents similar to above one. And database would contain multiple collections.

  

3. What is Atlas? —> **Database As A Service**

  

The Atlas cloud database is full managed database built for a wide range applications with MongoDB at its core.


  

Atlas users can deploy clusters, which are groups of servers that store your data.

**These servers are configured in what they’ve call a replica set, which is a set of a few MongoDB instances that store the same data.**

**Instance**: a single machine locally or in the cloud, running a certain software. In this case it is the MongoDB database being run in the cloud.

This setup ensures that if something happens to one of the machines in the replica set, the data will remain intact and available for use by the application by the remaining working members of the replica set.

So every time that you make changes in the a document or  a collection, redundant copies of that data are stored within the replica set.

  

-   Atlas free tier cluster 3-server replica set 512 MB storage. Never expires.

  

Connect database with Mongo Shell:

-   mongo "mongodb+srv://first-mongodb-cluster.XXXX.mongodb.net/sampleDatabase” --username XXXX

  

**Chapter 2**

  

1.  How does MongoDB store data?

  

When you view or update documents in MongoDB shell, you are working in JSON. JSON is text-based format, and text parsing is very slow. (Space-consuming) JSON readable format is far from space efficient, and that was another database concern. And JSON only supports a limited number of basic data types.
  
MongoDB use BSON (Binary JSON).

**BSON**

  

-   Bridges the gap between binary representation and JSON format. 
-   Optimized for: Speed, Space and Flexibility.
-   The goal was to achieve high-performance and general-purpose focus.
-   Since its initial formulation,BSON has been extended to add some optional non-JSON native data types like dates and binary data.

| **JSON** | **BSON** |
|--|--|
| **Encoding** | **Encoding** |
| UTF-8 String| Binary |
| **Data Support**| **Data Support** |
| String,Boolean,Number,Array | **Encoding** |
| **Encoding** | String,Boolean,Number(Integer, Float, Long),Array,Date,Raw Binary |
| **Readability** | **Readability** |
| Human and Machines | Machines Only |


<!-- +--------------------+-----------------------------+
|   JSON             |       BSON                  |
+--------------------+-----------------------------+
| Encoding           | Encoding                    |
+--------------------+-----------------------------+
| UTF-8 String       | Binary                      |
+--------------------+-----------------------------+
| String,Boolean,    | Array,Date,Raw Binary       |
| Number,Array       | String,Boolean,             |
|                    | Number(Integer, Float, Long)|
+--------------------+-----------------------------+
| Readability        | Readability                 |
+--------------------+-----------------------------+
| Human and Machines | Machines Only               |
+--------------------+-----------------------------+ -->


MongoDB stores the data in BSON, internally and over the network.

But that doesn't mean you can't think of MongoDB as a JSON database. 

Anything you can represent in JSON can be natively stored in MongoDB and retrieved just as easily n JSON.

-   **BSON provides additional features, speed, and flexibility.**

  

2. Importing and Exporting Data

  

As we learned data in MongoDB is stored in BSON but is viewed in JSON. BSON is great way to store data but isn’t really human readable.

If you are looking to just store the data, and transfer it to a different system or cluster best way would be to export in BSON. (It is lighter and faster.)

However reading that data after I export it, human-readable JSON is better choice.

  
| **JSON** | **BSON** |
|--|--|
| mongoimport | mongorestore |
| mongoexport | mongodump |


**EXPORT**

Once the choice of format is made, we can proceed to export the data.

  
-   **mongodump —uri “<Atlas Cluster URI>”  —> Export data in BSON.**
-   **mongoexport —uri “<Atlas Cluster URI>”  —> Export data in JSON.**

							--collection=<collection_name>

							--out=<filename.json>

 

Uniform Resource Identifier ( URI String)

  

srv —> establish a secure connection between your application and a MongoDB instance.

  

**mongo+srv://user:password@clusterURI.mongodb.net/database** **—>** You can use the URI connection string in this format, when connecting your Atlas Cluster.

**IMPORT**

  

-   **mongorestore —uri “<Atlas Cluster URI>”  —> Imports data in BSON.**

									--drop dump

-   **mongoimport —uri “<Atlas Cluster URI>”  —> Imports data in JSON.**

									--drop=<filename.json>
									--collection <collection_name>


**mongodump --uri "mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies"**

  

**mongoexport --uri="mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --collection=sales --out=sales.json**

  

**mongorestore --uri "mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies"  --drop dump**

  

**mongoimport --uri="mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --drop sales.json**

  

  

3. Data Explorer

  

A **namespace** is the concatenation of a collection name and database name.

  

-   Example: sample_training.companies —> This is the namespace for the company’s collection. Which is part of the sample_training database. If you select that, then the selected namespace will appear above the collection preview.

By default data explorer gives us a data preview in the Find tab.

Collection size, Total documents, Indexes total size are all listed at the top of the Data Explorer.

  

-   Example: I want to see all the documents where the state is New York.

```bash
	{“state”:”NY”}
```
-   Example: I want to see all the documents where the state is New York and city Albany
```bash
	{“state”:”NY”, “city”:”ALBANY”}
```
  

4. FIND Command

  

**admin** database does a number of administrative things, one of which keeping track of existing users that have access to the database.

Also **local** database takes care administrative stuff.

  

**show dbs** —> shows the list of databases that are in the cluster.

  

-   **use sample_training** command switch to db.
-   **show collections** command  —> list collections in particular db.
-   db.zips.**find**({“state”:”NY”}) —> find command in the zips collection with query. We don’t specify the database name since we navigated to the database earlier. And now db objects pointing sample_training database.
-   **it —>** iterates through a **cursor**. A **pointer** to a result set of a query. A direct access of the memory location.

  

-   Example: How many zip codes in NY?

**db.zips.find({"state": "NY"}).count()**

-   Example: Atlas atlas-10b5bi-shard-0 [primary] sample_training> 
	- db.zips.find({"state": "NY", "city": "ALBANY"}).count() —> 7
-   db.zips.find({"state": "NY", "city": "ALBANY"}).**pretty()** —> More readable data.

  

  

**Chapter 3**

  

1.  Inserting New Documents - ObjectId

  

Every document must have a **unique** _id value.

  

Every MongoDB document has one thing in common. And that is that every document must have an underscore id field. Every underscore id field in a collection must have a unique value from the rest of the documents in the collection.

The rest of the fields and values are not enforced by default in any way.

In theory, you can have a collection where all the documents have same exact field value pairs in each document with the only difference between them being the underscore id field.

  

When we insert a new document, MongoDB populates the underscore id field with a value that is type **ObjectId**.

The underscore id doesn’t have to have the type ObjectId. It is just what it is created by default ensure unique values for each document.

  

2. Inserting Documents and the Errors

  

When we insert a lot of documents at a time, like insert a collection to a database that already contains the same documents, we get a lot of the same error.

**Error** : Duplicate key error followed by a namespace for the collection and the id value of a document that we attempted to insert. The insertion didn’t succeed because a document this exact id value already exists.

-   This is why we need to add the drop option. This way we remove the whole collection before inserting it back, thus eliminating the duplicate key issue.

  

db.inspections.**findOne()**; —> Get a random document from the collection. This function is good to have when you are looking for some document that matches a certain query,  or the general idea about the shape of documents in a collection.

  

This is a rare case, because most of the time, when a collection is queried, the goal is the get all of the documents that match the query, not just one.

  

When you get just one document, you don't know if this is the only document that matches the query or if there are others.
```bash
db.inspections.insert({

"_id" : ObjectId("56d61033a378eccde8a8354f"),

"id" : "10021-2015-ENFO",

"certificate_number" : 9278806,

"business_name" : "ATLIXCO DELI GROCERY INC.",

"date" : "Feb 20 2015",

"result" : "No Violation Issued",

"sector" : "Cigarette Retail Dealer - 127",

"address" : {

"city" : "RIDGEWOOD",

"zip" : 11385,

"street" : "MENAHAN ST",

"number" : 1712

}

})
```
  
```bash
db.inspections.insert({

"id" : "10021-2015-ENFO",

"certificate_number" : 9278806,

"business_name" : "ATLIXCO DELI GROCERY INC.",

"date" : "Feb 20 2015",

"result" : "No Violation Issued",

"sector" : "Cigarette Retail Dealer - 127",

"address" : {

"city" : "RIDGEWOOD",

"zip" : 11385,

"street" : "MENAHAN ST",

"number" : 1712

}

})

```

```bash
	db.inspections.find({"id" : "10021-2015-ENFO", "certificate_number" : 9278806}).pretty()
```
  

-   When we insert same document into a collection with _id, there will be a write error. Meaning that writing this document to the collection didn’t succeed. This means we cannot insert documents with identical _id values into the collection.
-   What happens if we remove the _id field and try to insert this document again? —>  This will be working, and the response from the database is that the number of inserted documents is one, which is exactly how many documents we try the insert in this example.

  

The two documents look identical, except for the _id value.

  

Inserting multiple documents syntax:

  

-   db.inspections.insert([ { "test": 1 }, { "test": 2 }, { "test": 3 } ])

  

-   db.inspections.insert([{ "_id": 1, "test": 1 },{ "_id": 1, "test": 2 },{ "_id": 3, "test": 3 }])

  

_Find the documents with_ _id: 1

-   db.inspections.find({ "_id": 1 })

  

_Insert multiple documents specifying the_ _id _values, and using the_ "ordered": false _option._

-   db.inspections.insert([{ "_id": 1, "test": 1 },{ "_id": 1, "test": 2 },{ "_id": 3, "test": 3 }],{ "ordered": false })

  

-   **When the default ordered insert happens, the moment there was a duplicate key error, the insert operation halts. And even if the rest of the documents have unique IDs, they won’t get a chance to be inserted, just like test 3 above example.**

  

-   **If insert is unordered, then every document that has a unique _id value gets added to the collection.**

  

_Insert multiple documents with_ _id: 1 _with the default_ "ordered": true _setting_

-   db.inspection.insert([{ "_id": 1, "test": 1 },{ "_id": 3, "test": 3 }]) —> And the result is no right errors and two documents inserted. Because there was a typo the collection name got misspelled. Instead of the plural ‘inspections’, it was a singular ‘inspection’. Why didn’t we get an error, because this behavior by design. MongoDB wants it to be simple for you to create a new collection or a database. So if you insert a document into a collection that doesn’t exist, then this collection will get created for you.

  

_View_ collections _in the active_ db

-   show collections

inspections

_inspection_

  

_Switch the active_ db _to_ training —> **If nothing was inserted, this list doesn’t contain the training database.**

-   use training

-   show dbs

simple_training

  

**Problem:**

Which of the following commands will successfully insert 3 new documents into an empty pets collection?

  

**Answer**

```bash

db.pets.insert([{ "pet": "cat" }, { "pet": "dog" }, { "pet": "fish" }])

```

**_The _id field is not specified in any of these documents, which means that it will be created for each automatically, and it will be unique._**

  

```bash

db.pets.insert([{ "_id": 1, "pet": "cat" },

{ "_id": 1, "pet": "dog" },

{ "_id": 3, "pet": "fish" },

{ "_id": 4, "pet": "snake" }], { "ordered": false })

```

**_This insert is unordered, which means that each document with a unique _id value will get inserted into the collection, which would make a total of 3 inserted documents._**

  

```bash

db.pets.insert([{ "_id": 1, "pet": "cat" },

{ "_id": 2, "pet": "dog" },

{ "_id": 3, "pet": "fish" },

{ "_id": 3, "pet": "snake" })

```

  

**_While there is a duplicate key error between the "fish" and "snake" documents, it occurs at the very end of the insert operation, because this insert is ordered by default. As a result the first 3 documents will get inserted and the last one will create a duplicate key error._**

  

3. Updating Documents

  

MongoDB flexible has a flexible document model, which means that you can store your data however it makes sense for your application. (For example array of objects)

An array of object is a common way to store data in certain applications.

  

## Problem:

- MongoDB has a flexible data model, which means that you can have fields that contain documents, or arrays as their values.

  

## Answer

  

```bash

{ 
	"_id": 1,
	"pet": "cat",
	"attributes": [ { 
						"coat": "fur","type": "soft"
						 },
					{ 
						"defense": "claws",
						"location": "paws",
						"nickname": "murder mittens" 
					} ],
	"name": "Furball" }
```

  

```bash

{ "_id": 1,

"pet": "cat",

"fur": "soft",

"claws": "sharp",

"name": "Furball" }

```

  

```bash

{ "_id": 1,

"pet": "cat",

"attributes": { "coat": "soft fur",

"paws": "cute but deadly" },

"name": "Furball" }

```

  

**None of the above.**

**_All the documents presented in the choices are valid MongoDB documents._**

  

Updating Documents - mongo shell (MQL - MongoDB Query Language)

  

Two operation to update documents in the Mongo shell, **updateOne()** and **updateMany().**

  

As we know of using **findOne(),** which returns the first document that happens to match the given query. This is different from **find()**, which returns a cursor with all the documents that correspond to the given query.

  

-   With **updateOne(),** if there are multiple documents that matches a given criteria, only one of them will be updated, whichever one this operations finds first.
-   Whereas using **updateMany()** will update all documents that match a given query.

  

-   **$inc** is an MQL update operator.

  

```bash
	{“$inc”: {“pop”:10, “<field2>”: <increment value>, … }}
```

  

-   It increments the value of a specified field by the given amount.

-   In this example(below), we’re looking to increment the “pop” field by 10 in every document which lists Hudson as the city. **

  

When the operation is complete, we get a summary of whether it succeeded.

{ “acknowledged” : true, “matchedCount” : 16, “modifiedCount” : 16 } 16 documents matched our query, and 16 were updated.

  

### $inc syntax allows us to update multiple fields at the same time by listing the fields and their increment value separated by a comma.

  

**$inc** is not the only MQL update operator.

**$set** is used, it updates the value of the given field with a specified value. If you were typo in some fields, that means you want to add this field to the document. And so the field gets added.

**$push** is used to add an element to an array field, which has this syntax. Just like $set operator if the field doesn’t exist in the document, then $push add an array field to the document with a specified value.

  

```bash
	{ $push: { <field1>: <value1>, … } }
```


To learn more about all available [update operators in MQL, visit documentation page](https://docs.mongodb.com/manual/reference/operator/update/#id1).

- Connect to your Atlas Cluster.

  

```bash
	mongo "mongodb+srv://<username>:<password>@<cluster>.mongodb.net/admin"
```

- Use the sample_training database as your database in the following commands.


```bash
	use sample_training
```

- Find all documents in the zips collection where the zip field is equal to "12434".

```bash
	db.zips.find({ "zip": "12534" }).pretty()
```

- Find all documents in the zips collection where the city field is equal to "HUDSON".

```bash
	db.zips.find({ "city": "HUDSON" }).pretty()
```

- Find how many documents in the zips collection have the city field equal to "HUDSON".

```bash
	db.zips.find({ "city": "HUDSON" }).count()
```

- Update all documents in the zips collection where the city field is equal to "HUDSON" by adding 10 to the current value of the "pop" field. **

```bash
	db.zips.updateMany({ "city": "HUDSON" }, { "$inc": { "pop": 10 } })
```

- Update a single document in the zips collection where the zip field is equal to "12534" by setting the value of the "pop" field to 17630.

```bash
	db.zips.updateOne({ "zip": "12534" }, { "$set": { "pop": 17630 } })
```

- Update a single document in the zips collection where the zip field is equal to "12534" by setting the value of the "population" field to 17630.

```bash
	db.zips.updateOne({ "zip": "12534" }, { "$set": { "population": 17630 } })
```

- Find all documents in the grades collection where the student_id field is 151 , and the class_id field is 339.

```bash
	db.grades.find({ "student_id": 151, "class_id": 339 }).pretty()
```

- Find all documents in the grades collection where the student_id field is 250 , and the class_id field is 339.

```bash
	db.grades.find({ "student_id": 250, "class_id": 339 }).pretty()
```

- Update one document in the grades collection where the student_id is ``250`` *, and the class_id field is 339 , by adding a document element to the "scores" array.

```bash
	db.grades.updateOne({ "student_id": 250, "class_id": 339 },

{ "$push": { "scores": { "type": "extra credit",
						 "score": 100 }
}
})
```

  

## Problem

- Given a pets collection where each document has the following structure and fields:

  

## Answer

  

```bash
db.pets.updateMany({ "pet": "cat" },
{ "$set": { "type": "dangerous",
			"look": "adorable" }})
```

  

**_Fields "type" and "look" do not exist in the existing documents in the collection, so this command will create new fields with the given values for all documents that have the "pet" field equal to "cat"._**

  

```bash
db.pets.updateMany({ "pet": "cat" },
{ "$push": { "climate": "continental",
			 "look": "adorable" } })
```

  

**_While the "climate" field is already present in the documents in this collection, the field "look" is new, and this command will create a new array field called "look", with one element "adorable" in it._**

  

4. Deleting Documents

  

**deleteOne(),  deleteMany()** work as similar way to updateOne() and updateMany(). Except in this case, the only update that happens is that the document gets removed from the database.

  

**The only times when deleteOne() is a good approach to deleting documents is when we are querying by the _id value, thus guaranteeing that this is the only document matching this query. Otherwise, we are running the risk of deleting one of a few, or even one of many documents that we needed to delete. We can’t consistently rely on findOne(), updateOne(), deleteOne() to always return the same document when multiple fit the search query, unless we are querying by the _id value.**

  

-   db.<collection>.drop() —> deleted the given collection.
-   deleteOne(), deleteMany() deletes documents that match a given query.
-   After these commands is issued the **data is GONE**.

  

**Chapter 4**

  

1.Query Operators - Comparison

  

**Update Operators**

  

**$inc, $set, $unset** operators enabled you to modify data in your database.

Enable us to modify data in the database.

  

**Query Operators**

  

Query operators provide additional ways to locate data within the database.

Provide additional ways to locate data within the database.

What query operators have in common with all kinds of operators is the dollar sign that precedes the operator.

  

**$ has multiple uses**.

  

The dollar sign is used for multiple things in MongoDB, operators, aggregation pipeline stages, and accessing field values.

Precedes MQL operators

Precedes Aggregation pipeline stages

Allow Access to Field Values

  

**$eq** = **EQ**ual

**$ne** = **N**ot **E**qual to

**$gt** > **G**rater **T**han

**$lt** < **L**ess **T**han

**$gte** >= **G**rater **T**han or **E**qual to

**$lte** <= **L**ess **T**han or **E**qual to

  

All use the same syntax of field, colon, and then in curly brackets, operator colon value.

  

Syntax;

  

```bash
	{ <field>: { <operator>: <value> } }

-   { “tripduration”: { “$lte” : 70 } }

-   { “tripduration”:  { “$lte” : 70 }, “usertype”: { “$ne” : “Subscriber” } }
```

  

Query operators provide additional ways to locate data within the database.

  

Comparison operators specifically allow us to find data within a certain range.

  

**Problem 1:**

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

How many documents in the sample_training.zips collection have fewer than 1000 people listed in the pop field?

  

**Answer :**

  

```bash
	db.zips.find({"pop": {"$lt": 1000}}).pretty().count()
```

  

**Problem 2:**

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

What is the difference between the number of people born in 1998 and the number of people born after 1998 in the sample_training.trips collection?

  

**Answer**

  

```bash
db.trips.find({"birth year": {"$gt": 1998}}).count() - db.trips.find({
			   "birth year": {"$eq": 1998}}).count()
```

  

**Problem 3:**

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

Using the sample_training.routes collection find out which of the following statements will return all routes that have at least one stop in them?

  

**Answer**

  

```bash
	db.routes.find({'stops': {'$gte': 1}}).pretty()
	db.routes.find({'stops': {'$ne': 0}}).pretty()
	db.routes.find({'stops': {'$gt': 0}}).pretty()
```

  

2.Query Operators - Logical

  

In MQL, we have the standart set of four logical operators.

  

**$and :** Match **all** of the specified query clauses.

  

**$or : At least one** of the query clauses is matched. **$or** returns the documents as long as at least one of the query clauses is matched.

  

**$nor :** Returns all documents that fail to match both clauses. **Fail to match** both given clauses.

  

**$not : Negates** the query requirements and returns all documents that do not match the query.

  

**$and, $or, $nor** have similar to each other syntax where the operator precedes an array of clauses that it will operate on.

  

```bash
	{ <operator> : [ {statement1}, {statement2}, … ] }
```

  

**$not** simply negates what is in front of it. Thus array syntax is not necessary.

  

```bash
	{ $not : { statement } }
```

  

**$and** is used as the default operator when an operator is not specified.

  

For example, this query actually reads as an $and statement.

  

```bash
	{ sector: “Mobile Food Vendor - 881”, result: “Warning”}
```

  

Is the same as:

  

```bash
	{ “$and”: [ { sector: “Mobile Food Vendor - 881”, result: “Warning”} }
```

  

If you have multiple criteria must be true for your query.

  

Another example of an **implicit $and** can be seen when we apply multiple conditions to the same field.

—> Find which students ids are > 25 and < 100 in the sample_training.grades collection.

  

```bash
	{ “$and”: [ { “student_id”: { “$gt”: 25 } }, { “student_id”: { “$lt”: 100 } } ] }
```

  

But we could also simplify it significantly.

  

```bash
	{ “student_id”: {“$gt”: 25, “$lt”: 100 } }
```

  

Explicit $and

  

When you need to include the same operator more than once in a query

  

**Question**

Using the routes collection find out how many CR2 and A81 airplanes come through the KZN airport?

  

**False:**

  

```bash
	{ “$or” : [ {dst_airport : “KZN”}, {src_airport: “KZN”}]}
```

  

and

  

```bash
	{“$or”: [ {airplane: “CR2”}, { airplane: “A81” } ] }
```

  

**True:**

  

```bash
{ “$and”: [{ “$or” : [ {dst_airport : “KZN”}, {src_airport: “KZN”}]},
		   {“$or”: [ {airplane: “CR2”}, { airplane: “A81” } ] } ] }
```

  

Summary of Logical Operators:

  

Logical operators allow us to be more granular in our search for data

  

Syntax

  

{ “$<operator>”: [ { <clause1> }, { <clause2>}, … ] } for all logical queries but the $not operator { $not : { <clause> } }

  

**$and** is used as the default operator when an operator is not specified.

  

Explicitly use **$and** when you need to include the same operator more than once in a query.

  

**Problem 1:**

How many businesses in the sample_training.inspections dataset have the inspection result "Out of Business" and belong to the "Home Improvement Contractor - 100" sector?

  

**Answer:**

  

```bash
	db.inspections.find({"$and": [{"result": "Out of Business"}, 
								  {"sector": "Home Improvement Contractor - 100"}]}).count()
```

**Problem 2:**

How many zips in the sample_training.zips dataset are neither over-populated nor under-populated?

In this case, we consider population of more than 1,000,000 to be over- populated and less than 5,000 to be under-populated.

  

**Answer:**

  

```bash
	db.zips.find({ "pop": { "$gt": 5000, "$lt": 1000000 }}).count()
```

```bash
	db.zips.find({ "$nor": [ { "pop": { "$lt":5000 } },{ "pop": { "$gt": 1000000 } } ] } ).count()
```

**Problem 3:**

How many companies in the sample_training.companies dataset were

either founded in 2004

-   [and] either have the _social_ category_code [or] _web_ category_code,

[or] were founded in the month of October

-   [and] also either have the _social_ category_code [or] _web_ category_code?

  

**Answer:**

  

```bash
db.companies.find({ "$and": [

	{ "$or": [ { "founded_year": 2004 },

	{ "founded_month": 10 } ] },

	{ "$or": [ { "category_code": "web" },

	{ "category_code": "social" }]}]}).count()
```

  

3.Expressive Query Operator ($expr)

  

It is expressive, meaning it can do more than one simple operation. It allows the use of aggregation expressions within the query language, and it uses this syntax.

  

Syntax:

**{ $expr: { <expression> } }**

  

$expr, also allows us to use variables and conditional statements.

  

We were comparing a field’s value to some number. We can compare fields **within the same document** to each other.

  

_Find all documents where the trip started and ended at the same station:_

  

```bash
	db.trips.find( { "$expr": { "$eq": [ "$end station id", "$start station id"] } } ).count()
```

  

The dollar sign symbol a lot of power in MQL. One of them is to denote when you’re using an operator. Another one is the signify that you’re looking at the value of that field, rather than just the field name itself.

  

**$**

-   $ denotes the use of an operator.
-   $ addresses the field value.

  

```bash
	{ "$expr": { "$eq": [ "$start station id”, “$end station id" ] } }
```

  

**$start station id**: Means the value 439.

  

-   If we were to use $start station name, that would mean E 4th Street and 2nd Avenue.
-   If we don’t use the dollar sign in this case, we have to look for a specific value field in all document, rather than compare a value that varies from document to document to another value that varies from document to document.

  

```bash
{

"_id": {
	"$oid": "572bb8222b288919b68abf70"
},
	"tripduration": 110,
	"start station id": 439,
	"start station name": "E 4 St & 2 Ave",
	"end station id": 439,
	"end station name": "E 4 St & 2 Ave",
	"bikeid": 24021,
	"usertype": "Customer",
	"birth year": "",
	"start station location": {
	"type": "Point",
	"coordinates": [
		-73.98978041,40.7262807
]},
"end station location": {
"type": "Point",
"coordinates": [
	-73.98978041,40.7262807
]},
"start time": {
	"$date": {
	"$numberLong": "1451607024000"
}},
"stop time": {
	"$date": {
	"$numberLong": "1451607135000"
}}}
```

  

**Question:**

-   Another question that I have for this data set is how many of these people rented the bikes out for more than o couple of minutes?

  

**Answer:**

  

-   _Find all documents where the trip started and ended at the same station:_

  

```bash
	db.trips.find({ "$expr": { "$eq": [ "$end station id", "$start station }).count()
```

  

-   _Find all documents where the trip lasted longer than_ 1200 _seconds, and started and ended at the same station:_

  

```bash
	db.trips.find({ "$expr": { "$and": [ { "$gt": [ "$tripduration", 1200 ]},
							 { "$eq": [ "$end station id", "$start station id" ]} 
																			   ]}}).count()
```

  

A closer look into that query:

  

1.  We added greater than operator to our equals operator under the same “$and” umbrella.

1.  MQL Syntax:  { <field>: { <comparison_operator>: <value> } }
2.  Aggregation Sytax: { <operator>: { <field>: <value> } }

  

**Problem:**

Which of the following statements will find all the companies that have more employees than the year in which they were founded?

  

**Answer:**

  

```bash
	db.companies.find({ "$expr": { "$gt": [ "$number_of_employees", "$founded_year" ] }}).count()
```

  

```bash
	db.companies.find({ "$expr": { 
						"$lt": [ "$founded_year", "$number_of_employees" ] } } ).count()
```

  

**Problem:**

How many companies in the sample_training.companies collection have the same permalink as their twitter_username?

  

**Answer:**

  

```bash
	db.companies.find({ "$expr": { "$eq": [ "$permalink", "$twitter_username" ] } }).count()
```

  

4.Array Operators

  

**$push,** allows us to add an element to an array. Or turn a field into an array field if it was previously a different type of value.

  

**$size,** array operator will return all documents where the specified array field is exactly the given length.

  

```bash
	{ <array field> : { “**$size**”: <number> } }
```

  

**$all,** array operator will return a cursor with all documents in which the specified array field contains all the given elements, regardless of their order in the array.

  

```bash
	{ <array field> : { “**$all**”: <number> } }
```

  

When querying an array field with an array match, MongoDB will look for an exact array match, unless specified otherwise.

  

When querying an array field with a single element, MongoDB will return all documents where the specified array field contains this given element.

  

_Find all documents with exactly_ 20 _amenities which include all the amenities listed in the query array:_

  

```bash
db.listingsAndReviews.find({ "amenities": {
		"$size": 20,
		"$all": [ "Internet", "Wifi",  "Kitchen",
				  "Heating", "Family/kid friendly",
				  "Washer", "Dryer", "Essentials",
				  "Shampoo", "Hangers",
				  "Hair dryer", "Iron",
				  "Laptop friendly workspace" ]}}).pretty()
```

  

**Problem:**

What is the name of the listing in the sample_airbnb.listingsAndReviews dataset that accommodates more than 6 people and has exactly 50 reviews?

Copy/Paste the value of the "name" field into the response field **without** quotation marks.

  

**Answer:**

  

```bash
	db.listingsAndReviews.find({ "reviews": { "$size":50 },"accommodates": { "$gt":6 }})
```

  

-   We can use the $size operator to select only the documents that have exactly 50 elements in the reviews field. This query can also run in Atlas so that it is easier to see the value of the name field right away.

  

```bash
	db.listingsAndReviews.find({ “amenities”: { "$eq":50 },"accommodates": { "$gt":6 }})
```

  

**Problem:**

Using the sample_airbnb.listingsAndReviews collection find out how many documents have the "property_type" "House", and include "Changing table" as one of the "amenities"?

Enter the number of results to the response field.

  

**Answer:**

  

```bash
db.listingsAndReviews.find({ "amenities": { $all:  [ "Changing table" ] }, 
										"property_type" : { "$eq": "House"} }).count() —> 11
```

  

**Problem:**

Which of the following queries will return all listings that have "Free parking on premises", "Air conditioning", and "Wifi" as part of their amenities, and have at least 2 bedrooms in the sample_airbnb.listingsAndReviews collection?

  

**Answer:**

  

```bash
	db.listingsAndReviews.find({ "amenities":{ "$all": [ "Free parking on premises",
														 "Wifi", 
														 "Air conditioning" ] }, 
														 "bedrooms": { "$gte":  2 } } ).pretty()
```

  

5.Array Operators and Projection

  

Projection:

  

_Find all documents with exactly_ 20 _amenities which include all the amenities listed in the query array, and display their_ price _and_ address:

  

```bash
	db.listingsAndReviews.find({ "amenities":{ "$size": 20, 
	   "$all": ["Internet", 
				"Wifi",  
				"Kitchen", 
				"Heating",
				"Family/kid friendly", 
				"Washer", 
				"Dryer",
				"Essentials", 
				"Shampoo", 
				"Hangers",
				"Hair dryer", 
				"Iron",
				"Laptop friendly workspace" ] } },{"price": 1, "address": 1}).pretty()
```

  

1.  The first part of that query we’re looking for.
2.  The second is a projection describing specifically which fields we’re looking for.

  

This way cursor doesn’t have to include every single field in the result set. (Closer look to above example; only include **price** and **address** fields in the cursor result.)

As this travel search, I want to know the price and address information only, so that is what I specify in my projection.

  

**Projection Syntax:**

  

db.<collection>.find( { <query> }, { <projection> } )

  

1 - include the field. ( Want to see)

0 - exclude the field. ( Don’t want to see)

  

Use only 1s or only 0s.

  

When using projection, you can specify which fields you do or don’t want to see in the resulting cursor. You can’t mix zeros and ones in a single projection. If you are using ones, than you’ll only get the fields that you specified, plus the **_id** fields.

  

```bash
	db.<collection>find( { <query> }, { <field1>: 1, <field2>: 1 } )
```

  

If you are using zeros, the you’ll get all the fields except for the ones that you specifically excluded.

  

```bash
	db.<collection>find( { <query> }, { <field1>: 0, <field2>: 0 } )
```

  

****EXCEPTION****

  

The only time when you can mix ones and zeros is when you’re specifically asking to exclude the **_id** field, because it will be included by default otherwise.

  

```bash
	db.<collection>find( { <query> }, { <field1>: 1, <field2>: 1} )
```

  

**$elemMatch,** an array operator that can be used both in query and projection part of the find() command.

  

```bash
	{ <field>: { “**$elemMatch**”: { <field>: <value> } } }
```

  

$elemMatch, matches documents that contain an array field with at least one element that matches all the specified query criteria, or projects only the array elements with at least one element that matches the specified criteria.

  

_Find all documents where the student in class_ 431 _received a grade higher than_ 85 _for any type of assignment:_

  

```bash
	db.grades.find({ "class_id": 431 },{ "scores": { "$elemMatch": { 
                                                                "score": { "$gt": 85 } } } 
                    } ).pretty()
```

  

_Find all documents where the student had an extra credit score:_

  

```bash
	db.grades.find({ "scores": { "$elemMatch": { "type": "extra credit" } } } ).pretty()
```

  

**Problem:**

How many companies in the sample_training.companies collection have offices in the city of Seattle?

Copy/paste your answer to the response field.

  

**Answer:**

  

```bash
	db.companies.find({ "offices": { "$elemMatch": { "city": "Seattle" } } }). count()
```

  

**Problem:**

Which of the following queries will return only the names of companies from the sample_training.companies collection that had exactly 8 funding rounds?

  

**Answer:**

  

```bash
	db.companies.find({ "funding_rounds": { "$size": 8 } },{ "name": 1, "_id": 0 })
```

  

6.Array Operators and Sub-Documents

  

The field name from the sub document follows the top-level field separated by a dot or a period, and the whole thing is included in quotes.

  

**$regex**

  

Provides regular expression capabilities for pattern matching strings in queries. MongoDB uses Perl compatible regular expressions (i.e. "PCRE" ) version 8.42 with UTF-8 support.

  

To use `$regex`, use one of the following syntaxes:

  

```bash
	{ <field>: { $regex: /pattern/, $options: '<options>' } }

	{ <field>: { $regex: 'pattern', $options: '<options>' } }

	{ <field>: { $regex: /pattern/<options> } }
```

In MongoDB, you can also use regular expression objects (i.e. /pattern/) to specify regular expressions:

  

```bash
	{ <field>: /pattern/<options> }
```

For more about [$regex](https://www.mongodb.com/docs/manual/reference/operator/query/regex/).

  

```bash
	db.trips.findOne({ "start station location.type": "Point" }) 

	db.companies.find({ "relationships.0.person.last_name": "Zuckerberg" },
					  { "name": 1 }).pretty()
  
	db.companies.find({ "relationships.0.person.first_name": "Mark",
					    "relationships.0.title": { "$regex": "CEO" } },
					  { "name": 1 }).count()

	db.companies.find({ "relationships.0.person.first_name": "Mark",
					    "relationships.0.title": {"$regex": "CEO" } },
					  { "name": 1 }).pretty()

	db.companies.find({ "relationships":{ "$elemMatch": { 
						"is_past": true,
						"person.first_name": "Mark" } } },
					  { "name": 1 }).pretty()

	db.companies.find({ "relationships":{ "$elemMatch": { 
						"is_past": true,
						"person.first_name": "Mark" } } },
					  { "name": 1 }).count()
```

  

**Problem:**

How many trips in the sample_training.trips collection started at stations that are to the west of the -74 longitude coordinate?

Longitude decreases in value as you move west.

Note: We always list the longitude first and then latitude in the coordinate pairs; i.e.
```bash
	<field_name>: [ <longitude>, <latitude> ]
```

**Answer:**

  

```bash
	db.trips.find({ "start station location.coordinates.0": { "$lt": -74 }}).count()
```

The _"start station location"_ has a sub-document that contains the coordinates array. To get to this coordinates array we must use use dot-notation. We can issue a range query to find all documents in this longitude. The caveat is to remember that all trips take place in NYC so the latitude value in the coordinates array will always be positive, and we don't have to worry about it when issuing a range query like this.

  

**Problem:**

How many inspections from the sample_training.inspections collection were conducted in the city of NEW YORK?

  

**Answer:**

  

```bash
	db.inspections.find({ "address.city": "NEW YORK" }).count()
```

Here we need to use dot-notation to get to the "city" field and search for all documents where this field is equal to "NEW YORK".

  

**Problem:**

Which of the following queries will return the names and addresses of all listings from the sample_airbnb.listingsAndReviews collection where the first amenity in the list is "Internet"?

  

**Answer:**

  

```bash
	db.listingsAndReviews.find({ "amenities.0": "{ "name": 1, "address": 1 }).pretty()
```

To reach the first element in an array field we need to use dot notation and the element's position which is zero for the first element in most arrays in most languages. For the projection part, we don't need to explicitly exclude the _id field because the question prompt isn't terribly strict about that.

  

  

**Chapter 5**

  

  

1.Aggregation Framework

  

An aggregation framework, in its simplest form, is just another way to query data in MongoDB.

  

Syntax:

  

_Find all documents that have_ Wifi _as one of the amenities. Only include_ price _and_ address _in the resulting cursor._

  

```bash
	db.listingsAndReviews.find({ "amenities": "Wifi" },
							   {"price": 1, "address": 1, "_id": 0 }).pretty()
```


  

To use the aggregation framework, we use aggregate instead of find. The reason for that is because sometimes we might want to aggregate, as in group or modify our data in some way, instead of always just filtering for the right documents.

  

This means that you can perform operations other than finding and projecting data.

  

But you can also calculate using aggregation.

  

  

```bash
db.listingsAndReviews.aggregate([
	{ $match: { “amenities”: “Wifi” } },
	{ $project: { “price”: 1, “address”: 1, “_id”:0 } }
])
```

  

The aggregation framework works as a pipeline, where the order of actions in the pipeline matters. And each action is executed in the order in which we list it.

  

**$group:** The group stage is one of the many stages that differentiates the aggregation framework from MQL(compute, reshape).  With MQL, we can filter and update data. With the aggregation framework we can compute and reshape data.

  

An operator that takes the incoming stream of data, and siphons in into multiple distance reservoirs.

  

-   Non-filtering stages do not modify the original data. When they do the summaries, calculations, and groupings of data. Instead they work with the data they get previous stage in the pipeline, which is in its own cursor.

  

_Find one document in the collection and only include the_ address _field in the resulting cursor._

  

```bash
	db.listingsAndReviews.findOne({ },{ "address": 1, "_id": 0 })
```

  

$group stage syntax:

  

```bash
{$group:{
	_id: <expression>, // Group By Expression
	<field>: { <accumulator1>: <expression1> },
	… } }
```

  

As the group stage receives documents from the previous stage, it uses the expression that we provide in the _id field to identify the group that this documents belongs to.

  

```bash
	db.listingsAndReviews.aggregate( [ { $project: { "address": 1, "_id": 0 } }, 
									   { $group: { “_id”: “$address.country } } ] )
```

  

```bash
	db.listingsAndReviews.aggregate( [ { $project: { "address": 1, "_id": 0 } }, 
									   { $group: { “_id”: “$address.country”, 
												   “count”: { “$sum”: 1 } } } ] )
```

  

Aggregation Framework > MQL - Pipeline stages in order - Syntax

  

  

**Problem:**

What room types are present in the sample_airbnb.listingsAndReviews collection?

  

**Answer:**

  

```bash
	db.listingsAndReviews.aggregate([ { "$group": { "_id": "$room_type" } }])
```

  

**Problem:**

What are the differences between using aggregate() and find()?

  

**Answer:**

  

```bash
-   aggregate() can do what find() can and more.
Any find() query can be translated into an aggregation pipeline equivalent, 
but not every aggregation pipeline can be translated into a find() query.


-   aggregate() allows us to compute and reshape data in the cursor.
The aggregation framework allows us to compute and reshape data via using stages like 
$group, $sum, and others.
```