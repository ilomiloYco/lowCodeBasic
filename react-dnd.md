### react-dnd

#### Dnd-Provider

本质是一个由React.createContext创建的一个上下文容器，控制拖拽行为和数据共享。

#### Backend

将 DOM 事件相关的代码独立出来就叫做 Backend，将拖拽事件转换为 React DnD 内部的 redux action。由于拖拽发生在 H5 的时候是 ondrag，发生在移动设备的时候是由 touch 模拟，是 DnD 在 Dom 层的实现。

- react-dnd-html5-backend : 用于控制html5事件的backend
- react-dnd-touch-backend : 用于控制移动端touch事件的backend
- react-dnd-test-backend : 用户可以参考自定义backend

#### useDrag

让DOM实现拖拽能力的构子

**返回三个参数**

* 第一个返回值是一个对象，表示关联在拖拽过程中的变量，需要在collect属性中映射绑定，比如isDragging、canDrag等。
* 第二个返回值是拖拽元素的ref。
* 第三个返回值是拖拽元素拖拽后实际操作的dom。

**传入两个参数**

* 第一个参数是一个对象，描述drag的配置信息
  * type：指定元素的属性，元素属性相同才能drop。
  * item：描述拖拽元素的数据，如果是一个方法，在开始拖拽时调用，返回描述拖拽元素的数据。
  * end（item，moniter）：拖拽结束的回调函数。
  * isDragging（moniter）：判断元素是否处于拖拽过程中。
  * canDrag（moniter）：判断元素是否可以拖拽。
  * collect（item，moniter）：返回一个描述状态的普通对象，然后返回注入到组件中。
* 第二个参数是一个数组，对方法更新的约束，数组中的参数发生改变，重新生成方法。

#### DragSourceMonitor

传入拖动源collect函数中的对象，允许获取拖动状态的信息。

* canDrag()
* isDragging()
* getItemType()
* getItem()
* getDropResult()：返回拖拽结果，可以拿到从drop元素中返回的数据
* didDrop()：拖拽结束，元素是否放置成功。
* getDifferenceFromInitialOffset():获取相对拖拽起始位置的相对偏移坐标

#### useDrop

实现拖拽物放置的钩子

返回两个参数

* 第一个返回值是一个对象，表示关联在拖拽过程中的变量，在collect属性中映射绑定。
* 第二个返回值是放置元素的ref。

传入一个参数

* 描述drop的配置信息
  * accept：指定接收元素的类型。
  * drop（item，moniter）：有拖拽物放置到元素上触发的回调方法，返回一个对象，可以由拖拽物的moniter.getDropResult()方法获得。
  * hover（item，moniter）：当拖拽物在上方hover时触发，返回bool值。
  * canDrop（item，moniter）：是否可以放置。



