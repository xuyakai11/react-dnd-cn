
# useDrop

`useDrop` hook提供了一种方法，可以将组件作为拖放目标连接到 DnD 系统中。通过向`useDrop`hook传递一个规范,你可以指定包括drop-target接受数据item的type、要`collect`的props等等。此函数返回一个数组，该数组包含要附加到Drop Target节点的ref和收集的props

```jsx
import { useDrop } from 'react-dnd'

function myDropTarget(props) {
  const [collectedProps, drop] = useDrop(() => ({
    accept
  }))

  return <div ref={drop}>Drop Target</div>
}
```

#### 参数

- **`spec`** 创建规范对象的规范对象或函数。有关规范对象的详细信息，请参阅下文
- **`deps`** 一个可用于缓存的依赖数组，它的工作方式类似于内置的`useMemo` React hook。默认值是 function spec 的空数组和包含对象 spec 的 spec 的数组

#### 返回值数组

- **`[0] - Collected Props`**: 包含从 collect 函数收集的属性的对象. 如果`collect`方法未定义，则返回一个空对象

- **`[1] - DropTarget Ref`**: 拖放目标的connector函数. 必须附加到DOM的拖放目标部分

###  规范对象成员

- **`accept`**: 必需。这必须是一个string、symbol、数组 或者一个返回给定组件的任何一个`props`值的函数。这个`drop target`只会响应`drag sources`指定的`type`或`types`的项，阅读[概述](/快速开始/概览.md)可以了解更多关于item和type的信息

- **`options`**: 可选。一个纯js对象，如果组件中的一些`props`不是标量(也就是说，不是原始值或函数) ，那么在`options`对象中定一个自定义的`arePropsEqual(props, otherProps)函数可以提高性能。除非你有性能问题，否则不用担心。

- **`drop(item, monitor)`**: 可选。当兼容的item被拖放到目标上时调用，你可以返回undefined，也可以返回普通对象。如果返回一个对象，它将成为拖放结果，并作为`monitor.getDropResult()`对 `endDrag`方法中的拖动源可用。如果你希望根据接收的拖放目标执行不同的操作，这将非常有用。如果你有嵌套的拖放目标，你可以通过检查`monitor.didDrop()`和 `monitor.getDropResult()`来测试嵌套目标是否已经处理了`drop`。`drop`方法和源的`endDrag`方法都是触发Flux动作的好地方。如果定义了`canDrop()`并返回了`false`，则不会调用此方法。

- **`hover(item, monitor)`**: 可选。当item悬停在组件上时调用。你可以检查`monitor.isOver({ shallow: true })`，以测试悬停是仅发生在当前目标上，还是发生在嵌套目标上。与 `drop()`不同，即使定义了 `canDrop()` 并返回 `false`，也会调用这个方法。你可以检查 `monitor.canDrop()` 来测试是否是这种情况。

- **`canDrop(item, monitor)`**: 可选。使用它指定拖放目标是否能够接受该item。如果你想总是允许它，只需省略这个方法。如果你希望基于`props`或`monitor.getItem()`断言禁用拖动，则指定它非常方便。注意: 不能在此方法中调用 `monitor.canDrop()`。

- **`collect`**: 可选。collecting方法。它应该返回一个简单的props对象，以便返回注入到您的组件中。它接受两个参数，`monitor`和`props`。请阅读monitor和collecting功能的介绍[概述](/快速开始/概览.md)。请参阅下一节中详细描述的collecting功能。


