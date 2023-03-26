## Домашнее задание

Необходимо:
* установить MongoDB одним из способов: ВМ, докер;
* заполнить данными;
* написать несколько запросов на выборку и обновление данных.

Для работы с MongoDB использовал официальный docker образ mongo и развернул его через docker-compose.
После запуска контейнера подключился к нему:
```
docker exec -it 3mongodb-mongo-1 /bin/bash
```
Далее подключился к самой mongo:
```
mongosh --port 27017 -u "root" -p "example" --authenticationDatabase "admin"
```
Результат:
```
Current Mongosh Log ID: 64204a088904e16b66338288
Connecting to:          mongodb://<credentials>@127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&authSource=admin&appName=mongosh+1.8.0
Using MongoDB:          6.0.5
Using Mongosh:          1.8.0
```
Создаем новую БД:
```
use primer
```
Результат:
```
switched to db primer
```
Создаем новую коллекцию:
```
db.createCollection('cars')
```
Результат:
```
{ ok: 1 }
```
Добавляем данные:
```
db.cars.insertMany( [
{ _id: 1, brand: "BMW", model: "X5", year: 2015 },
{ _id: 2, brand: "Audi", model: "Q3", year: 2015 },
{ _id: 3, brand: "BMW", model: "M5", year: 2003 },
{ _id: 4, brand: "KIA", model: "Rio", year: 2003 },
{ _id: 5, brand: "BMW", model: "Z4", year: 2015 }
] )
```
Результат:
```
{
  acknowledged: true,
  insertedIds: { '0': 1, '1': 2, '2': 3, '3': 4, '4': 5 }
}
```
Найдём все марки авто BMW:
```
db.cars.find( {"brand": "BMW"} )
```
Результат:
```
[
  { _id: 1, brand: 'BMW', model: 'X5', year: 2015 },
  { _id: 3, brand: 'BMW', model: 'M5', year: 2003 },
  { _id: 5, brand: 'BMW', model: 'Z4', year: 2015 }
]
```
Найдём все авто выпущенные после 2005 года:
```
db.cars.find( {"year": {$gt: 2005}} )
```
Результат:
```
[
  { _id: 1, brand: 'BMW', model: 'X5', year: 2015 },
  { _id: 2, brand: 'Audi', model: 'Q3', year: 2015 },
  { _id: 5, brand: 'BMW', model: 'Z4', year: 2015 }
]
```
