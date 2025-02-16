
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
Then make file in root project folder in `server.js` and here paste it and here using 2 methods for importer like `const express = require("express");` or `import express from "express";` any one method using in all project files.
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
## And for post method two type post request supported here
1. First Type when use file upload this time use FormData like 
```
const create_design = async () => {
      const image = await htmlToImage.toBlob(ref.current);
      const design = JSON.stringify(obj);
      if (image) {
         const formData = new FormData();
         formData.append("design", design);
         formData.append("image", image);
         try {
            setLoader(true);
            const { data } = await api.post(
               "/api/create-user-design",
               formData,
               {
                  headers: {
                     "Content-Type": "multipart/form-data",
                  },
               }
            );
            console.log(data)
         } catch (error) {
            console.error(error);
         }
      }
   };
```
2. Second Type post method use request type `json` when not using any file in post this time using 
```
const image = await htmlToImage.toBlob(ref.current);
      const design = JSON.stringify(obj);
      if (image) {
         const formData = {
            name: "MD Anwar",
            email: "example@gmail.com",
            password: "01234567899"
         }
         try {
            setLoader(true);
            const { data } = await api.post(
               "/api/create-user-design",
               formData
            );
            console.log(data)
         } catch (error) {
            console.error(error);
         }
      }
   };
```

## And when using postman test mern api this time using two method for post request
1. First Method when inert any file this time used form-data in body in postman

![App Screenshot](https://media-hosting.imagekit.io//4c119d7d1b964432/Screenshot%20(5).png?Expires=1834276518&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=xev2scp3Bajdfc6lO4W0Ny6fLBXlUobRMyl9rpwiv3POmAXmb7Gw9V-vtmLDBNEobEnaBAstf2J3Kc1gqZeIXO5drRieshg9djJa2KcVkbzNifJVAn3jmncViKabzQnemiCkOC4VAjEGDos14kwJhJ3WtKdGMBbHfCIxNqR-yaMsmZyFhLPtWRnal~yWWu~ZnSypjqbEse0xpxj7Gj553x-A4x1ncrQHLeVfpVPC2rHn1Ja-by-yYG0D4PvFYv8cN6yA-3Y~CUXrmQ4f-YvsIs1P9MAbplDqpdl35kj5aZcOKN9phLuWeArefDYNxgnfVU2OePp2mt8LBh2ThqrLEg__)

2. Second method when not using any file this time using `json` type body data in postman like

![App Screenshot](https://media-hosting.imagekit.io//72a47905a7454aa5/Screenshot%20(6).png?Expires=1834276889&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=BZGzbmwFD7Br-nKENgRor4Plu9V1wTuBApOkiec~-V8yTvb7B0bs60AKNUrqBtGlI9aS1XdmIz14aRH2AEh88IKdNuHnFIzYv5aQDmcc4-iNbrQylI1E6E3aoklhoaC8803Q1C1NvN3-atxwBV5KtK-XSZ-dsaGWZXZVtGakjv9~PcYuCSGuQJ4TiwjICK1re2X8Dcb~laToJj9iFnOAykup8dcSk91hyhIHNSXQ4KM9Cf9rEvOdKlMKoUAIP7Ld7SbWYWCNL-kERTdqONeYISDXavs-FWTrgv5hjuoZR4ZaGKaRMUKL96c66HpmJofPJXFnsVJWzEy3yHrKGY3Pjg__)
