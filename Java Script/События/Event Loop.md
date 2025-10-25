По другому событийный цикл
Создание простой ассинхронной функции
 
```
const awaitFunc = (callback) => {
    setTimeout(callback, 4)
}
```
 

promise -  специальный обьект надстройка для работы с асинхронным кодом. Имеет три состояния:
состояния:
```
pending - ожидание (исходное состояние)
fullfiled - выполнено успешно, получен результат
rejected - получена ошибка
```
 
основные методы:
```
then() - обрабатывает состояние fuiifiled
catch() - обробатывает состояние rejected
finally() - выполняеться не завивсимо от итогового состояния
```
 
```
const prom = new Promise((fullfill, reject) => {
    console.log("Нчальное состояние pending")
    setTimeout(() => {
        if (Math.random() > 0,5) {
            fullfill("Завершено fuflfilled")
        } else {
            reject("Завершено с ошибкой rejected")
        }
    }, 3000)
})
prom
.then((successData) => {console.log("Получены данные:", successData)})
.catch((errerData) => {console.log("Получены данные:", errerData)})
.finally(() => {console.log("этот код выполниться в любом случае")})
 
```
async - пишеться в начале функции и гарантирует что функция вернет promise
 
```
async function getSomething() {} при FUNCTION DECLORATION
const getSomething = async () => {} при ARROW FUNCTION
 
const getSomething = async () => {
    return "dfnfafr"
}
```
вызов async функции
 
```
getSomething().then((something) => {
    console.log(something)
})
```