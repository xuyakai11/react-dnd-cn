

# DragLayerMonitor

`DragLayerMonitor` 是传递给[hooks-based](/hooks-api/useDragLayer.md)或[decorator-based]的colleting函数的对象。它的方法使您可以获得有关全局拖动状态的信息
### 方法

- **`isDragging`**: 如果正在执行拖动操作返回`true`，否则返回`false`。

- **`getItemType()`**: 返回`string`或`symbol`标识当前拖动项的type。如果未拖动任何项，则返回`null`

- **`getItem()`**:返回表示当前拖动项的普通对象。每个拖动源必须通过从`beginDrag()`方法返回一个对象来指定它。如果未拖动任何项，则返回`null`

- **`getInitialClientOffset()`**: 返回当前拖动操作开始时指针的client offset值：`{ x, y }`。如果未拖动任何项，则返回`null`。

- **`getInitialSourceClientOffset()`**: 返回当前拖动操作开始时拖动源组件的根DOM节点的client offset: `{ x, y }`。如果未拖动任何项，则返回`null`。

- **`getClientOffset()`**: 当拖动操作进行时，返回指针最后记录的client offset: `{ x, y }`。如果未拖动任何项，则返回`null`。

- **`getDifferenceFromInitialOffset()`**: 返回指针最后记录的client offset与当前拖动操作开始时client offset之间的`{x，y}`差。如果未拖动任何项，则返回`null`。

- **`getSourceClientOffset()`**: 根据当前拖动操作开始时的位置和移动差异，返回拖动源组件的根DOM节点的预计client offset: `{ x, y }`。如果未拖动任何项，则返回`null`。
