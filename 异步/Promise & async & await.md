# Promise & async & await

1. 如何使用多个 success 函数？

``` javascript
axios({
    url: '',
}).then((success) => {
    return Promise.reject('reject') // Promise.reject相当于主动抛出一个错误
}, (fail) => {
    console.log('错误')
}).then((success) => {
    // 只有在第一个then是成功时,才会进入第二个then的第一个参数
}, (fail) => {
    // 只要第一个then里有错误(不管是成功参数还是错误参数),就会进入这里第二个then的第二个参数
})
```

- 自己实现 Promise

``` javascript
function ajax(){
    return new Promise((resolve, reject)=>{
        // 代码
        // 如果成功就调用 resolve
        // 如果失败就调用 reject
    })
}

var promise = ajax()
promise.then(successFn, errorFn)
```

2. async(异步) / await(同步)

``` javascript
function buyFruit(){
    return new Promise((resolve, reject)=>{
        // 代码
        // 如果成功就调用 resolve
        // 如果失败就调用 reject
    })
}

var promise = await ajax()
```

``` javascript
async functon fn(){
    var result = await buyFruit()
    return result
}

var r = await fn()
console.log(r)
```