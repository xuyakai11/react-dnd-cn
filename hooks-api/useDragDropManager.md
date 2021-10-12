# useDragDropManager

该钩子为用户提供了进入 DnD 系统的访问权限。DragDropManager实例是React DnD创建的单例模式，它包含对状态、监视器、后端等的访问。

```jsx
import { useDragDropManager } from 'react-dnd'

function Example() {
  // The manager provides access to all of React DnD's internals
  const dragDropManager = useDragDropManager()

  return <div>Example</div>
}
```
