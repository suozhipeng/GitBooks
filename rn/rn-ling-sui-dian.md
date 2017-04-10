
# React Native 零碎知识点收集

## 1、样式布局
** 绝对定位**
```javascript
detialStyle:{
// 绝对定位
position:'absolute',
left:0,
bottom:30,
backgroundColor:'red',
color:'white',
padding:2
}

```
**flexWrap-自动换行效果使用**


```javascript
const styles = StyleSheet.create({
contentViewStyle:{
        // 设置主轴的方向
        flexDirection:'row',
        // 多个cell在同一行显示
        flexWrap:'wrap',
        // 宽度
        width:width,
        // 注意：这里必须设置，不然换行不起作用
        alignItems:'center'
    }
});

```

**图片的样式**

```javascript

resizeMode enum('cover', 'contain', 'stretch', 'repeat', 'center') 

决定当组件尺寸和图片尺寸不成比例的时候如何调整图片的大小。

cover: 在保持图片宽高比的前提下缩放图片，直到宽度和高度都大于等于容器视图的尺寸（如果容器有padding内衬的话，则相应减去）。译注：这样图片完全覆盖甚至超出容器，容器中不留任何空白。

contain: 在保持图片宽高比的前提下缩放图片，直到宽度和高度都小于等于容器视图的尺寸（如果容器有padding内衬的话，则相应减去）。译注：这样图片完全被包裹在容器中，容器中可能留有空白

stretch: 拉伸图片且不维持宽高比，直到宽高都刚好填满容器。

repeat: 重复平铺图片直到填满容器。图片会维持原始尺寸。仅iOS可用。

center: 居中不拉伸。



```



![](/assets/WX20170401-152943@2x.png)

## **- 页面跳转**
```javascript
// 跳转到指定页
// 通过这种方式，或取到所有的 导航条
        this.props.navigator.push({
            component:HomeDetail,  //页面名称
            title:'详情页', // 跳转到的页面导航栏的 title
            passProps:{'data':data}    // 传递的参数
        })

// 跳转到 上一页
()=>{this.props.navigator.pop()}

```




