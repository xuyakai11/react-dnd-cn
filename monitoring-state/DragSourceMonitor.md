# DragSourceMonitor

`DragSourceMonitor` 是传递给[hooks-based](/hooks-api/useDrag.md)或decorator-based的拖动源的colleting函数的对象。它的方法使您可以获得关于特定拖动源的拖动状态的信息。绑定到该监视器的特定拖动源在下面称为监视器的所有者

### 方法

- **`canDrag()`**: 如果没有进行拖动操作，并且所有者的`canDrag()`返回`true`或未定义，则返回`true`

- **`isDragging()`**: 如果正在执行拖动操作，并且所有者发起了拖动，或者定义了其`isDraging()`并返回`true`，则返回`true`。

- **`getItemType()`**: 返回`string`或`symbol`标识当前拖动项的type。如果未拖动任何项，则返回`null`

- **`getItem()`**:返回表示当前拖动项的普通对象。每个拖动源必须通过从`beginDrag()`方法返回一个对象来指定它。如果未拖动任何项，则返回`null`

- **`getDropResult()`**: 返回一个表示最近记录的拖动结果的普通对象。拖放目标可以通过从其`drop()`方法返回一个对象来选择性地指定它。当为嵌套目标自底向上分派`drop()`链时，任何显式返回其自己的`drop()`结果的父节点都会覆盖子节点以前设置的子节点drop结果。如果在`endDrag()`之外调用返回`null`。

- **`didDrop()`**: 如果某个drop目标已处理drop事件，则返回`true`，否则返回`false`。即使目标没有返回`drop`结果，`didDrop()`也会返回`true`。在`endDrag()`中使用它来测试是否有任何拖放目标已经处理了拖放。如果在`endDrag()`之外调用`didDrop()`会返回`false`。

- **`getInitialClientOffset()`**: 返回当前拖动操作开始时指针的client offset值：`{ x, y }`。如果未拖动任何项，则返回`null`。

- **`getInitialSourceClientOffset()`**: 返回当前拖动操作开始时拖动源组件的根DOM节点的client offset: `{ x, y }`。如果未拖动任何项，则返回`null`。

- **`getClientOffset()`**: 当拖动操作进行时，返回指针最后记录的client offset: `{ x, y }`。如果未拖动任何项，则返回`null`。

- **`getDifferenceFromInitialOffset()`**: 返回指针最后记录的client offset与当前拖动操作开始时client offset之间的`{x，y}`差。如果未拖动任何项，则返回`null`。

- **`getSourceClientOffset()`**: 根据当前拖动操作开始时的位置和移动差异，返回拖动源组件的根DOM节点的预计client offset: `{ x, y }`。如果未拖动任何项，则返回`null`。
