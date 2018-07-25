### 组件的数据

React 组件的数据分为两种，prop 和 state。**prop 是组件的对外的接口，state 是组件的内部状态**。对外用prop ，对内用state。

#### prop

* 在 react 中，prop 是从外部传递给组件的数据，一个 react 组件通过定义自己能够接受的prop 就定义了自己的对外公共接口。每个react 组件都是独立存在的模块，组件之外一切都是外部世界，外部世界就是通过prop来和组件对话的。
* react 组件的prop除了支持字符串，还可以是任何一种js语言支持的数据类型。（HTML 的prop 只能支持字符串）
* 外部世界传数据给react 组件最直接的方式是prop；同样，react 组件也可以通过prop反馈数据给外部世界（此时prop应该是一个函数，函数类型的prop等于是父组件交给了子组件一个回调函数，子组件在恰当的时候调用函数类型的prop，带上必要的参数便可以将信息传递给外部世界）。
* 组件要接受传入的prop，必须得有构造函数**constructor\(props\)**，且首先调用**super\(props\)，**后续才可以用**this.props**获取传入进来的值。

```js
/*...*/
class Counter extends Component {
    constructor(props){
        super(props);
        this.onClickIncrementButton = this.onClickIncrementButton.bind(true);
        /*...其他初始化操作*/
        this.state = {
            count:props.initValue
        }
    }
}
/*...*/
Counter.propTypes = {
    initValue:PropTypes.number||0, //此种默认赋值方法易遗漏，可以之用类的defaultProps属性来定义默认值
    caption:PropTypes.string.isRequired

}
```

* **propTypes**：组件接口类型检查，es6 语法中必须定义在类的**propTypes**属性上。当传入数据与要求类型不一致是会在控制台中报错，但是不会阻断渲染（即非强制性）。（v15.5起移出到prop-type，得单独npm安装）
* **defaultProps**：定义prop的默认值（有时父类中忘传prop,则可使用默认值）

#### state

* state 代表组件的内部状态。由于**react组件不能修改传入的prop**，所以需要记录自生数据的变化就用state。通常在构造函数的结尾通过对**this.state**赋值完成对组件的初始化。

> 严格来说，React 并没有办法阻止修改传入的props对象。所以，每个开发者就把这个当做一个规矩，在编码中一定不要踩这条红线，不然可以遇到不可预料的bug。

* **组件的state必须是一个js对象**，即使我们需要存储的知识一个数字类型的数据，也只能把它存作state某个字段的值。

* 在早期的react中，创建组件使用**React.createClass **方法来创建组件类，这种方式下通过定义组件类的一个getInitialState方法来获取初始state值。这种做法现在**已废弃**。\(还有与之配套的两个方法getDefaultProps 和 getInitialState \)（现在使用es6 class）

* 更新state必须使用**this.setState**\({filed:value}\)，否则将破坏响应性，不会触发渲染

#### prop VS state

* prop用于定义外部接口，state用于记录内部状态
* prop 的赋值在外部世界中使用组件时，state的赋值在组件内部
* 组件不应该改变prop的值，而state存在的目的就是让组件来改变的

> UI = render\(data\)
>
> React 组件扮演的是render函数的角色，应该是一个没有副作用的纯函数。修改props值是一个有副作用的操作，组件应该避免。

### 组件的声明周期

![](/assets/react-component-life-cycle.png)

几点注意

* 创建组件的方法React.createClass 及其配套的初始化方法getInitialState/getDefaultProps正被逐渐废弃。现在主要使用es6语法的class、this.state/defaultProps替代。

```js
//过时，不推荐
const Sample = React.createClass({
    getInitialState:function(){
        return {foo:'bar'};
    },
    getDefaultProps:function(){
        return {sampleProp:0}
    }
})

//推荐
class Sample extends React.Componet{
    constructor(props){
        super(props);
        this.state = {
            foo:'var'
        }
    }
}

Sample.defaultProps = {
    sampleProp:0
}
```

* 在render函数执行的过程，其前后有两组钩子函数**componentWillMount/componentDidMount**、**componentWillUpdate/componentDidUpdate**，分别用于第一次组件初始化渲染前后和组件状态变更渲染前后。
* 触发组件状态跟新（re-render）的两种情况：props改变或state改变

> 1.**componentWillReceiveProps\(nextProps\)**  
> 只要父组件的render函数被调用，在render函数里面被渲染的子组件就会经历更新过程，不管父组件传递给子组件的props有没有改变，都会触发子组件的componentWillReceiveProps函数。（注意通过this.setState方法触发的更新过程不会调用这个函数）
>
> **2.shouldComponentUpdate\(nextProps,nextState\)**
>
> 除了render函数外，React 组件生命周期中最重要的一个函数。render重要是因为render函数决定了什么该渲染，而shouldComponentUpdate函数重要，是因为它决定了一个组件什么时候不需要渲染。render和shouldComponentUpdate也是react生命周期中唯二两个要求有返回结果的函数。render函数的返回结果将用于构造DOM对象，而shouldComponentUpdate函数返回的结果告诉react这个组件在更新过程中是否要继续。
>
> **组件通过this.setState函数引发更新的过程，并不是立即跟新组件的state值，在执行到函数shouldComponentUpdate的时候，this.state依然是this.setState函数执行之前的值，所以我们要做的实际是在nextProps、nextState、this.props和this.state中相互对比。**

* **组件向外传递数据**：即利用函数类的prop，通过在子组件中触发父组件中函数类的prop回调传值。（增加了组件的耦合性，利用redux可解决这一问题）





