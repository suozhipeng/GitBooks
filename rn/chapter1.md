# ReactNative

---

## React Native 项目中 **回调函数使用**

`A`--&gt;`B`--&gt;`C`:A是主页面，包含组件B。组件B又有组件C构成  
**- 组件C**

```javascript
var MiddleCommonView = React.createClass({
    getDefaultProps(){
        return{
            title:'',
            detailText:'',
            rightIcon:'',
            textColor:'',
            tplurl:'',  // 下级界面的 URL 路径
            // 回调函数
            callBackClickCell:null
        }
    },

    render() {
        return (
            // 点击当前 View 执行的方法，同时传递的参数是 tplurl
          <TouchableOpacity onPress={()=>{this.clickCell(this.props.tplurl)}}> 
            <View style={styles.container}>
               {/*当前组件 View 中要展示的内容*/}
            </View>
           </TouchableOpacity>
        );
    },

    // 点击触发的方法
    clickCell(data){
        // 判断处理
        if(this.props.callBackClickCell == null){
            return;
        }
        // 执行回调函数
        this.props.callBackClickCell(data);
        {alert(data)}
    }
});
```

**- 组件B**  
1、var 导入组件C

```javascript
var ContentMiddleView = React.createClass({

    getDefaultProps(){
      return{
          // 回调函数
          popTopHome:null
      }
    },

    render() {
        return (
            <View style={styles.container}>
                <CommonView
                    title= {itemData.maintitle}
                    detailText={itemData.deputytitle}
                    rightIcon={this.renderConvertUrl(itemData.imageurl)}
                    textColor={itemData.typeface_color}
                    tplurl={itemData.tplurl}
                    callBackClickCell={(itemData)=>{this.popToTopView(itemData)}}
                    key={i}
                />
            </View>
        );
    },
    // 继续执行回调函数
    popToTopView(data){
      this.props.popTopHome(data)
    },
```

**- 组件A**  
1、导入组件 `B`

```javascript
var Home = React.createClass({
    render() {
        return (
            <View style={styles.container}>
                <HomeContentMiddle
                      popTopHome={(data)=>{this.pushToDetail(data)}}
                />
            </View>
        );
    },

    // 跳转到详情页
    pushToDetail(data){
        // 通过这种方式，或取到所有的 导航条
        this.props.navigator.push({
            component:HomeDetail,  //页面名称
            title:'详情页', // 跳转到的页面导航栏的 title
            passProps:data    // 传递的参数
        })
    },
});
```



