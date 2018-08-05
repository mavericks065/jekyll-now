---
layout: post
title: MongoDB, GridFS and MongoFiles
---
So today I will talk about the file management into MongoDB. Indeed I met some issues while manipulating them so I thought some people could be happy to have a basic article on GridFS and MongoFiles.

First, you need to know that MongoDB is storing objects in a binary format called BSON. Then Mongo cannot store objects whose size is superior than 16 MB, in the case your document exceeds this weight the file is chunked.

## MongoDB: MongoFiles

It is used to manipulate files you want to insert in your database or documents you already have stored in your Mongo database.

Mongo files are stored under GridFS objects in your collection.

**What is the the basic command of MongoFile?**

First, there are 3 components in a mongofile command :

* **Options**: you can have 1 or more. We’ll see below some of them.
* **Commands**: to choose what action we want to do on our files.
* **Filename**: which is either: the name of a file on your local’s file system, or a GridFS object.


**mongofiles \<options\> \<commands\> \<filename\>**

Mongofiles can access data stored in your database even if you do not have a running mongod instance. More precisely it will access data stored in your MongoDB data directory you use for your instance when you’re running it.

In case of replicaSet it will read only the primary.

* Options ( just the ones I think we will all use one day if we work on mongoDB)

--help

Returns information on the options of MongoFiles

--version

Returns the MongoFiles release number.

--host <hostname><:port>

Specifies a resolvable hostname for the MongoDB that holds your GridFS system. By default, it attempts to connect to the process running on the localhost port number 27017.

--port <port>

Default: 27017

Specifies the TCP port on which the MongoDB instance listens for client connections.

--ssl

Enables connection to a Mongod that has SSL support enabled.

The default distribution of MongoDB does not contain support for SSL.

--username <username>, -u <username>

Specifies a username with which to authenticate to a MongoDB database that uses authentication. Use in conjunction with the --password and --authenticateDatabase options.

--password <password>, -p <password>

Specifies a password with which to authenticate to a MongoDB database that uses authentication.

--dbpath <path>

Specifies the directory of the MongoDB data files. Can be very useful if you like to have a complete control of where you have your data directory

--db <database>, -d <database>

Specifies the name of the database on which to run the mongofiles.

--replace, -r

Alters the behavior of mongofiles put to replace existing GridFS objects with the specified local file, rather than adding an additional object with the same name.

In the default operation, files will not be overwritten by a mongofiles put option.

* Commands
    - list <prefix>

    Lists the files in the GridFS store. The characters specified after list (e.g. <prefix>) optionally limit the list of returned items to files that begin with that string of characters.

    - search <string>

    Lists the files in the GridFS store with names that match any portion of <string>.

    - put <filenameYouWantYourFileToHaveInYourMongoDB>

    Copy the specified file from the local file system into GridFS storage.

    - get < filenameYourObjectWillHaveInGRIDFS>

    Copy the specified file from GridFS storage to the local file system.

    - delete <filename>

    Delete the specified file from GridFS storage.

Example :

mongofiles -d myMongoDB list

mongofiles -d myMongoDB put /home/java-4all/myFile.txt

If you want more examples or more options you should visit the official documentation here

## MongoDB: GridFS

Instead of storing a file in a single document, GridFS divides a file into chunks and stores each of those chunks as a separate document. And it uses 2 collections to store files. One is used for the Metadata the other for the chunks.

By default, GridFS limits chunk size to 255k.

Obviously, when you query a GridFS store for a file, the client will reassemble the chunks as needed.

For using GridFS, the official documentation recommends to use MongoFiles – we just saw it above – or the MongoDB driver.

**What are the GridFS collections?**

* Chunks
* Files

When you have a look you see them prefixed by a « fs ». And you think: this guy is saying bullshit.

Nope! MongoDb puts them in the same bucket!

Each document in the chunks collection represents a distinct chunk of a file as represented in the GridFS store. Each chunk is identified by its unique ObjectId stored in its « _id » field.

What are the fields in these collections ?

The “fs.files”  collections contains MetaData.

```json
{

“_id” : <unspecified>  //Unique ID per File.
“filename” : data_string  // Human name per File.
“chunkSize” : data_number  // Size of Each Chunks , Default is 256k.
“uploadDate” : data_date  // Date when object first stored.
“md5″ : data_string  // MD5 hash for the binary data.
“length” : data_number   // Size of the files in bytes.
}
```

The “fs.chunks” collections contain Binary Data
```json
{
“_id” : <unspecified>  // Object id of the chunk in the _chunks collections
“files_id” : <unspecified>  // _id of the corresponding files collection entry.
“n” : chunk_number  // Chunks are numbered in order,  starting with 0.
“data” : data_binary  //  The chunk ’s payload as a BSON binary type.

}
```

More information? [Here is the official documentation](http://docs.mongodb.org/manual/core/gridfs/).

Hope it will help you in your projects :)