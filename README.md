# How to install mern and setup completely with mongodb

At first run that cmd

```
npm init -y
```

Then install this all tools

```
npm install express mongoose cors dotenv
```

Then install this

```
npm install --save-dev nodemon
```

Then make file in root project folder in `server.js` and here paste it

```
const express = require("express");
const cors = require("cors");
const dotenv = require("dotenv");
const connectDB = require("./configs/db");

dotenv.config();
const app = express();

app.use(express.json());
app.use(cors());

connectDB();

app.get("/", (req, res) => res.send("API Running"));

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

Then make `configs/db.js` and paste there

```
const mongoose = require("mongoose");

const connectDB = async () => {
   await mongoose
      .connect(process.env.MONGO_URI)
      .then(() => console.log("MongoDB Connected"))
      .catch((err) => console.log(err));
};

module.exports = connectDB;
```

Then make `.env` and paste there it

```
MONGO_URI=mongodb://localhost:27017/lipys_app
```

And then go to `package.json` file then paste it

```
 "scripts": {
      "start": "node server.js",
      "dev": "nodemon server.js"
   },
```

Finaly Backend App is ready and run the app

```
npm run dev
```

or

```
npm start
```
