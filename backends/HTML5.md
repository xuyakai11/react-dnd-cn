# HTML5

这是 React-DnD 支持的主要后端。它使用了[HTML5的拖放API](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Drag_and_drop)，隐藏了[自己的怪癖](http://quirksmode.org/blog/archives/2009/09/the_html5_drag.html)。

### 初始化

```
npm install react-dnd-html5-backend
```

### 额外的

除了默认的导出功能，HTML5后端模块还提供了一些额外功能:

- **`getEmptyImage()`**: 返回一个透明空[`Image`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/Image)的函数。使用[DragSourceConnector](/docs/api/drag-source-connector)的`connect.dragPreview()`完全隐藏浏览器绘制的拖动预览。
用 DragLayer 绘制[自定义拖曳图层](/hooks-api/useDragLayer.md)很方便。请注意，自定义拖动预览在IE中不起作用

- **`NativeTypes`**: 三个常量的枚举：`NativeTypes.FILE`, `NativeTypes.URL`和`NativeTypes.TEXT`。您可以为这些类型注册[拖放目标](/hooks-api/useDrop.md)，以处理本机文件、 url或常规页面文本的拖放

### 用法

```jsx
import { HTML5Backend } from 'react-dnd-html5-backend'
import { DndProvider } from 'react-dnd'

export default function MyReactApp() {
  return (
    <DndProvider backend={HTML5Backend}>
      /* your drag-and-drop application */
    </DndProvider>
  )
}
```

当您在监视器上调用`getItem()`时，HTML5后端会公开来自事件的各种数据，具体取决于drop type:

- `NativeTypes.FILE`:
  - `getItem().files`, 带有一个文件数组
  - `getItem().items`, 带有 `event.dataTransfer.items` (当删除目录时，可以使用它列出文件)
- `NativeTypes.URL`:
  - `getItem().urls`, 包含已删除URL的数组
- `NativeTypes.TEXT`:
  - `getItem().text`, 已删除的文本

