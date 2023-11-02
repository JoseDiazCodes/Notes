# Server.js File Breakdown

#### Importing Libraries and Initializing Variables

```js
const express = require("express");
const app = express();
const bodyParser = require("body-parser");
const MongoClient = require("mongodb").MongoClient;
```

> Here, we are importing the required libs and creating an instance of the Express app. We are also initializing the **Mongo Client** from the _MongoDB library_

```js
var db, collection;
```

> Here, we are declaring the variables to store the reference to the MongoDB database and collection

Keep in mind that collection is something that we still haven't used in the code so that's a starting point to debug

#### MongoDB Connection string and Database Name

```js
const url =
	"mongodb+srv://demo:demo@cluster0-q2ojb.mongodb.net/test?retryWrites=true";
const dbName = "demo";
```

> Here we are defining the connection string for MongoDB and specifying the name of the database I will be using

#### Setting Up the Express Server

```js
app.listen(3000, () => {
	MongoClient.connect(
		url,
		{ useNewUrlParser: true, useUnifiedTopology: true },
		(error, client) => {
			if (error) {
				throw error;
			}
			db = client.db(dbName);
			console.log("Connected to `" + dbName + "`!");
		}
	);
});
```

> We are setting up the Express application to listen on port 3000. Once the server is running, it tries to connect to your MongoDB database. If it connects successfully, it logs a confirmation message to the console.

#### Configuring Express

```js
app.set("view engine", "ejs");
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use(express.static("public"));
```

> Here, we are setting 'ejs' as the templating engine. We are also configuring the body parser to handle URL-encoded data and JSON-formatted data. The express.static('public') line tells Express to serve static files (like CSS, images, etc.) from the 'public' directory without having you to explicitly route everything manually

#### Handling GET Requests to the Home Page

```js
app.get("/", (req, res) => {
	db.collection("messages")
		.find()
		.toArray((err, result) => {
			if (err) return console.log(err);
			res.render("index.ejs", { messages: result });
		});
});
```

> This code sets up a route to handle GET requests to the home page ('/'). It queries the 'messages' collection in your MondoDB database, converts the results to an array, and then renders the 'index.ejs' view, passing in the messages.

#### Handling POST Requests to Add a Message

```js
app.post("/messages", (req, res) => {
	db.collection("messages").insertOne(
		{ name: req.body.name, msg: req.body.msg, thumbUp: 0, thumbDown: 0 },
		(err, result) => {
			if (err) return console.log(err);
			console.log("saved to database");
			res.redirect("/");
		}
	);
});
```

> This route handles POST requests to add a new message, It insets a new document into the 'messages' collection with the data received from the client and initializes the 'thumbUP' and 'thumbDump' properties to 0. After insertion, it redirects the client back to the home pages.

#### Handling PUT Requests to Update a Message

```js
app.put("/messages", (req, res) => {
	db.collection("messages").findOneAndUpdate(
		{ name: req.body.name, msg: req.body.msg },
		{
			$set: {
				thumbUp: req.body.thumbUp + 1,
			},
		},
		{
			sort: { _id: -1 },
			upsert: true,
		},
		(err, result) => {
			if (err) return res.send(err);
			res.send(result);
		}
	);
});
```

> This route handles PUT requests to update a message's 'thumbUp' value. It finds a message by 'name' and 'msg', increments its 'thumbUp' value by 1, and returns the updated message. If the message doesn’t exist, it creates a new one.

#### Handling DELETE Requests to Remove a Message

```js
app.delete("/messages", (req, res) => {
	db.collection("messages").findOneAndDelete(
		{ name: req.body.name, msg: req.body.msg },
		(err, result) => {
			if (err) return res.send(500, err);
			res.send("Message deleted!");
		}
	);
});
```

> This route handles DELETE requests to remove a message. It find a message by 'name' and 'msg' and delete it from the 'messages' collection.

## Goals

1. [x] Get sort from highest upvoting to lowest working (Ambitious)

```js
app.get("/", (req, res) => {
	db.collection("messages")
		.find()
		.sort({ thumbUp: -1 }) // changed this to sort from highest liked to lowest.
		.toArray((err, result) => {
			if (err) return console.log(err);
			res.render("index.ejs", { messages: result });
		});
});
```

> The .sort({ thumbUp: -1 }) is a method used in MongoDB, a popular NoSQL database, to sort the results of a query.

> In this specific instance, the .sort({ thumbUp: -1 }) method is sorting the documents in the collection based on the thumbUp field in descending order. The -1 denotes a descending sort order, while 1 would denote an ascending sort order.

> Here’s a brief breakdown:

> `.sort():` This is a MongoDB method used to sort the results of a query.
> `{ thumbUp: -1 }:` This is an object that specifies the sort order. In this case, it’s saying to sort by the thumbUp field in descending order.
> When you run a query with this sort method, MongoDB will return the documents ordered from the one with the highest thumbUp value to the one with the lowest. If thumbUp is a numerical field, for example, the document with the highest number will be first, and the one with the lowest number will be last.

```js
{ _id: 1, name: 'Alice', thumbUp: 10 }
{ _id: 2, name: 'Bob', thumbUp: 5 }
{ _id: 3, name: 'Charlie', thumbUp: 15 }
```

```js
{ _id: 3, name: 'Charlie', thumbUp: 15 }
{ _id: 1, name: 'Alice', thumbUp: 10 }
{ _id: 2, name: 'Bob', thumbUp: 5 }
```

---

2. [x] Get the downvote working...

```js
app.put("/messages", (req, res) => {
	db.collection("messages").findOneAndUpdate(
		{ name: req.body.name, msg: req.body.msg },
		{
			$set: {
				thumbUp: req.body.decrement
					? req.body.thumbUp - 1
					: req.body.thumbUp + 1,
				// added this
			},
		},
		{
			sort: { _id: -1 },
			upsert: true,
		},
		(err, result) => {
			if (err) return res.send(err);
			res.send(result);
		}
	);
});
```

```js
$set: {
	thumbUp: req.body.decrement
		? req.body.thumbUp - 1
		: req.body.thumbUp + 1,
	// added this
},
```

> In this section, $set is used to specify the fields to update in the found document. Here's what's happening:

> thumbUp: This field is being updated based on the condition provided.
> If req.body.decrement is truthy (i.e., it exists and is not false), then it decreases the thumbUp value by 1.
> If req.body.decrement is falsy, then it increases the thumbUp value by 1.

```js
Array.from(thumbUp).forEach(function (element) {
	element.addEventListener("click", function () {
		const name = this.parentNode.parentNode.childNodes[1].innerText;
		const msg = this.parentNode.parentNode.childNodes[3].innerText;
		const thumbUp = parseFloat(
			this.parentNode.parentNode.childNodes[5].innerText
		);
		fetch("messages", {
			method: "put",
			headers: { "Content-Type": "application/json" },
			body: JSON.stringify({
				name: name,
				msg: msg,
				thumbUp: thumbUp,
				decrement: false,
			}),
		})
			.then((response) => {
				if (response.ok) return response.json();
			})
			.then((data) => {
				console.log(data);
				window.location.reload(true);
			});
	});
});

// added the code below
Array.from(thumbDown).forEach(function (element) {
	element.addEventListener("click", function () {
		const name = this.parentNode.parentNode.childNodes[1].innerText;
		const msg = this.parentNode.parentNode.childNodes[3].innerText;
		const thumbUp = parseFloat(
			this.parentNode.parentNode.childNodes[5].innerText
		); // changed this to 5 because thats the location of the button
		fetch("messages", {
			method: "put",
			headers: { "Content-Type": "application/json" },
			body: JSON.stringify({
				name: name,
				msg: msg,
				thumbUp: thumbUp,
				decrement: true, // added this to fire when you press the thumbs down button and decrement the thumbsup by 1 serverside
			}),
		})
			.then((response) => {
				if (response.ok) return response.json();
			})
			.then((data) => {
				console.log(data);
				window.location.reload(true);
			});
	});
});
```

---

### Suggestions:

> It's worth noting that the value for thumbUp is being taken directly from req.body, which implies that the client sending the request is responsible for providing the current thumbUp value. This could potentially lead to issues if multiple clients are updating the same document simultaneously, as they might not have the most up-to-date value when they send their update. A more robust solution might involve using the $inc operator to increment or decrement the thumbUp field, which would ensure atomic updates and prevent potential race conditions.

---

#### Example using `$inc` instead of `$set`:

```js
app.put("/messages", (req, res) => {
	db.collection("messages").findOneAndUpdate(
		{ name: req.body.name, msg: req.body.msg },
		{
			$inc: {
				thumbUp: req.body.decrement ? -1 : 1,
			},
		},
		{
			sort: { _id: -1 },
			upsert: true,
			returnDocument: "after",
		},
		(err, result) => {
			if (err) return res.send(err);
			res.send(result);
		}
	);
});
```

#### Changes:

- Instead of $set, we are now using $inc.
- The thumbUp field is updated with -1 if req.body.decrement is truthy, and 1 otherwise. This will increment or decrement the existing value of thumbUp in the document directly, ensuring that the update is atomic.
- I've added the option returnDocument: 'after' to the options object. This ensures that the modified document is returned in the result of the findOneAndUpdate call, rather than the original document. This option is the equivalent of the returnNewDocument: true option in some MongoDB drivers.

  > With these changes, the client no longer needs to send the current value of thumbUp in the request body. Instead, it simply indicates whether it wants to increment or decrement the value, and MongoDB takes care of updating the field atomically. This prevents issues that could arise from multiple clients trying to update the field simultaneously with stale values.
