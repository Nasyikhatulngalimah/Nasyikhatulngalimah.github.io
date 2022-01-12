const http = require("http");
const server = http.createServer((req, res) => { console.log(req.url, req.method, req.headers);
// process.exit();
});
server.listen(3000)

const http = require("http");
const server = http.createServer((req, res) => { console.log(req.url, req.method, req.headers);
// process.exit();
res.setHeader("Content-Type", "text/html"); res.write("<html>");
res.write("<head><title>My First Page</title></head>"); res.write("<body><h1>Hello From Node.js Server!</h1></body>"); res.write("</html>");
res.end();
});
server.listen(3000);

const http = require("http");
const server = http.createServer((req, res) => { const url = req.url;
if (url === "/") {
res.setHeader("Content-Type", "text/html"); res.write("<html>"); res.write("<head><title>Server</title></head>"); res.write(
'<body><form action="/message" method="POST"><input type="text" value=""></form></body>'
);
res.write("</html>"); return res.end();
} else if (url === "/secondserver") { res.setHeader("Content-Type", "text/html"); res.write("<html>");
res.write("<head><title>Server Page second</title></head>"); res.write("<body><h2>Welcome to the Internet</h2></body>"); res.write("</html>");
res.end();
}
res.setHeader("Content-Type", "text/html"); res.write("<html>");
res.write("<head><title>Server Page second</title></head>"); res.write("<body><h2>Welcome to the Internet</h2></body>"); res.write("</html>");
res.end();
});
server.listen(3000);

const http = require("http"); 
const fs = require("fs");
const server = http.createServer((req, res) => { const url = req.url;
const method = req.method; if (url === "/") {
res.setHeader("Content-Type", "text/html"); res.write("<html>"); res.write("<head><title>Server</title></head>"); res.write(
'<body><form action="/message" method="POST"><input type="text" value=""></form></body>'
);
res.write("</html>");
return res.end();
}
if (url === "/message" &amp;&amp; method === "POST") { fs.writeFileSync("testing.txt", "YOLO WORLD"); res.statusCode = 302; res.setHeader("Location", "/");
return res.end();
}
res.setHeader("Content-Type", "text/html"); res.write("<html>");
res.write("<head><title>Server Page second</title></head>"); res.write("<body><h2>Welcome to the Internet</h2></body>"); res.write("</html>");
res.end();
});
server.listen(3000);

const http = require("http"); 
const fs = require("fs");
const server = http.createServer((req, res) => { const url = req.url;
const method = req.method; if (url === "/") {
res.write("<html>"); res.write("<head><title>Server</title></head>"); res.write(
'<body><form action="/message" method="POST"><input type="text" name="message" value=""></form></body>
);
res.write("</html>"); return res.end();
}
if (url === "/message" &amp;&amp; method === "POST") { const body = [];
req.on("data", (chunk) => { console.log(chunk); body.push(chunk);
});
req.on("end", () => {
const parseBody = Buffer.concat(body).toString(); const message = parseBody.split("=")[1]; fs.writeFileSync("testing.txt", message);
});
res.statusCode = 302;
res.setHeader("Location", "/"); return res.end();
}
res.setHeader("Content-Type", "text/html"); res.write("<html>");
res.write("<head><title>Server Page second</title></head>"); res.write("<body><h2>Welcome to the Internet</h2></body>"); res.write("</html>");
res.end();
});
server.listen(3000);

const http = require("http");
const routes = require("./routes.js");
const server = http.createServer(routes.handle);
server.listen(3000);

const fs = require("fs");
const reqHandle = (req, res) => { const url = req.url;
const method = req.method; if (url === "/") {
res.write("<html>"); res.write("<head><title>Server</title></head>"); res.write(
'<body><form action="/message" method="POST"><input type="text" name="message" value=""></form></body>'
);
res.write("</html>"); return res.end();
}
if (url === "/message" &amp;&amp; method === "POST") { const body = [];
req.on("data", (chunk) => { console.log(chunk); body.push(chunk);
});
req.on("end", () => {
const parseBody = Buffer.concat(body).toString(); const message = parseBody.split("=")[1]; fs.writeFileSync("testing.txt", message);
});
res.statusCode = 302; res.setHeader("Location", "/"); return res.end();
}
res.setHeader("Content-Type", "text/html"); res.write("<html>");
res.write("<head><title>Server Page second</title></head>"); res.write("<body><h2>Welcome to the Internet</h2></body>"); res.write("</html>");
res.end();
};
exports.handle = reqHandle;

const express = require("express"); 
const http = require("http");
const app = express();
const server = http.createServer(app); server.listen(5000);

const express = require("express");
 const http = require("http");
const app = express();
app.use((req, res, next) => { console.log("In the middleware"); next();
});
app.use((req, res, next) => { console.log("In another middleware");
//	next();
});
const server = http.createServer(app);
server.listen(5000);

const express = require("express"); 
const http = require("http");
const app = express();
app.use((req, res, next) => { console.log("In the middleware"); next();
});
app.use((req, res, next) => { console.log("In another middleware"); res.send("<h1>Hello from express</h1>");
//	next();
});
const server = http.createServer(app);
server.listen(5000);

const express = require("express"); const app = express();
app.use((req, res, next) => { console.log("In the middleware"); next();
});
app.use((req, res, next) => { console.log("In another middleware"); res.send("<h1>Hello from express</h1>");
//	next();
});
app.listen(5000);

const express = require("express");
const router = express.Router();
router.get("/add-product", (req, res, next) => { res.send(
`<form action="/product/add-product" method="POST">
<input type="text" name="title">
<button type="submit">Create Product</button>
</form>`
);
});
router.post("/add-product", (req, res, next) => { console.log(req.body);
res.redirect("/");
});
module.exports = router;

const express = require("express");
const bodyParser = require("body-parser");
const shopRoutes = require("./routes/shop.routes.js");
const productRoutes = require("./routes/product.routes.js");
const app = express();
app.use(bodyParser.urlencoded({ extended: false }));
app.use("/product", productRoutes); app.use(shopRoutes);
app.listen(5000);

const express = require("express");
const router = express.Router();
router.get("/", (req, res, next) => { res.send("<h1>Hello there</h1>");
});
module.exports = router;

{
   "name":"rest",
   "version":"1.0.0",
   "description":"",
   "main":"index.js",
   "scripts":{
      "start":"nodemon server.js"
   },
   "keywords":[
      
   ],
   "author":"",
   "license":"ISC",
   "dependencies":{
      "cors":"^2.8.5",
      "dotenv":"^10.0.0",
      "express":"^4.17.1",
      "mongoose":"^6.0.8",
      "nodemon":"^2.0.13"
   }
}

const express = require("express");
	const cors = require("cors");

	const dotenv = require("dotenv");

	dotenv.config();

	const app = express();

	const PORT = process.env.PORT || 5000;

	// listen
	app.listen(PORT, () =>
	console.log(`Server is running on http://localhost:${PORT}`)
	);

const mongoose = require("mongoose");
	require("dotenv").config();

	const dbURL = process.env.MONGO_DB_URL;

	const configDatabase = async () => {
  	try {
    	await mongoose.connect(dbURL, {
      	useNewUrlParser: true,
      	useUnifiedTopology: true,
    	});
    	console.log("Database connected");
  	} catch (err) {
    	console.log(err);
    	process.exit(1);
  	}
	};

	module.exports = configDatabase;

const express = require("express");
const cors = require("cors");
const configDatabase = require("./dbConfig/database.js");

const dotenv = require("dotenv");

dotenv.config();

const app = express();

const PORT = process.env.PORT || 5000;

//connecting to the mongodb database
configDatabase();

app.use(cors({ origin: true, credentials: true }));

// add the middlewares
app.use(express.json({ extended: false }));
app.get("/", (req, res) =>
  res.send("Hello there!! Cheers !! The server is up and running")
);

// listen
app.listen(PORT, () =>
  console.log(`Server is running on http://localhost:${PORT}`)
);	

const mongoose = require("mongoose");

const TodoListSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
  },
  date: {
    type: Date,
    default: Date.now,
  },
});

const Todo = mongoose.model("todo", TodoListSchema);

module.exports = Todo;

const express = require("express");

const router = express.Router();

const {
  listAllTodo,
  createTodo,
  updateTodo,
  deleteTodo,
} = require("../controllers/todo.controller.js");

router.get("/", listAllTodo);

router.post("/", createTodo);

router.put("/:id", updateTodo);

router.delete("/:id", deleteTodo);

module.exports = router;

exports.listAllTodo = (req, res) => {
  Todo.find()
    .then((todo) => {
      console.log({ todo });
      res.json(todo);
    })
    .catch((err) => {
      res
        .status(404)
        .json({ message: "There isnt any todo available", error: err.message });
    });
};

exports.createTodo = (req, res) => {
  Todo.create(req.body)
    .then((todo) => {
      console.log({ todo });
      res.json({
        message: "Cheers!! You have successfully added TODO",
        todo,
      });
    })
    .catch((err) => {
      res.status(404).json({
        message: "Sorry your todo list cannot be added",
        error: err.message,
      });
    });
};

exports.updateTodo = (req, res) => {
  Todo.findByIdAndUpdate(req.params.id, req.body)
    .then((todo) => {
      console.log({ todo });
      return res.json({
        message: "Cheers!! You have successfully updated TODO",
        todo,
      });
    })
    .catch((err) => {
      res.status(404).json({
        message: "Sorry your todo list cannot be updated",
        error: err.message,
      });
    });
};

exports.deleteTodo = (req, res) => {
  Todo.findByIdAndRemove(req.params.id, req.body)
    .then((todo) => {
      console.log({ todo });
      res.json({
        message: "Cheers!! You have successfully deleted your TODO",
        todo,
      });
    })
    .catch((err) => {
      res.status(404).json({
        message: "Sorry your todo is not there",
        error: err.message,
      });
    });
};

const express = require("express");
const cors = require("cors");
const configDatabase = require("./dbConfig/database.js");
const todo = require("./routes/todo.routes.js");

const dotenv = require("dotenv");

dotenv.config();

const app = express();

const PORT = process.env.PORT || 5000;

//connecting to the mongodb database
configDatabase();

app.use(cors({ origin: true, credentials: true }));

// add the middlewares
app.use(express.json({ extended: false }));
app.get("/", (req, res) =>
  res.send("Hello there!! Cheers !! The server is up and running")
);

// using our routes
app.use("/api/todo", todo);

// listen
app.listen(PORT, () =>
  console.log(`Server is running on http://localhost:${PORT}`)
);

{
  "name": "rest-harper",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "nodemon index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^10.0.0",
    "express": "^4.17.1",
    "harperive": "^2.0.1",
    "nodemon": "^2.0.13"
  }
}

const express = require("express");
const app = express();
app.use(express.json());

const express = require("express");
const app = express();
require("dotenv").config();
 
app.use(express.json());
 
const PORT = process.env.PORT || 5000;
 
app.use((req, res, next) => {
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader(
    "Access-Control-Allow-Methods",
    "GET, POST, OPTIONS, PUT, PATCH, DELETE"
  );
  res.setHeader(
    "Access-Control-Allow-Headers",
    "X-Requested-With,content-type"
  );
  res.setHeader("Access-Control-Allow-Credentials", true);
  next();
});

app.use("/testing", require("./routes/testing.routes.js"));
 
app.use("/students", require("./routes/students.routes.js"));
 
app.listen(process.env.PORT, () => {
  console.log(`App is currently running at http://localhost:${PORT}`);
 
});

// create connection for Harper DB
const harperive = require("harperive");
const configuration = {
  username: process.env.HARPER_INSTANCE_USERNAME,
  password: process.env.HARPER_INSTANCE_PASSWORD,
  schema: process.env.HARPER_INSTANCE_SCHEMA,
  harperHost: process.env.HARPER_HOST_INSTANCE_URL,
};
const db = new harperive.Client(configuration);
module.exports = db;

const controller = require("../controllers/testing.controllers.js");
const router = require("express").Router();
router.get("/appinfo", controller.getAppInfo);
module.exports = router;

const router = require("express").Router();
const controller = require("../controllers/" + "students" + ".controllers");
router
  .get("/", controller.getAllStudent)
  .get("/:id", controller.getOneStudent)
  .post("/", controller.createOneStudent)
  .put("/:id", controller.updateOneStudent)
  .delete("/:id", controller.deleteOneStudent);
module.exports = router;

exports.getAppInfo = (req, res, next) => {
  return res.status(200).json({ "Aviyel CRUD API Testing": "v1.0.0" });
};

const client = require("../util/db");
const DB_SCHEMA = process.env.HARPER_INSTANCE_SCHEMA;
const TABLE = "students";

const client = require("../util/db");
const DB_SCHEMA = process.env.HARPER_INSTANCE_SCHEMA;
const TABLE = "students";

//Get only one student
exports.getOneStudent = async (req, res, next) => {
  try {
    const qry = `SELECT * FROM ${DB_SCHEMA}.${TABLE} WHERE id="${req.params.id}"`;
    const student = await client.query(qry);
    res.json(student);
  } catch (error) {
    console.error("ERROR while fetching student " + "Student:", error);
    return res.status(500).json(error);
  }
};

//Get only one student
exports.getOneStudent = async (req, res, next) => {
  try {
    const qry = `SELECT * FROM ${DB_SCHEMA}.${TABLE} WHERE id="${req.params.id}"`;
    const student = await client.query(qry);
    res.json(student);
  } catch (error) {
    console.error("ERROR while fetching student " + "Student:", error);
    return res.status(500).json(error);
  }
};

//update one student
exports.updateOneStudent = async (req, res, next) => {
  try {
    const updateStudent = await client.update({
      table: TABLE,
      records: [
        {
          id: req.params.id,
          username: req.body.username,
          password: req.body.password,
          rollNumber: req.body.rollNumber,
        },
      ],
    });
    res.json(updateStudent);
  } catch (error) {
    res.status(500).json(error);
  }
};

//Delete one student
exports.deleteOneStudent = async (req, res, next) => {
  try {
    const qry = `DELETE FROM ${DB_SCHEMA}.${TABLE} WHERE id="${req.params.id}"`;
    const deleteStudent = await client.query(qry);
    res.json(deleteStudent);
  } catch (error) {
    res.status(500).json(error);
  }
};

