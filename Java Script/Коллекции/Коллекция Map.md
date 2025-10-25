это специальная струкутра данных
чтобы создать нужно в скобках указать матрицу с парами ключей и значений
 
```
const data = Map([
    ["ключ может быть даже числом", true],
    [1, "вот так"]
])
```
 
const data = Map()
data = set("word", "dfnfafr") - динамическое добавление элемента в колекцию
data.delete("word") - точечное удаление элементов
console.log(data.get("word")) - получение данных по ключу
console.log(data.has("name")) - проверка наличя ключа
data.clear() - полная очистка колекции
console.log(data.size) - обращение к длине коллекции
data.keys()
data.entries()       колекция имеет методы обьектов
data.values()         
 
колекция имеет методы обьектов - каждый из этих методов позволяет получить коллекцию Map() в виде перебираемого итерируемого обьекта
чтобы перебрать такой обьект импользуеться цикл for of
 
```
for (let key of data.keys()) {
    console.log(key)
}
 
for (let value of data.values()) {
    console.log(value)
}
 
 
for (let entry of data.entries()) {
    console.log(entry)
}
 
```
у коллекции есть собственный метод forEach
 
```
data.forEach((value , key , map) => {
    console.log(value)
    console.log(key)
    console.log(map)
})
 
```
value - значение текущей пары коллекции
key - ключ
map - ссылка на саму колекцию
 
 
const map = new Map(Object.entries(myObj)) - преоброзование обьекта в колллекцию
const myObj = Object.fromEntries(map) - обратное действие

[[Коллекция Set]]