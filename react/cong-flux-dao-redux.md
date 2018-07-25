> 一个容易理解的对比：React 是用来取代Jquery的，那么Flux 就是以替换Backbone.js/Ember.js等MVC一族框架为目的的。
>
> 要了解Redux，首先要从Flux 说起。可以认为Redux 是Flux思想的另一种实现方式。通过了解Flux、我们可以知道Flux一族框架贯彻的最重要的观点--单向数据流，更重要的是我们可以发现Flux框架的缺点，从而更深刻的认识到Redux相对于Flux的改进之处。

### MVC 框架的缺陷

![](/assets/MVC-Tradition.png)

MVC框架把应用分为三个部分：

1. **Model** 负责管理数据，大部分业务逻辑也应该放在Model中；
2. **View** 负责渲染用户界面，应该避免在View中涉及业务逻辑；
3. **Controller** 负责接受用户输入，根据用户输入调用对应的Model部分逻辑，把产生的数据结果交给View部分，让VIew渲染出必要的输出。

> 实际使用中的MVC：前端MVC往往为了操作方便允许View 和Model直接对话，将造成复杂的网状依赖关系，使局面失控。
>
> 对于MVC框架，为了让数据流可控，Controller 应该是中心，当View要传递消息给Model时，应该调用Controller的方法，同样，当Model需要跟新View时，也应该通过Controller。

![](/assets/tradition-mvc-conplex.png)

#### Flux 框架

![](/assets/Flux-framwork.png)

Flux 应用的四个部分：

1. Dispatcher ，处理动作分发，维持Store之间的依赖关系；
2. Store ，负责存储数据和处理数据相关逻辑；
3. Action，驱动Dispatcher 的js 对象；
4. View ，视图部分，负责显示用户界面。

> 在 MVC框架中，系统能够提供什么什么样的服务，通过Controller 暴露的函数来实现。每增加一个功能，Controller 往往就要增加一个函数；在Flux的世界里，新增加功能并不需要Dispatcher增加新的函数，实际上，Dispatcher自始至终只需要暴露一个函数Dispatch，当需要增加新的功能时，要做的是增加一个新的Action类型，Dispatcher对外的接口不用改变。

![](/assets/TIM截图20180717113931.png)

> **CounterStore.js** 通过注册action自负责自身的数据变更，Counter组件通过事件派发action，触发CounterStore.js 维护的数据便跟后，根据CounterStore.js 提供的getCounterValues接口返回变更后的数据。

![](/assets/scanner_20180720_120010.jpg)

Flux 的优缺点：

1. 单向数据流限制了model和view之间的混乱
2. store之间依赖关系
3. 难以进行服务端渲染
4. store混杂了逻辑和状态

### Redux

Flux的基本原则是“单向数据流”，Redux在此基础上强调三个基本原则：

1. **唯一数据源（Single Source of Truth）**：整个应用只保持一个Store，所有组件的数据源就是这个Store上的状态。
2. **保持状态只读（State is read-only）**：不直接修改状态，要修改Store的状态，必须要通过派发一个action对象完成。
3. **数据改变只能通过纯函数完成（Changes are made with pure funtions）**：这里所说的纯函数是指reducer。reducer函数接受两个参数：**reducer\(state,action\)**。第一个参数state是当前的状态，第二个参数action是收受到的action对象，而reducer函数要做个事情就是根据state和action的值产生一个新的对象返回（返回的结果必须完全由参数state和action决定，而且不应产生任何副作用）。

> Flux中更新状态的函数只有一个参数action，因为状态是由Store直接管理的，所以处理函数中会看到直接更新state.
>
> ```js
> CounterStore.dispatchToken = AppDispatcher.register((action)=>{
>     if(action.type === ActionTypes.INCREMENT){
>         counterValues[action.counterCaption]++;
>         CounterStore.emitChange();
>     }else if(action.type === ActionTypes.DECREMENT){
>         counterValues[action.counterCaption]--;
>         CounterStore.emitChange();
>     }
> });
> ```
>
> Redux中实现同样功能的reducer代码如下：reducer只负责计算状态，却并不负责存储状态。
>
> ```js
> import * as ActionTypes from './ActionTypes.js';
>
> export default (state,action)=>{
>     const {counterCaption} = action;
>     switch(action.type){
>         case ActionTypes.INCREMENT:
>             return {...state,[counterCaption]:state[counterCaption]+1};
>         case ActionTypes.DECREMENT:
>             return {...state,[counterCaption]:state[counterCaption]-1};
>         default:
>             return state;
>     }
> }
> ```



