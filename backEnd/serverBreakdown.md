# Index.html

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>MY APP</title>
	</head>
	<body>
		May Node and Express be with you.

		<form action="/items" method="POST">
			<input type="text" placeholder="name" name="name" />
			<input type="text" placeholder="quote" name="quote" />
			<button type="submit">Submit</button>
		</form>
	</body>
</html>
```

---

## Index.ejs

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>21 Savage Fans</title>
  <link rel="shortcut icon" href="favicon.ico">
  <link rel="stylesheet" href="font-awesome.min.css">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>21 Savage</h1>
  <h2>Why you trappin so hard?</h2>


  <h3>Messages</h3>
  <ul class="messages">
  <% for(var i=0; i<messages.length; i++) {%>
    <li class="message">
      <span><%= messages[i].name %></span>
      <span><%= messages[i].msg %></span>
      <span><%= messages[i].thumbUp %></span>
      <span><i class="fa fa-thumbs-up" aria-hidden="true"></i></span>
      <span><i class="fa fa-thumbs-down" aria-hidden="true"></i></span>
      <span><i class="fa fa-trash" aria-hidden="true"></i></span>
    </li>
  <% } %>
  </ul>

  <h2>Add a message</h2>

  <form action="/messages" method="POST">
    <input type="text" placeholder="name" name="name">
    <input type="text" placeholder="message" name="msg">
    <button type="submit">Submit</button>
  </form>

  <script src="main.js"></script>

</body>
</html>

```

---

## Main.js

```js
var thumbUp = document.getElementsByClassName("fa-thumbs-up");
var trash = document.getElementsByClassName("fa-trash");
var thumbDown = document.getElementsByClassName("fa-thumbs-down"); // added this

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

Array.from(trash).forEach(function (element) {
	element.addEventListener("click", function () {
		const name = this.parentNode.parentNode.childNodes[1].innerText;
		const msg = this.parentNode.parentNode.childNodes[3].innerText;
		fetch("messages", {
			method: "delete",
			headers: {
				"Content-Type": "application/json",
			},
			body: JSON.stringify({
				name: name,
				msg: msg,
			}),
		}).then(function (response) {
			window.location.reload();
		});
	});
});
```

---

## Server.js

```js
const express = require("express");
const app = express();
const bodyParser = require("body-parser");
const MongoClient = require("mongodb").MongoClient;

var db, collection;

const url =
	"mongodb+srv://demo:demo@cluster0-q2ojb.mongodb.net/test?retryWrites=true";
const dbName = "demo";

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

app.set("view engine", "ejs");
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use(express.static("public"));

app.get("/", (req, res) => {
	db.collection("messages")
		.find()
		.sort({ thumbUp: -1 }) // changed this to sort from highest liked to lowest.
		.toArray((err, result) => {
			if (err) return console.log(err);
			res.render("index.ejs", { messages: result });
		});
});

app.post("/messages", (req, res) => {
	console.log(req);
	db.collection("messages").insertOne(
		{ name: req.body.name, msg: req.body.msg, thumbUp: 0, thumbDown: 0 },
		(err, result) => {
			if (err) return console.log(err);
			console.log("saved to database");
			res.redirect("/");
		}
	);
});

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

#### Code Breakdown:

[Server.js Breakdown](serverJS.md)
