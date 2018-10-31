# React注意事项

    * 首先: this.setState(() => ({
        inputValue:value}));
  setState里面建议使用函数的形式返回对象。如果想要使用this.state 则在里面传入
preState，等价于this.state

## ref是指向dom层的，一般不建议使用  


## 生命周期函数一般分为 init Mounting Uqdation UnMounting  
  * Init: set up props和state  
  * Mounting:
        componentWillMount
        render
        componentDidmount
  * Uqdation:  
        props:  componentWillReciveProps  
                shouldComponentUqdate return true
                componentWillUqdate
                render
                componentDidUqdate
        state: shouldComponentUqdate return true
               componentWillUqdate
               render
               componentDidUqdate

  ## 关于对传参数的设置 :
   propsType:这里设置参数的类型的设置  
   defaultProps: 对参数的初始化，如果参数没有设置的化

  ## Diff算法  
  对于React生成的dom树，显示生成虚拟dom树（这里是js对象），然后渲染成真实的dom树，如果state发生变化，则先对比原先的虚拟dom树，然后替换掉变化的。因为对比js对象，消耗较少。

  ## key的设置
  一般不建议设置成index，设置key值是为了diff算法更新渲染做对比。

  ## 开发小细节
   对于TodoList这样的子组件，一般通过设置函数传入数组或者对象来对对象遍历循环，使用map方法。
