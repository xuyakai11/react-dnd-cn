
# useDragLayer

使用 `useDragLayer` hook可以将一个组件作为_drag layer_连接到DnD系统中。

```jsx
import { useDragLayer } from 'react-dnd'

function DragLayerComponent(props) {
  const collectedProps = useDragLayer(
    monitor => /* Collected Props */
  )
  return <div>...</div>
}
```
#### 参数

- **`collect`**: 必须。collecting方法。它应该返回一个简单的props对象，以便返回注入到您的组件中。它接受两个参数，`monitor`和`props`。请阅读monitor和collecting功能的介绍[概述](/快速开始/概览.md)。请参阅下一节中详细描述的collecting功能。

#### 返回值

从 collect 函数收集属性的对象
