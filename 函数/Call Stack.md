# Call Stack

Stack: 栈(是一种数据结构,先进后出,跟队列相反)

``` javascript
// 普通调用 1+1+1
function a() {
    console.log('a')
    return 'a'
}

function b() {
    console.log('b')
    return 'b'
}

function c() {
    console.log('c')
    return 'c'
}

a()
b()
c()

// 以上代码执行结果是:
// a
// b
// c
// "c"
```

``` javascript
// 嵌套调用 1>2>3
function a(){
    console.log('a1')
    b()
    console.log('a2')
  return 'a'  
}
function b(){
    console.log('b1')
    c()
    console.log('b2')
    return 'b'
}
function c(){
    console.log('c')
    return 'c'
}
a()
console.log('end')

// 执行结果:
// a1
// b1
// c
// b2
// a2
// end

// 执行顺序:
// 1. 先执行a函数
// 2. 进入a函数
// 3. 打印a1
// 4. 进入b函数
// 5. 打印b1
// 6. 进入c函数
// 7. 打印c
// 8. 返回'c'到b函数, c函数执行完毕
// 9. b函数继续执行,打印b2
// 10. 返回'b'到a函数, b函数执行完毕
// 11. a函数继续执行,打印a2
// 12. 返回'a', a函数执行完毕
// 13. 打印end
```

``` javascript
// 递归
function fab(n){
    console.log('start calc fab '+ n)
    if(n>=3){
        return fab(n-1) + fab(n-2)
    }else{
        return 1
    }
}

fab(5)
```