# DragPreviewImage

将HTML Image元素呈现为断开连接的拖动预览的组件

### 用法

```jsx
import { DragSource, DragPreviewImage } from 'react-dnd'

function DraggableHouse({ connectDragSource, connectDragPreview }) {
  return (
    <>
      <DragPreviewImage src="house_dragged.png" connect={connectDragPreview} />
      <div ref={connectDragSource}>🏠</div>
    </>
  )
}
export default DragSource(
  /* ... */
  (connect, monitor) => ({
    connectDragSource: connect.dragSource(),
    connectDragPreview: connect.dragPreview()
  })
)
```

### Props

- **`connect`**: 必需。拖动预览的connector function
