## Popover 弹出框

### 基础用法

Popover 的属性与 Tooltip 很类似，它们都是基于`Vue-popper`开发的，因此对于重复属性，请参考 Tooltip 的文档，在此文档中不做详尽解释。

:::demo `trigger`属性用于设置何时触发 Popover，支持四种触发方式：`hover`，`click`，`focus` 和 `manual`。对于触发 Popover 的元素，有两种写法：使用 `#reference` 的具名插槽，或使用自定义指令`v-popover`指向 Popover 的索引`ref`。

```html
<template>
  <el-popover
    placement="top-start"
    title="标题"
    :width="200"
    trigger="hover"
    content="这是一段内容,这是一段内容,这是一段内容,这是一段内容。"
  >
    <template #reference>
      <el-button>hover 激活</el-button>
    </template>
  </el-popover>

  <el-popover
    placement="bottom"
    title="标题"
    :width="200"
    trigger="click"
    content="这是一段内容,这是一段内容,这是一段内容,这是一段内容。"
  >
    <template #reference>
      <el-button>click 激活</el-button>
    </template>
  </el-popover>

  <el-popover
    ref="popover"
    placement="right"
    title="标题"
    :width="200"
    trigger="focus"
    content="这是一段内容,这是一段内容,这是一段内容,这是一段内容。"
  >
    <template #reference>
      <el-button>focus 激活</el-button>
    </template>
  </el-popover>

  <el-popover
    placement="bottom"
    title="标题"
    :width="200"
    trigger="manual"
    content="这是一段内容,这是一段内容,这是一段内容,这是一段内容。"
    v-model:visible="visible"
  >
    <template #reference>
      <el-button @click="visible = !visible">手动激活</el-button>
    </template>
  </el-popover>
</template>

<script>
  export default {
    data() {
      return {
        visible: false,
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';

  export default defineComponent({
    setup() {
      return {
        visible: ref(false),
      };
    },
  });

</setup>
-->
```

:::

### 嵌套信息

可以在 Popover 中嵌套多种类型信息，以下为嵌套表格的例子。

:::demo 利用分发取代`content`属性

```html
<el-popover placement="right" :width="400" trigger="click">
  <template #reference>
    <el-button>click 激活</el-button>
  </template>
  <el-table :data="gridData">
    <el-table-column width="150" property="date" label="日期"></el-table-column>
    <el-table-column width="100" property="name" label="姓名"></el-table-column>
    <el-table-column
      width="300"
      property="address"
      label="地址"
    ></el-table-column>
  </el-table>
</el-popover>

<script>
  export default {
    data() {
      return {
        gridData: [
          {
            date: '2016-05-02',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
          {
            date: '2016-05-04',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
          {
            date: '2016-05-01',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
          {
            date: '2016-05-03',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
        ],
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, reactive, toRefs } from 'vue';

  export default defineComponent({
    setup() {
      const state = reactive({
        gridData: [
          {
            date: '2016-05-02',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
          {
            date: '2016-05-04',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
          {
            date: '2016-05-01',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
          {
            date: '2016-05-03',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄',
          },
        ],
      });
      return {
        ...toRefs(state),
      };
    },
  });

</setup>
-->
```

:::

### 嵌套操作

当然，你还可以嵌套操作，这相比 Dialog 更为轻量：

:::demo

```html
<el-popover placement="top" :width="160" v-model:visible="visible">
  <p>这是一段内容这是一段内容确定删除吗？</p>
  <div style="text-align: right; margin: 0">
    <el-button size="mini" type="text" @click="visible = false">取消</el-button>
    <el-button type="primary" size="mini" @click="visible = false"
      >确定</el-button
    >
  </div>
  <template #reference>
    <el-button @click="visible = true">删除</el-button>
  </template>
</el-popover>

<script>
  export default {
    data() {
      return {
        visible: false,
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';

  export default defineComponent({
    setup() {
      return {
        visible: ref(false),
      };
    },
  });

</setup>
-->
```

:::

### Attributes

| 参数                      | 说明                                                                                                    | 类型           | 可选值                                                                                                    | 默认值                                                  |
| ------------------------- | ------------------------------------------------------------------------------------------------------- | -------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| trigger                   | 触发方式                                                                                                | String         | click/focus/hover/manual                                                                                  | click                                                   |
| title                     | 标题                                                                                                    | String         | —                                                                                                         | —                                                       |
| content                   | 显示的内容，也可以通过 `slot` 传入 DOM                                                                  | String         | —                                                                                                         | —                                                       |
| width                     | 宽度                                                                                                    | String, Number | —                                                                                                         | 最小宽度 150px                                          |
| placement                 | 出现位置                                                                                                | String         | top/top-start/top-end/bottom/bottom-start/bottom-end/left/left-start/left-end/right/right-start/right-end | bottom                                                  |
| disabled                  | Popover 是否可用                                                                                        | Boolean        | —                                                                                                         | false                                                   |
| visible / v-model:visible | 状态是否可见                                                                                            | Boolean        | —                                                                                                         | false                                                   |
| offset                    | 出现位置的偏移量                                                                                        | Number         | —                                                                                                         | 0                                                       |
| transition                | 定义渐变动画                                                                                            | String         | —                                                                                                         | fade-in-linear                                          |
| show-arrow                | 是否显示 Tooltip 箭头，更多参数可见[Vue-popper](https://github.com/element-component/vue-popper)        | Boolean        | —                                                                                                         | true                                                    |
| popper-options            | [popper.js](https://popper.js.org/documentation.html) 的参数                                            | Object         | 参考 [popper.js](https://popper.js.org/documentation.html) 文档                                           | `{ boundariesElement: 'body', gpuAcceleration: false }` |
| popper-class              | 为 popper 添加类名                                                                                      | String         | —                                                                                                         | —                                                       |
| show-after                | 延迟出现，单位毫秒                                                                                      | Number         | —                                                                                                         | 0                                                       |
| hide-after                | 延迟关闭，单位毫秒                                                                                      | Number         | —                                                                                                         | 0                                                       |
| auto-close                | Tooltip 出现后自动隐藏延时，单位毫秒，为 0 则不会自动隐藏                                               | number         | —                                                                                                         | 0                                                       |
| tabindex                  | Popover 组件的 [tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) | number         | —                                                                                                         | —                                                       |

### Slot

| 参数      | 说明                          |
| --------- | ----------------------------- |
| —         | Popover 内嵌 HTML 文本        |
| reference | 触发 Popover 显示的 HTML 元素 |

### Events

| 事件名称    | 说明                   | 回调参数 |
| ----------- | ---------------------- | -------- |
| show        | 显示时触发             | —        |
| after-enter | 显示动画播放完毕后触发 | —        |
| hide        | 隐藏时触发             | —        |
| after-leave | 隐藏动画播放完毕后触发 | —        |
