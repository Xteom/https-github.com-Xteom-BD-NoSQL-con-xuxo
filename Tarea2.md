# Tarea 2

##### Mateo De La Roche Macías
##### 190748

###### Ejercicios 4 al 7

4. Cómo podemos saber si los tuiteros hispanohablantes interactúan más en las noches? (Entre 19 y 23)
```javascript
db.tweets.aggregate([
   {$lookup: {from:"primarydialects","localField":"_id","foreignField":"lang","as":"language"}},
   {$match: {"user.lang": 'es', "created_at": /^[A-Z]+[a-z]{1,2}\s+[A-Z]+[a-z]{1,2}\s+[0-9]{1,2}\s+([1]+[9]|[2]+[0-3])+:+[0-5]+[0-9]+:+[0-5]+[0-9].........../}},
  {$group: {_id:"$user.lang","cuenta":{$count:{}}}}
 ])
 db.tweets.aggregate([
    {$lookup: {from:"primarydialects","localField":"_id","foreignField":"lang","as":"language"}},
    {$match: {"user.lang": 'es', "created_at": /^[A-Z]+[a-z]{1,2}\s+[A-Z]+[a-z]{1,2}\s+[0-9]{1,2}\s+([0]+[1-9]|[1]+[0-8])+:+[0-5]+[0-9]+:+[0-5]+[0-9].........../}},
   {$group: {_id:"$user.lang","cuenta":{$count:{}}}}
  ])
```
>Al correr las dos queries podemos ver que hay más twitteros en las noches
5. Cómo podemos saber de dónde son los tuiteros que más tiempo tienen en la plataforma?

 ```javascript
db.tweets.aggregate([
  {$addFields: {"user.created_at":{"$toDate":"$user.created_at"}}},
  {$project:{"user.created_at":1,"user.location":1,"user.time_zone":1}},
  {$sort:{"user.created_at":1}}
  ])
```

6. En intervalos de 7:00:00pm a 6:59:59am y de 7:00:00am a 6:59:59pm, de qué paises la mayoría de los tuits?
```javascript
db.tweets.aggregate([
  {$match: {"created_at": /^[A-Z]+[a-z]{1,2}\s+[A-Z]+[a-z]{1,2}\s+[0-9]{1,2}\s+([1]+[9]|[2]+[0-3]|[0]+[0-6])+:+[0-5]+[0-9]+:+[0-5]+[0-9].........../}},
  {$group:{_id:{"zona":"$user.time_zone"},"cuenta":{$count:{}}}},
  {$sort: {"cuenta":-1}}
 ])

 db.tweets.aggregate([
   {$match: {"created_at": /^[A-Z]+[a-z]{1,2}\s+[A-Z]+[a-z]{1,2}\s+[0-9]{1,2}\s+([0]+[7-9]|[1]+[0-8])+:+[0-5]+[0-9]+:+[0-5]+[0-9].........../}},
   {$group:{_id:{"zona":"$user.time_zone"},"cuenta":{$count:{}}}},
   {$sort: {"cuenta":-1}}
  ])
```
7. De qué país son los tuiteros más famosos de nuestra colección?
```javascript
db.tweets.aggregate([
  {$project:{"user.time_zone":1,"user.friends_count":1}},
  {$sort:{"user.friends_count":-1}},
  {$limit: 5}
  ])
```
