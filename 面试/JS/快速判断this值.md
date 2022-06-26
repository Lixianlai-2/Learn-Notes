## 快速判断this值

#### 前置条件

想要得到this，那么我们需要调用获取this值的函数，如下面的fn1

```
function fn1() {
	console.log(this)
}

fn1(); // window
```

#### 判断依据

在哪里面调用的获取this值的函数（获取this值的函数的外面第一层处于哪里）

#### 四种情况

##### 在全局环境下调用获取this值的函数

- 返回undefined
- this值在非严格模式下转化为window对象

```
      let obj = {
        fn1() {
          function fn2() {
            console.log(this);
          }
          fn2();
        },
      };

      obj.fn1();
```

- 在函数`fn1`中调用的`fn2`，非严格模式，那么返回window

##### 在对象中调用获取this值的函数

- 需要函数外面第一层就是对象
- 那么this值就是这个对象

```
var obj = {
  foo: function(){
    console.log(this)
  }
}

obj.foo() 
```

- 在对象中调用，那么this值就是obj这个对象

##### 在函数中调用获取this值的函数

- 比如对象中函数里面嵌套函数得到this，那么就返回undefiend
- this值然后非严格模式下转化为window

```
var obj = {
  foo: function(){
    console.log(this)
  }
}

var bar = obj.foo
bar()
```

- bar是一个普通函数，在全局环境下调用，返回的this值是window

##### 如果获取this值的是箭头函数，那么this就是外面第一层的this

```
      let obj = {
        fn1() {
          let fn2 = () => {
            console.log(this);
          };
          fn2();
        },
      };

      obj.fn1();
```

- fn2是箭头函数，那么它的this就是外面第一层的this，而外面第一层的this就是obj，所以这里的this值就是obj

```
    let obj = {
        fn1: () => {
          let fn2 = () => {
            console.log(this);
          };
          fn2();
        },
      };

      obj.fn1();
```

- fn2是箭头函数，那么它的this就是外面第一层的this，而这时外面的fn1也是箭头函数，那么它会无视obj对象，这时的this值就是undefined，在非严格模式下变成window



