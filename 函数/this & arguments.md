# this & arguments

- 重要: **[this 就是 call 的第一个参数！call 的其他参数统称为 arguments](https://zhuanlan.zhihu.com/p/23804247)**

- this 是隐藏的第一个参数，且一般是对象（如果不是对象，就显得很没有意义了）

  ``` javascript
  function f() {
      console.log(this)
      console.log(arguments)
  }
  f.call() // window,因为call()没有传参数,所以this默认是window
  f.call({name:'frank'}) // {name: 'frank'}, []
  f.call({name:'frank'},1) // {name: 'frank'}, [1]
  f.call({name:'frank'},1,2) // {name: 'frank'}, [1,2]
  ```

- this 为什么得是对象, 因为 this 就是函数与对象之间的羁绊

  ``` javascript
   var person = {
          name: 'frank',
          sayHi: function(person) {
              console.log('Hi, I am ' + person.name)
          },
          sayBye: function(person){
              console.log('Bye, I am ' + person.name)
          },
          say: function(person, word){
              console.log(word + ', I am ' + person.name)
          }
      }
      person.sayHi(person)
      person.sayBye(person)
      person.say(person, 'How are you')
      // 如果没有this,那么代码就得像上面的写法,很麻烦

      // 如果要改成这样的写法
      person.sayHi()
      person.sayBye()
      person.say('How are you')

      // 那么源代码就要改了
      var person = {
          name: 'frank',
          sayHi: function() {
              console.log('Hi, I am ' + this.name)
          },
          sayBye: function(){
              console.log('Bye, I am ' + this.name)
          },
          say: function(word){
              console.log(word + ', I am ' + this.name)
          }
      }
      // 如果你不想吃语法糖,可以这样写:
      person.sayHi.call(person)
      person.sayBye.call(person)
      person.say.call(person, 'How are you')

      // 还是回到那句话：this 是 call 的第一个参数
      // this 是参数，所以，只有在调用的时候才能确定
      person.sayHi.call({name:'haha'})  // 这时 sayHi 里面的 this 就不是 person 了
      // this 真的很不靠谱

      // 两种不同的写法,会有不同的结果
      var fn = person.sayHi
      person.sayHi() // this === person,这是因为this指向 .sayHi() 前面的对象
      fn()  // this === window,这是因为fn()前没有对象,this不知道该指向谁所以默认指向window
  ```

如果你用call()调用函数,想让this指向window并且要传参数,可以这样写:

``` javascript
function sum(x, y) {
    return x + y
}
sum.call(undefined, 1, 2)
```

- call / apply

fn.call(asThis, p1,p2) 是函数的正常调用方式
当你不确定参数的个数时，就使用 apply
fn.apply(asThis, params)

``` javascript
var arr = [1, 2, 3, 4, 5]
function sumAll() {
    var n = 0
    for(var i = 0; i < arguments.length; i++) {
        n += arguments[i]
    }
    return n
}

sumAll.apply(undefined, arr)
```