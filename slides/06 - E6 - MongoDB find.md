# MongoDB  - Esercitazione (Find)

## Restaurants
1. Visualizzare tutti i ristoranti. 

```mongodb
db.restaurants.find();
```

2. Visualizzare quartiere (borough) e tipo di cucina (cuisine) di tutti i ristoranti. 

```mongodb
db.restaurants.find({}, { borough: 1, cuisine: 1 });
```

3. Visualizzare quartiere (borough) e tipo di cucina (cuisine) di tutti i ristoranti, ma senza _id. 

```mongodb
db.restaurants.find({}, { borough: 1, cuisine: 1, _id : 0 });
```

4. Visualizzare quartiere (borough), tipo di cucina (cuisine) e via (address.street) di tutti i ristoranti. 

```mongodb
db.restaurants.find({}, { borough: 1, cuisine: 1, "address.street": 1 ,_id : 0 });
```

5. Visualizzare iI ristorante il cui zipcode è 11225

```mongodb
db.restaurants.find({ "address.zipcode": "11225" });
```

6. Visualizzare i ristoranti il cui tipo di cucina è Hamburgers 

```mongodb
db.restaurants.find({ "cuisine": "Hamburgers" });
```

7. Visualizzare i ristoranti il cui tipo di cucina NON è Hamburgers 

```mongodb
db.restaurants.find({ "cuisine" : { "$nin" : ["Hamburgers"] }});
```

8. Visualizzare i ristoranti il cui tipo di cucina è tra Hamburgers, Bakery o Irish 

```mongodb
db.restaurants.find({ "cuisine" : { "$in" : ["Hamburgers", "Bakery", "Irish" ] }});
```

9. Visualizzare i ristoranti il cui tipo di cucina NON è tra Hamburgers, Bakery o Irish 

```mongodb
db.restaurants.find({ "cuisine" : { "$nin" : ["Hamburgers", "Bakery", "Irish" ] }});
```

10. Visualizzare i ristoranti il cui tipo di cucina non esiste 

```mongodb
db.restaurants.find({ "cuisine" : { "$exists" : false }});
```

## Yelp business
11. Visualizzare tutti i business che hanno ricevuto almeno 10 recensioni (review_count) E si trovano in Arizona o in Nevada (state = NV o AZ) 

```mongodb
db.getCollection("yelp-business").find({ review_count: { $gte: 10 }, $or: [{ state: "NV" }, { state: "AZ" }] })
```

12. Visualizzare tutti i business che hanno ricevuto almeno 10 recensioni (review_count) O si trovano in Arizona o in Nevada (state = NV o AZ) 

```mongodb
db.getCollection("yelp-business").find( { $or: [{ review_count: { $gte: 10 }}, { $or: [{ state: "NV" }, { state: "AZ" }]}] })
```

13. Visualizzare tutti i business che hanno Grocery tra le categorie 

```mongodb
db.getCollection("yelp-business").find( { categories: "Grocery" })
```

14. Visualizzare tutti i business che hanno Grocery E Food tra le categorie 

```mongodb
db.getCollection("yelp-business").find( { categories: { $all : ["Grocery", "Food"] }})
```

15. Visualizzare tutti i business che hanno Grocery O Food tra le categorie 

```mongodb
db.getCollection("yelp-business").find( { categories: { $in : ["Grocery", "Food"] }})
```

16. Visualizzare tutti i business che hanno SOLAMENTE Grocery E Food tra le categorie 

```mongodb
db.getCollection("yelp-business").find( { categories: ["Grocery", "Food"] })
```

17. Visualizzare tutti i business che hanno 5 categorie 

```mongodb
db.getCollection("yelp-business").find({ categories: { $size: 3 }})
```

18. Visualizzare tutti i business che hanno 5 categorie e la quinta categoria è Food 

```mongodb
db.getCollection("yelp-business").find({ categories: { $size: 5 }, "categories.4": "Food" })
```

19. Visualizzare le prime due categorie di ogni business 

```mongodb
db.getCollection("yelp-business").find({}, { categories: { $slice: 2 }})
```

20. Visualizzare unicamente le categorie dei business del Nevada 

```mongodb
db.getCollection("yelp-business").find({ state: "NV" }, { categories: 1 })
```

21. Visualizzare i valori distinti del campo city

```mongodb
db.getCollection("yelp-business").distinct("city")
```

22. Visualizzare i valori distinti del campo city nello stato del Nevada

```mongodb
db.getCollection("yelp-business").distinct("city", { state: "NV" })
```

23. Visualizzare i valori distinti dell’array categories

```mongodb
db.getCollection("yelp-business").distinct("categories")
```

## Games

24. Visualizzare le partite disputate nel 2010. (1239 risultati). Formato data: "anno-mese-giorno"

25. Visualizzare le partite in cui una delle squadre ha totalizzato almeno 160 punti (6 risultati)

26. Visualizzare le partite in cui la squadra di casa ha perso (12197 risultati)

27. Visualizzare le partite in cui ha giocato Michael Jordan (990 risultati)

28. Visualizzare le partite in cui Michael Jordan ha segnato più di 60 punti (4 risultati)

29. Visualizzare le prime 10 partite memorizzate nella collection (10 risultati)

30. Visualizzare le prime 10 partite in ordine di data (10 risultati)

31. Visualizzare le prime 10 partite del 2010 in ordine di data (10 risultati)

32. Visualizzare le seconde 10 partite (dalla 11°) del 2010 in ordine di data (10 risultati)

## Esercizi aggiuntivi

33. [Restaurants] Visualizzare i ristoranti che hanno ricevuto almeno un punteggio (grades.score) maggiore di 10

34. [Restaurants] Visualizzare i ristoranti che hanno ricevuto almeno un punteggio (grades.score) maggiore di 10 nel 2014

35. [Yelpbusiness] Contare i business di categoria Yoga che hanno ricevuto almeno 4 di punteggio (stars) e che sono aperti (is_open=1)

36. [Games] Visualizzare le partite in cui la squadra di casa ha perso pur totalizzando più di 120 punti

37. [Games] Visualizzare l’elenco distinto di date in cui una delle squadre ha totalizzato almeno 160 punti

38. [Games] Visualizzare le partite in cui una delle due squadre ha sbagliato tutti i tiri liberi (box.team.ft=0) pur avendone provati almeno 2 (box.team.fta>=2)