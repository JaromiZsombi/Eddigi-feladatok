# Eddigi-feladatok
=============================

- [Java](#java)
- [JavaFx](#javafx)
- [Backend](#backend)
- [Frontend](#frontend)

# java
# javafx
# backend
```
pnpm init
```
<img width="507" height="279" alt="image" src="https://github.com/user-attachments/assets/69ab7166-e10e-4b7b-832d-663a6f2613ed" />

```
pnpm i express cors mysql2 
```
<img width="549" height="343" alt="image" src="https://github.com/user-attachments/assets/54a04edd-10ad-4cdc-8d12-32ea27d3501d" />

```
"dev":"node index.js",
"type":"module"
```
<img width="540" height="483" alt="image" src="https://github.com/user-attachments/assets/ffb870d9-2716-4613-8741-58bc635b0789" />

# index.js eleje
```
import express from "express";
import cors from "cors";
import mysql from "mysql2/promise";
```
```
let con = await mysql.createConnection({
    host: "localhost",
    port: 3306,
    database: "viragbolt",
    user: "root",
    password: ""
 });
```
# get funkció

```
async function getCategories(req, res) {
    let sql = "select * from kategoriak";
    try {
        const [ json ] = await con.query(sql);
        res.send(json);        
    } catch(err) { res.status(500).send({ error: "Adatbázis hiba!" })}
}
```


 # index.js alja
 ```app.get("/", (req, res) => res.send("<h1>Virágbolt v1.0.0</h1>"));```
 
 többire példa:
 ```
 app.get("/api/categories", getCategories);
 app.put("/api/categories", putCategories);
 app.delete("/api/categories", deleteCategories);
 app.listen(8000, err => console.log(err ? err : "Server on :88"));
 ```
# frontend
