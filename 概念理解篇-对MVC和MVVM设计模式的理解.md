# 对前端框架MVC和MVVM的理解
## 一、概念解释
`MVC` 即 `Model-View-Controller` 的缩写，就是 模型—视图—控制器。 
`MVVM` 是Model-View-ViewModel 的缩写，它是一种基于前端开发的架构模式，其核心是提供对View 和 ViewModel 的双向数据绑定，这使得ViewModel 的状态改变可以自动传递给 View，即所谓的数据双向绑定。


## 三、为什么前端要工程化，要是使用MVC会如何？

在HTML5 还未火起来的那些年，`MVC` 作为Web 应用的最佳实践是OK 的，这是因为 Web 应用的View 层相对来说比较简单，前端所需要的数据在后端基本上都可以处理好，View 层主要是做一下展示，那时候提倡的是 Controller 来处理复杂的业务逻辑，所以View 层相对来说比较轻量，就是所谓的瘦客户端思想。

相对 HTML4，HTML5 最大的亮点是它为移动设备提供了一些非常有用的功能，使得 HTML5 具备了开发App的能力， HTML5开发App 最大的好处就是跨平台、快速迭代和上线，节省人力成本和提高效率，逐渐用H5代替Native，希望使用H5 开发的应用能和Native 媲美，或者接近于原生App 的体验效果，于是前端应用的复杂程度已不同往日，今非昔比。 那 View 层所做的事，就不仅仅是简单的数据展示了，它不仅要管理复杂的数据状态，还要处理移动设备上各种操作行为等等。因此，前端也需要工程化，也需要一个更合理的框架来管理这些复杂的逻辑，使开发更加高效。 这时前端开发就暴露出了三个痛点问题：

1. 开发者在代码中大量调用相同的 DOM API，处理繁琐 ，操作冗余，使得代码难以维护。
2. 大量的DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。
3. 当 Model 频繁发生变化，开发者需要主动更新到View ；当用户的操作导致 Model 发生变化，开发者同样需要将变化的数据同步到Model 中，这样的工作不仅繁琐，而且很难维护复杂多变的数据状态。

其实，早期jquery 的出现就是为了前端能更简洁的操作DOM 而设计的，但它只解决了第一个问题，另外两个问题始终伴随着前端一直存在。  `MVVM` 的出现，完美解决了以上三个问题。  

**`MVVM` 构成**  
`Model` 层代表数据模型，也可以在`Model`中定义数据修改和操作的业务逻辑；  
`View` 代表UI 组件，它负责将数据模型转化成UI 展现出来；  
`ViewModel` 是一个同步View 和 Model的对象。  

**`MVVM`特点**  
`View` 和 `Model` 之间并没有直接的联系，而是通过`ViewModel`自动进行交互，无需人为干涉  
`Model` 和 `ViewModel` 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上  

ViewModel 是由前端开发人员组织生成和维护的视图数据层。`在这一层，前端开发者对从后端获取的 Model 数据进行转换处理，做二次封装，以生成符合 View 层使用预期的视图数据模型`。需要注意的是 ViewModel 所封装出来的数据模型包括视图的`状态和行为`两部分，而 Model 层的数据模型是只包含状态的，比如页面的这一块展示什么，那一块展示什么这些都属于视图状态（展示），而页面上的交互操作属于视图行为（交互），视图状态和行为都封装在了 ViewModel 里。这样的封装使得 ViewModel 可以完整地去描述 View 层。由于实现了双向绑定，ViewModel 的内容会实时展现在 View 层，这是激动人心的，因为前端开发者再也不必低效又麻烦地通过操纵 DOM 去更新视图，MVVM 框架已经把最脏最累的一块做好了，我们开发者只需要处理和维护 ViewModel，更新数据视图就会自动得到相应更新，真正实现数据驱动开发。看到了吧，View 层展现的不是 Model 层的数据，而是 ViewModel 的数据，由 ViewModel 负责与 Model 层交互，这就完全解耦了 View 层和 Model 层，这个解耦是至关重要的，它是前后端分离方案实施的重要一环。

## MVVM的好处

1. 低耦合。视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model不可以不变，当Model变化的时候View也可以不变。

2. 可重用性。你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。

3. 独立开发。开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计，使用Expression Blend可以很容易设计界面并生成xaml代码。

4. 可测试。界面素来是比较难于测试的，而现在测试可以针对ViewModel来写。
