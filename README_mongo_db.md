### What is MongoDB?

- MongoDB is a document-oriented database that stores 
data in a flexible, JSON-like format. It is often used 
for applications that 
require high levels of scalability and performance.

### What are NoSQL databases? How do they differ from SQL?

- NoSQL databases are non-relational 
databases that store and retrieve data in a 
different way than SQL databases. Unlike SQL databases, 
NoSQL databases do not use a 
fixed schema and can handle unstructured data types.

### Why is MongoDB popular?

- MongoDB is popular because it is highly scalable, 
performs well with large amounts of data, and can be 
used for a wide range of applications. Its history 
dates back to 2007 when it 
was first released as an open-source project.

### What is it’s history?

- MongoDB was first developed by Dwight Merriman and Eliot Horowitz 
in 2007 while they were working on a web application platform called 
10gen. They found that the traditional SQL databases were not well-suited 
for the type of web applications they were building, which required flexible 
data models and the ability to scale horizontally across multiple servers.
- To address these limitations, Merriman and Horowitz created MongoDB as a scalable, 
document-oriented database that could handle large amounts of unstructured 
data. They released MongoDB as an open-source project in 2009, 
and it quickly gained popularity among developers who were looking 
for a more flexible alternative to SQL databases.
Today, MongoDB is used by a wide range of organizations, 
from small startups to large enterprises, and has become one of the 
most popular NoSQL databases on the market.


![mongo_diagram.png](files%2Fmongo_diagram.png)

- The MongoDB cluster architecture mainly includes three parts: 
the shard server, the router server, and the config server. 
The actual data are stored in the shard server, which can be 
a replica set or a server. The router server is the entry that 
clients request the database and is used to address and locate 
the requests from these clients. 
All these requests need to be handled by mongos and forwarded 
to the corresponding shard server. The config server is used 
to store the configuration information of the router and the 
shard, which is set up at first and does not need significant 
space and resources.

### What is seeding in MongoDB? Why do Mongo databases need to be seeded?

Seeding in MongoDB refers to the process of populating a database with initial data. This data can be used for various purposes, such as testing, development, or setting up a new instance of the database.


- In the context of testing, seeding is often used to create a set of test data that can be used to verify that the database is working correctly. For example, a developer may want to test how the application handles different types of data or scenarios, and they can use seeded data to simulate these scenarios.

- In development, seeding can be used to create a set of initial data that can be used to kickstart the development process. For example, a developer may want to create a set of default user accounts or sample data that can be used to showcase the application's functionality.

- When setting up a new instance of the database, seeding can be used to ensure that the database is populated with initial data that is necessary for the application to function correctly. For example, a new instance of the database may need to be seeded with default settings or configurations to ensure that the application can run properly.


Overall, seeding is a useful technique in MongoDB that can save developers time and effort by providing them with a set of initial data that can be used for various purposes.

### What port does MongoDB use?

- MongoDB uses port 27017 by default, 
but it can be configured to use a different port if necessary.

### How do you connect to a Mongo database?

- To connect to a MongoDB database, you can use the 
MongoDB shell, which is a command-line tool that allows you to interact with the database using JavaScript commands. You can also use a MongoDB driver, which is a software component that 
allows you to connect to the database from within an application.