# Picker

> 公司项目开发中经常用到的一个组件, 起先也用到了如Mint UI等第三方组件库, 但是产品需求复杂, picker滑动的时间段也是从后端获取, 进行计算的, 所以自己结合不同的业务需求

## 介绍

原生 Javascript 实现移动端 Picker 组件

## 效果图：

![演示图](https://raw.githubusercontent.com/mqyqingfeng/waterfall/master/demonstration.gif)

源码地址：

[https://github.com/peng-yin/Picker](https://github.com/peng-yin/Picker)

## 依赖

原生 JavaScript 实现，无依赖。

## 大小

整个组件的js只用到了300多行实现， 压缩后 5KB，gzip 压缩后更小。

## 兼容

滑动动画流畅, 在安卓,ios下未出现兼容问题

## 下载

```js
https://github.com/peng-yin/Picker.git
```

## 使用

```html
<script src="path/picker.js"></script>
```

或者

```js
import picker from 'path/picker.js'
```

## 示例

```js
var $picker = new Picker({
    el: '.date-box',
    autoHide: true,
    itemHeight: 36,
    data: '',
    onChange: res => {
        switch (res.index) {
            case 0:
                selectYear = res.value;
            break;
            case 1:
                selectMonth = res.value;
            break;
            case 2:
                selectDay = res.value;
            break;
        }
    },
    onChangeEnd: res => {
        let _day = [], maxDay = new Date(selectYear, selectMonth, 0).getDate();
        for (var i = 0; i <=maxDay; i++) {
            _day.push({
                title: i + ' 日',
                value: i
            });
        }
        if (res.index === 0 || res.index === 1) {
            $picker.setItem({
                index: 2,
                data: _day,
                default: selectDay < maxDay ? selectDay : maxDay
            })
        }
    }
})
```

## API

### 初始化

```js
var $picker = new Picker(options);
```

### options

**container**

必填，指定Picker容器的 selector

**autoHide**

必填，指定瀑布流添加的区块的 selector

**loader**

必填，指定瀑布流加载时的 loading 的 selector

**autoHide**

默认值为 `false`，pins 上下间隔的距离

**gapWidth**

默认值为 `20`，pins 左右间隔的距离

**pinWidth**

默认值为 `216`，pins 的宽度为 216px

**threshold**

默认值为 `100`，当距离底部还是有 100px 的时候就开始加载

### 事件绑定

当需要加载新的数据时，会触发 load 事件

```js
waterfall.on("load", function(){
    // 模拟数据加载
    setTimeout(function(){
        // 注意当加载新的 pins 的时候，需要调用 waterfall.append 函数
        waterfall.append(htmlStr, selector)
    }, 1000)
})
```

### 方法

**append**

该函数传入两个参数：

1.htmlStr 类似于

```js
'<div class="pin"><img class="img"> ... </div>'
```

需要注意每个 pin 需要添加与 options.pins 一致的类名，图片元素需要添加类名，然后作为选择符，传入第二个参数

2. selector

图片的选择符，以上面的例子为例，应该传入

```js
waterfall.append(htmlStr, '.img')
```

这是为了根据选择符筛选出要加载的图片，判断所有的图片都有了高度之后，才会添加进瀑布流中。


## TodoList
1. 代码测试，压缩 上传npm
