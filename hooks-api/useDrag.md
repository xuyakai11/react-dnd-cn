# useDrag
`useDrag` hook提供了一种将组件作为拖动源连接到DnD系统的方法。通过将一个规范传入`useDrag`，您可以声明性地描述可拖动生成的type、表示拖动源的`item`object、要`collect`的props等等。`useDrag` hooks返回一些关键item: 一组收集的props，以及可能附加到_拖动源_和_拖动预览_元素的引用


```jsx
import { useDrag } from 'react-dnd'

function DraggableComponent(props) {
  const [collected, drag, dragPreview] = useDrag(() => ({
    type,
    item: { id }
  }))
  return collected.isDragging ? (
    <div ref={dragPreview} />
  ) : (
    <div ref={drag} {...collected}>
      ...
    </div>
  )
}
```

#### 参数

- **`spec`** 创建规范对象的规范对象或函数。有关规范对象的详细信息，请参阅下文
- **`deps`** 一个可用于缓存的依赖数组，它的工作方式类似于内置的`useMemo` React hook。默认值是 function spec 的空数组和包含对象 spec 的 spec 的数组

#### 返回值数组
- **`[0] - Collected Props`**: 包含从 collect 函数收集的属性的对象. 如果没有 `collect` function未定义，则返回一个空对象
- **`[1] - DragSource Ref`**: 拖动源的connector函数. 必须附加到DOM的可拖动部分
- **`[2] - DragPreview Ref`**: 一个用于拖动预览的connector函数。这可能附加到DOM的预览部分

###  规范对象成员

- **`type`**: 必需。这必须是一个string或symbol。只有注册的type相同，拖放目标才会对此item作出反应。阅读[概述](/快速开始/概览.md)可以了解更多关于item和type的信息。

- **`item`**: 必需(object或function)。

  - 当值为对象时，item是一个描述被拖动数据的普通js对象，这是拖放目标可以获得的关于拖动源的唯一信息，因此选择他们需要知道的最小数据非常重要，你可能想在这里放一个复杂的引用，但是您应该尽量     避免这样做，因为它会将拖放源和拖放目标耦合在一起， 使用类似于`{ id }`是比较好的方法

  -  当这是一个函数时，它在拖动操作开始时触发，并返回一个表示拖动操作的对象(参见第一个项目符号)。如果返回 null，则取消拖动操作

- **`previewOptions`**: 可选。描述拖动预览选项的纯 JavaScript 对象

- **`options`**: 可选。一个包含以下任一属性的纯JavaScript对象

   - **`dropEffect`**: 可选。要在此拖动上使用的拖放效果的类型。（“移动”或“复制”是有效值。）

- **`end(item, monitor)`**: 可选。当拖动停止，`end`被调用。对于每个`start`调用，都保证有一个相应的`end`调用。您可以调用`monitor.didDrop()`来检查drop是否由兼容的drop目标处理。如果已经处理了，而且拖放目标通过从其`drop()`方法返回一个普通对象来指定拖放结果，那么它将是可用的作为`monitor.getDropResult()`。这个方法是触发flux action比较好的地方。注意: 如果组件在拖动时被卸载，组件参数设置为 null

- **`canDrag(monitor)`**:可选。使用它指定当前是否允许拖动。如果你想总是允许它，只需省略这个方法。如果你希望基于props断言禁用拖动，则指定它非常方便。注意: 不能在此方法中调用 `monitor.canDrag()`。

- **`isDragging(monitor)`**: 可选。默认情况下，只有启动拖动操作的拖动源被认为是拖动。您可以通过定义自定义的`isDragging`方法来重写此行为。它可能返回类似`props.id === monitor.getItem ().id`这样的内容。这样做，如果原始组件可能会在拖动期间卸载并且之后“复活”一个不同的父组件。例如，当在看板中移动一张卡片时，您希望它保留被拖动的外观，即使从技术上讲，每次您将该组件移动到另一个列表时，该组件都会被卸载，并且会挂载另一个不同的组件。注意: 您不能在此方法中调用`monitor.isDragging()`。

- **`collect`**: 可选。collecting方法。它应该返回一个简单的props对象，以便返回到组件中进行注入。它接受两个参数，`monitor`和`props`。请阅读monitor和collecting功能的介绍[概述](/快速开始/概览.md)。请参阅下一节中详细描述的collecting功能。

