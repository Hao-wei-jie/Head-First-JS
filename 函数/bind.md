# bind

- call 和 apply 是直接调用函数，而 bind 则是返回一个新函数（并没有调用原来的函数），这个新函数会 call 原来的函数，call 的参数由你指定。

``` javascript
// 不使用bind的写法
var view = {
    element: 'div',
    bindEvent: function() {
        var _this = this
        return this.element.onclick = function() {
            console.log(this)  // window
            console.log(_this) // view
            _this.onClick()    // 这里想要在view.element上绑定,但直接使用this会指向window,所以在外面把this保存成_this,再在里面使用
        }
    },
    onClick: function() {
        console.log(this) // view
    }
}

var onClick = view.bindEvent()
onClick()

// bind的写法
var view = {
    element: 'div',
    bindEvent: function() {
        return this.element.onclick = this.onClick.bind(this)
        // 使用bind等同于返回了一个新函数:
        // function() {
        //     this.onClick.call(this)
        // }
    },
    onClick: function() {
        console.log(this) // view
    }
}

var onClick = view.bindEvent()
onClick()
```