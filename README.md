# nodeExp2021Passport


Note: Clone of nodeExp2021Mongo returned no /src/routers folder
If this folder and node_modules are added npm start will work 


------------

Continuation of Pluralsight tutorial 
Building Web Applications with Node.js and Express
by Jonathan Mills

https://app.pluralsight.com/library/courses/nodejs-express-web-applications-building/

How to build from scratch  routing, databases, and third-party APIs in Node.js and Express.

nodeExp2021 is static, without MongoDB


Remember to update package.json
"ejs": "^3.1.8",
 "express": "4.18.2",

cd to directory

	npm install
	npm start
http://localhost:4000/

---------

This part of the project works with
"mongodb": "3.6.6",
and 

mongodb+srv://<username>:<password>@<clustername>...
(find notes for Globomantics)

Remember to update app.js to address deprication warning
app.use(session({ secret: 'globomantics' }));
to
app.use(session({
  secret: 'globomantics',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}))

In local.strategy.js adminRouter.js authRouter.js updated MongoClient params to address warnings
            try {
              client = await MongoClient.connect(url);

            try {
              client = await MongoClient.connect(url, { useUnifiedTopology: true });
---------


-----------------

Jim Lynch 
a year ago edited
In Lesson 8: Creating a User: - authRouter.js
If you use MongoDB driver 4.x.x+, be warned collection.insertOne() will no longer return a document, but rather the inserted _id: and acknowledgement. If you want the document, you'll have to .find the document after inserting it:

const results = await db.collection('users').insertOne(user);
debug(results);
const returnedUser = await db.collection('users').findOne({ _id: results.insertedId});
debug(returnedUser);
req.login(returnedUser, () => {
res.redirect('/auth/profile');
});

credit: https://stackoverflow.com/q...


// note: Jim Lynch disscussion  change in MongodB
// MongoDB 4.x+,  collection().insertOne() no longer returns a doc,
// see https://stackoverflow.com/questions/68555397/return-inserted-document-in-mongodb-node-js

// removed
// const results = await db.collection('users').insertOne(user);
// debug(results);
// req.login(results.ops[0], () => {
//   res.redirect('/auth/profile');
// });









