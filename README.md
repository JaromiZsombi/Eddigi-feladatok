# Eddigi-feladatok
=============================

- [Java](#java)
- [JavaFx](#javafx)
- [Backend](#backend)
- [Frontend](#frontend)

# java

A lista nevét, attribútumát át kell írni, illetve a soutot is, meg ha az első sorban nem adat van, csak akkor kell a beolvasas.nextLine

```
List<Madarak> madarak = new ArrayList<>();
        try(Scanner beolvasas = new Scanner(new File("madarak.csv"))){
            beolvasas.nextLine();
            while (beolvasas.hasNextLine()){
                madarak.add(new Madarak(beolvasas.nextLine()));
            }
        }catch (Exception e){
            System.out.println("Hiba: "+e.getMessage());
        }
        System.out.printf("1) A madarak.csv fájlból %d madár adata beolvasva\n", madarak.size());
```

# javafx
# backend
```
pnpm init
```
<img width="507" height="279" alt="image" src="https://github.com/user-attachments/assets/69ab7166-e10e-4b7b-832d-663a6f2613ed" />

```
pnpm i express cors mysql2 
```
<img width="539" height="337" alt="image" src="https://github.com/user-attachments/assets/d25a652a-03bf-4ffc-ba25-28b9fa52eabb" />

```
"type":"module",
"dev": "node --watch index.js"
```
<img width="509" height="436" alt="image" src="https://github.com/user-attachments/assets/dcdb1fed-ba15-434f-8c08-b4654861ed57" />


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
