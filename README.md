# Eddigi-feladatok
=============================

- [Java](#java)
- [JavaFx](#javafx)
- [Backend](#backend)
- [Frontend](#frontend)

# java

Egy másik valami.java fileba a classt hozd létre
```
public class Madarak {
    String magyarNev;
    String latinNev;
    int atlagSuly;
    int atlagMagassag;
    int atlagReptav;

    public Madarak(String line) {
        String[] lineArr = line.split(";");
        magyarNev = lineArr[0];
        latinNev = lineArr[1];
        atlagSuly = Integer.parseInt(lineArr[2]);
        atlagMagassag = Integer.parseInt(lineArr[3]);
        atlagReptav = Integer.parseInt(lineArr[4]);
    }
}
```

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

Treemap:

A categ az az ami alapján csinálja a kategóriákat, itt pl a magasság szerint
```
TreeMap<Integer, Integer> madarakMagassaga = new TreeMap<>();
        for (Madarak obj: madarak){
            int categ = obj.getAtlagMagassag();
            if(!madarakMagassaga.containsKey(categ)){
                madarakMagassaga.put(categ, 1);
            }else{
                madarakMagassaga.put(categ, madarakMagassaga.get(categ)+1);
            }
        }
```

Ha valami alapján kikéne íratni a treemapben a dolgokat: 
```
List<String> madarMagas = new ArrayList<>();
        madarakMagassaga.forEach((key, value)->{
            if (value>1){
                madarMagas.add(key+"cm"+" "+ "("+value+")");
            }
        });
        System.out.printf("%s\n", String.join(", ", madarMagas));
```
a .add-nál pluszal add hozzá a cuccokat, a String.join meg megoldja a vesszőzést (valszeg kell majd)
Külön is iderakom azért a String.join-t
```
System.out.printf("%s\n", String.join(", ", madarMagas));
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
