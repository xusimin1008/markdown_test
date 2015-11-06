### vue 问题 ###
1. component中的replace作用
2. 

### vue 记录 ###
1. 要确保在初始化根实例之前注册了组件

### Vue data 内属性的添加和删除 ###

```
   var data1 = {
      msg: 'hello',
      attrs: {
         a: 1,
         b: 2,
      }
   }
   var vm  = new Vue({
      el: '#',
      data: data1,
   });
   更新属性：
   受 ES5 的限制，Vue.js 不能检测到对象属性的添加或删除。因为 Vue.js 在初始化实例时将属性转为 getter/setter，所以属性必须在 data 对象上才能让 Vue.js 转换它，才能让它是响应的。
   vm.$set('attrs.c', 3);
   Vue.set(data1.attrs, 'c', 4);
   Vue.set(data1, 'attrs.c', 4); (这种不行)
   
   删除属性：
   vm.$delete( key )
   只能删除 Vue instance（及它的 $data）的根属性。
   
   可以通过下面的方式进行删除:
   Vue.delete(data.attrs, c);
   
```
