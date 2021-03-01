## 浏览器渲染页面过程


## 概念解释

- **DOM Tree**：浏览器将HTML解析成树形的数据结构。  
- **CSS Rule Tree**：浏览器将CSS解析在树形的数据结构。  
- **Render Tree**：DOM和CSSOM(CSS Object Model:CSS对象模型)合并后生成Render Tree。  
- **layout**：有了Render Tree，浏览器已经能知道网页中有哪些节点，各个节点的CSS的定义以及他们的从属关系，从而去计算出每个节点的屏幕中的位置。  
- **painting**：按照算出来的规则，通过显卡，把内容画到屏幕上。  
- **reflow(回流)**：当浏览器发现某个部分发生了点变化影响了布局，需要倒回去重新渲染，称此为回退的过程，叫reflow.reflow会从`<html>`这个root frame开始递归往下，依次计算所有的结点几何尺寸和位置。feflow几乎是无法避免的。例如：树状目录的折叠，展开，实质上是元素的显示与隐藏等，都将引起浏览器的reflow，鼠标划过，点击，只要这些行为引起了页面上的某些元素的占位面积，定位方式，边距等属性的变化，都会引起它的内部，周围甚至整个页面的重新渲染。  
- **repaint(重绘)**：改变某个元素的背景色，文字颜色，边框颜色等等不影响它周围或内部布局的属性时，屏幕的一部分要重画，但是元素的几何尺寸没有变。 

注意点：
1. display:none的节点不会被加入Render Tree,而visibility:hidden则会，所以如果某个节点最开始是不显示的，设为display:none是最好的
2. display:none会触发reflow，而visibility:hidden只会触发repaint,因为位置没有发生变化.
3. 有些情况下，比如修改了元素的样式，浏览器不会立刻reflow和repaint一次，而是会把这样的操作积攒一批，然后做一次reflow，这又叫异步reflow或增量异步reflow,但是有些情况，如resize窗口，改变了页面默认的字体等，对于这些操作，浏览器会马上进行reflow

## 主流程
渲染引擎首先通过网络获得所请求文档的内容，通常以8K分块的方式完成。基本流程为：
解析HTML以构建DOM树 -> 解析CSS构建CSSOM -> 将DOM树与CSSOM树合并，构建Render树 -> 布局render树 -> 绘制render树

1. 构建DOM树：当浏览器客户端从服务器那接受到HTML文档后，就会遍历文档节点然后生成DOM树，DOM树结构和HTML标签一一对应。
2. CSS解析：处理CSS标记，构成层叠样式表模型CSSOM(CSS Object Model)，解析成CSS Rule Tree。
3. 渲染树：根据DOM和CSSOM来构造Render Tree，Render tree不等于DOM Tree,因为像Header或display:none的东西没有必要放在渲染树中。
4. 布局：render layout。
5. 绘制：将渲染树的各个节点绘制到页面上。
6. 
注意：上述这个过程是逐步完成的，为了更好的用户体验，渲染引擎将会尽可能早的将内容呈现到屏幕上，并不会等到所有的html都解析完成之后再去构建和布局render树。它是解析完一部分内容就显示一部分内容，同时，可能还在通过网络下载其余内容。


