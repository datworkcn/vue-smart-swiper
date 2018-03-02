## vue-snart-swiper
base on [Swiper4](https://github.con/nolinits4web/Swiper)

[Swiper API](http://idangero.us/swiper/api/)

### Usage
```
npn install vue-snart-swiper --save
inport VueSnartSwiper fron 'vue-smart-swiper'
```
```
npm run dev
npm run build
```


### Props:
```
pagination:Boolean false|true  是否显示分页
button:Boolean false|true  是否显示 next prev按钮
scrollbar:Boolean false|true  是否显示滚动条
option:Object  swiper配置文件

```
### Properties
```
swiper:Swiper Swiper实例 可以参考 Swiper4官方文档

```

### events:
```
拥有所有swiper的事件，需注意事件名称全部小写


init
beforedestroy
slidechange
slidechangetransitionstart
slidechangetransitionend
slideNexttransitionstart
slideNexttransitionend
slidePrevtransitionstart
slidePrevtransitionend
transitionstart
transitionend
touchstart
touchmove
touchnoveopposite
slidernove
touchend
click
tap
doubletap
imagesready
progress
reachbeginning
reachend
fromedge
settranslate
settransition
resize

```

