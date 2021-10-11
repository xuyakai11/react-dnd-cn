### DndProvider

DndProvider组件为你的应用程序提供了React-DnD功能。这必须通过`backend`注入一个backend，但它可能被注入一个`windoow`对象

### 用法

```jsx
import { HTML5Backend } from 'react-dnd-html5-backend'
import { DndProvider } from 'react-dnd'

export default class YourApp {
  render() {
    return (
      <DndProvider backend={HTML5Backend}>
        /* Your Drag-and-Drop Application */
      </DndProvider>
    )
  }
}
```
### Props 参数

- **`backend`**: 必选项。一个 React DnD 后端。除非您正在编写一个定制的后端，否则您可能需要使用[HTML5 backend](/backends/html5) ，这是React DnD承载的
- **`context`**: 可选。用于配置后端的后端上下文。这取决于后端实现
- **`options`**: 可选。用于配置后端的选项对象。这取决于后端实现
