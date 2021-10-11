# 使用 Hooks API

基于hooks的React DnD API利用了React的一个重要的新特性。hooks极大地影响了大多数人编写 React 组件的方式，并且是在 React 中编写有状态和有效代码的推荐方法。在hooks之前，React 社区在高阶组件和基于decorator的库中投入了大量的精力。在把hooks引入React社区之后，转向使用hook而不是基于decorator的技术的方法和库发生了戏剧性的转变

在概述页面中，指出拖放交互本质上是有状态的。因此react DnD 被设计为利用 Flux 数据模式和拖放状态模型，使用actions和reducers(独立于react)。hooks是在React中利用有状态数据源的完美方法。事实上，这是许多状态管理库在React中采用的方法！

有三个主要hooks用于将组件连接到 React DnD 中，第四个hooks提供给你接入React DnD (用于测试或开发目的)的能力

- [`useDrag`](/hooks-api/use-drag.md)
- [`useDrop`](/hooks-api/use-drop.md)
- [`useDragLayer`](/hooks-api/use-drag-layer.md)
- [`useDragDropManager`](/hooks-api/use-drag-drop-manager.md) (_dev/test hook_)

## 基本例子

为了开始使用hooks，让我们做一个可拖动的box。

```jsx
import { useDrag } from 'react-dnd'

function Box() {
  const [{ isDragging }, drag, dragPreview] = useDrag(() => ({
		// "type" is required. It is used by the "accept" specification of drop targets.
    type: 'BOX',
		// The collect function utilizes a "monitor" instance (see the Overview for what this is)
		// to pull important pieces of state from the DnD system.
    collect: (monitor) => ({
      isDragging: monitor.isDragging()
    })
  }))

  return (
    {/* This is optional. The dragPreview will be attached to the dragSource by default */}
    <div ref={dragPreview} style={{ opacity: isDragging ? 0.5 : 1}}>
        {/* The drag ref marks this node as being the "pick-up" node */}
        <div role="Handle" ref={drag} />
    </div>
  )
}
```

现在，让我们做一些东西把它拖进去。

```jsx
function Bucket() {
  const [{ canDrop, isOver }, drop] = useDrop(() => ({
    // The type (or types) to accept - strings or symbols
    accept: 'BOX',
    // Props to collect
    collect: (monitor) => ({
      isOver: monitor.isOver(),
      canDrop: monitor.canDrop()
    })
  }))

  return (
    <div
      ref={drop}
      role={'Dustbin'}
      style={{ backgroundColor: isOver ? 'red' : 'white' }}
    >
      {canDrop ? 'Release to drop' : 'Drag a box here'}
    </div>
  )
}
```

要进一步探索，请阅读单独的hooks API 文档，或者查看 GitHub 上基于[钩子的示例](https://github.com/react-dnd/react-dnd/tree/main/packages/examples-hooks)。
