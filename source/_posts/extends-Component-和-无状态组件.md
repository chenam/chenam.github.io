---
title: extends Component 和 无状态组件
date: 2019-04-26 16:28:11
tags:
---

### extends Component 定义组件

- 函数的绑定
使用`React.createClass`定义组件自动绑定`this`,但是在ES6的`class`不会
    1. 在构造函数里绑定 2. 使用箭头函数
- 调用super
> super关键字用于访问和调用一个对象的父对象上的函数。

```
import React, {Component} from 'react'

class InputControlES6 extends Component { 
    constructor(props) {
        super(props); //传递props给component
        // Set up initial state
            this.state = {
                text: props.initialValue || 'placeholder' 
            };
        // Functions must be bound manually with ES6 classes
        this.handleChange = this.handleChange.bind(this); 
    } 
    handleChange(event) {
        this.setState({ 
            text: event.target.value
        });
    } 
    render() {
        return (
            <div>
                Type something:
                <input onChange={this.handleChange}
                value={this.state.text} />
            </div>
        );
    }
}
InputControlES6.propTypes = { 
    initialValue: React.PropTypes.string
};
InputControlES6.defaultProps = {
    initialValue: ''
};
```

### 无状态函数式组件

```
const Item = ({ id, title, remove }) => <div className='item'>
  {title}
  <span
    className='deleteItem'
    onClick={remove(id)}
  > x </span>
</div>
```

[参考](https://www.jianshu.com/p/1dc57d51348b)
