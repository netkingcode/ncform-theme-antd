# ncform-theme-antd
ncform widgets of ant design vue

## todo


### input

1 autocomplete
* immediateShow
* itemTemplate

2 compound

3 Upload


### select

- filterLocal

### color picker

### date picker

1 type
- year
- datetime

### rate
```
  lowThreshold: 2, // 低分和中等分数的界限值，值本身被划分在低分中
  highThreshold: 4, // 高分和中等分数的界限值，值本身被划分在高分中
  colors: ['#F7BA2A', '#F7BA2A', '#F7BA2A'], // icon 的颜色数组，共有 3 个元素，为 3 个分段所对应的颜色
  voidColor: '#C6D1DE', // 未选中 icon 的颜色
  disabledVoidColor: '#EFF2F7', // 只读时未选中 icon 的颜色
  iconClasses: ['el-icon-star-on', 'el-icon-star-on','el-icon-star-on'], // icon 的类名数组，共有 3 个元素，为 3 个分段所对应的类名
  voidIconClass: 'el-icon-star-off', // 未选中 icon 的类名
  disabledVoidIconClass: 'el-icon-star-on', // 只读时未选中 icon 的类名
  showText: false, // 是否显示辅助文字，若为真，则会从 texts 数组中选取当前分数对应的文字内容
  showScore: false, // 是否显示当前分数，showScore 和 showText 不能同时为真
  textColor: '#1F2D3D', // 辅助文字的颜色
  texts: ['极差', '失望', '一般', '满意', '惊喜'] /
```

### checkbox
- button mode

### upload

### layout