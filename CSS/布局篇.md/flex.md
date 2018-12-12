## flex 布局
设置display：flex,则子元素的float, clear, vertical-align的属性将会失效.  
flex有6个属性:  
* flex-direction 属性设置主轴的方向，及项目的排列方向
* flex-wrap  
默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
* flex-flow  
  flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
* justify-content 属性定义了项目在主轴上的对齐方式
* align-items 属性定义项目在交叉轴上如何对齐
* align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
* flex属性是flex-grow(放大), flex-shrink(缩小) 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选
