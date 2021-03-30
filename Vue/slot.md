#### 独占默认插槽的缩写语法
当被提供内容只有默认插槽时，组件的标签才可以当作插槽的模板使用。
```html
<current-user v-slot:default="slotProps">
{{ slotProps.user.firstName }}
</current-user>

or

<current-user v-slot="slotProps">
{{ slotProps.user.firstName }}
</current-user>
```
#### 结构插值Prop
```html
<current-user v-slot="{user: person}">
{{ person.firstName}}
</current-user>
```
#### 动态插槽名
v-2.6.0+
```html
<base-layout>
  <template v-slot:[dynamicSlotName]>
  </template>
</base-layout>
```
#### 具名插槽的缩写
v-1.6.0+
类似于`v-bind`、`v-model`，`v-slot`可缩写为`#`