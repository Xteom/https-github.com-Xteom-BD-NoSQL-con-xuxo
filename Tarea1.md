# Tarea 1

##### Mateo De La Roche Macías
##### 190748

###### Ejercicios 12 al 32

12. Escribe una función find() para encontrar los restaurantes que no preparan ninguna cocina del continente americano y lograron una puntuación superior a 70 y se ubicaron en la longitud inferior a -65.754168.
>db.restaurants.find({"cuisine":{$not:/American/},"grades.score":{$gt:70},"address.coord.0":{$lt:-65.754168}},{"cuisine":1,"grades":1,"address.coord":1})


13. Escribe una función find() para encontrar los restaurantes que no preparan ninguna cocina del continente americano y obtuvieron una calificación de 'A' que no pertenece al distrito de Brooklyn. El documento debe mostrarse según la cocina en orden descendente.
>db.restaurants.find({"cuisine":{$not:/(American)/}, "grades.grade":'A', "borough":{$ne:'Brooklyn'}},{"cuisine":1, "grades.grade":1, "borough":1}).sort({"cuisine":-1})


14. Escribe una función find() para encontrar el ID del restaurante, el nombre, el municipio y la cocina de aquellos restaurantes que contienen 'Wil' como las primeras tres letras de su nombre.
>db.restaurants.find({"name":/^Wil/},{"restaurant_id":1, "name":1, "borough":1, "cuisine":1, "_id":0})


15. Escribe una función find() para encontrar el ID del restaurante, el nombre, el municipio y la cocina de aquellos restaurantes que contienen "ces" como las últimas tres letras de su nombre.
>db.restaurants.find({"name":/ces$/},{"restaurant_id":1, "name":1, "borough":1, "cuisine":1,"_id":0})


16. Escribe una función find() para encontrar el ID del restaurante, el nombre, el municipio y la cocina de aquellos restaurantes que contienen 'Reg' como tres letras en algún lugar de su nombre.
>db.restaurants.find({"name":/Reg/},{"restaurant_id":1, "name":1, "borough":1, "cuisine":1,"_id":0})


17. Escribe una función find() para encontrar los restaurantes que pertenecen al municipio del Bronx y que prepararon platos estadounidenses o chinos.
>db.restaurants.find({"borough":'Bronx', "cuisine":/^(American $|Hamburgers$|Chinese$)/},{"borough":1, "cuisine":1})


18. Escribe una función find() para encontrar la identificación del restaurante, el nombre, el municipio y la cocina de los restaurantes que pertenecen al municipio de Staten Island o Queens o Bronx or Brooklyn.
>db.restaurants.find({"borough":/^(Staten Island$|Queens|Bronx|Brooklyn)/},{"restaurant_id":1, "name":1, "borough":1, "cuisine":1,"_id":0})



19. Escribe una función find() para encontrar el ID del restaurante, el nombre, el municipio y la cocina de aquellos restaurantes que no pertenecen al municipio de Staten Island o Queens o Bronx or Brooklyn.
>db.restaurants.find({"borough":{$not:/^(Staten Island$|Queens|Bronx|Brooklyn)/}},{"restaurant_id":1, "name":1, "borough":1, "cuisine":1,"_id":0})


20. Escribe una función find() para encontrar el ID del restaurante, el nombre, el municipio y la cocina de aquellos restaurantes que obtuvieron una puntuación que no sea superior a 10.
>db.restaurants.find({"grades.score":{$lt:10}},{"restaurant_id":1,"name":1,"borough":1,"cuisine":1,"grades.score":1,"_id":0})


21. Escribe una función find() para encontrar el ID del restaurante, el nombre, el municipio y la cocina de aquellos restaurantes que prepararon platos excepto 'Americano' y 'Chinees' o el nombre del restaurante comienza con la letra 'Wil'.
>db.restaurants.find({"cuisine":{$not:/^(American|Chinese)/},"name":{$not:/^Wil/}},{"restaurant_id":1,"name":1,"borough":1,"cuisine":1,"_id":0})


22. Escribe una función find() para encontrar el ID del restaurante, el nombre y las calificaciones de los restaurantes que obtuvieron una calificación de "A" y obtuvieron una puntuación de 11 en un ISODate "2014-08-11T00: 00: 00Z" entre muchas de las fechas de la encuesta.
>db.restaurants.find({"grades":{$elemMatch:{"grade":'A',"score":11,"date":ISODate("2014-08-11T00:00:00.000Z")}}},{"restaurant_id":1,"name":1,"grades":1,"_id":0})


23. Escribe una función find() para encontrar el ID del restaurante, el nombre y las calificaciones de aquellos restaurantes donde el segundo elemento de la matriz de calificaciones contiene una calificación de "A" y una puntuación de 9 en un ISODate "2014-08-11T00: 00: 00Z".
>db.restaurants.find({"grades.1.grade":'A',"grades.1.date":ISODate("2014-08-11T00:00:00.000Z"),"grades.1.score":9},{"restaurant_id":1,"name":1,"grades":1,"_id":0})


24. Escribe una función find() para encontrar el ID del restaurante, el nombre, la dirección y la ubicación geográfica para aquellos restaurantes donde el segundo elemento de la matriz de coordenadas contiene un valor que sea más de 42 y hasta 52 .
>db.restaurants.find({"address.coord.1":{$gte:42,$lte:52}},{"restaurant_id":1,"name":1,"address":1,"_id":0})


25. Escribe una función find() para organizar el nombre de los restaurantes en orden ascendente junto con todas las columnas.
>db.restaurants.find().sort({"name":1})


26. Escribe una función find() para organizar el nombre de los restaurantes en orden descendente junto con todas las columnas.
>db.restaurants.find().sort({"name":-1})


27. Escribe una función find() para organizar el nombre de la cocina en orden ascendente y para ese mismo distrito de cocina debe estar en orden descendente.
>db.restaurants.find().sort({"cuisine":1,"borough":-1})


28. Escribe una función find() para saber si todas las direcciones contienen la calle o no.
>db.restaurants.find({"address.street":{$exists:true}},{"address.street":1})


29. Escribe una función find() que seleccionará todos los documentos de la colección de restaurantes donde el valor del campo coord es Double.
> db.restaurants.find({"address.coord":{$type:1}})


30. Escribe una función find() que seleccionará el ID del restaurante, el nombre y las calificaciones para esos restaurantes que devuelve 0 como resto después de dividir la puntuación por 7.
>db.restaurants.find({"grades.score":{$mod:[7,0]}},{"restaurante_id":1,"name":1,"grades":1,"_id":0})


31. Escribe una función find() para encontrar el nombre del restaurante, el municipio, la longitud y la altitud y la cocina de aquellos restaurantes que contienen "mon" como tres letras en algún lugar de su nombre.
>db.restaurants.find({"name":/mon/},{"name":1,"borough":1,"address.coord":1,"cuisine":1,"_id":0})


32. Escribe una función find() para encontrar el nombre del restaurante, el distrito, la longitud y la latitud y la cocina de aquellos restaurantes que contienen 'Mad' como las primeras tres letras de su nombre.
>db.restaurants.find({"name":/^Mad/},{"name":1,"borough":1,"address.coord":1,"cuisine":1,"_id":0})



```
