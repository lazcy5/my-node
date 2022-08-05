```javascript
import React, {Component} from 'react';

import {ScrollView, View, StyleSheet, StatusBar, Dimensions, Image, Text} from 'react-native';

 

var {width} = Dimensions.get('window');

 

 

export default class HelloWorldApp extends Component {

 

​    constructor() {

​        super(...arguments);

​        this.state = {list: [1, 2, 3], current: 0};

​        this.timer=null;

​        this.point = 0

​    }

 

​    createPointer() {

​        return (<View style={S.dot}>{this.state.list.map((item, index) => {

​            var color = index === this.state.current ? {color: 'blue'} : {color: 'white'}

​            return <Text key={index} style={[{

​                fontSize: 25,

​                marginLeft: 20

​            }, color]}

​            \>&bull;

​            </Text>

​        })

​        }</View>)

​    }

//自动轮播

​    move = (e) => {

​        this.setState({current: e.nativeEvent.contentOffset.x / width})

​    }

//拖拽开始

​    drag=()=>{

​        this.timer&&clearInterval(this.timer)

​    }

//拖拽结束

​    end=()=>{

​        var scroll=this.refs.scroll;

​        this.timer=setInterval(() => {

​            this.point++;

​            if (this.point > this.state.list.length - 1) {

​                this.point = 0

​            }

​            this.setState({current: this.point})

​            scroll.scrollResponderScrollTo({x:this.point*width,y:0,animated:true})

​        }, 2000)

​    }

​    componentDidMount() {

​        // var scroll=this.refs.scroll;

​        // this.timer=setInterval(() => {

​        //     this.point++;

​        //    if (this.point > this.state.list.length - 1) {

​        //         this.point = 0

​        //     }

​        //     this.setState({current: this.point})

​        //     scroll.scrollResponderScrollTo({x:this.point*width,y:0,animated:true})

​        // }, 2000)

​    }

​    componentWillUnmount() {

​    //   clearInterval(this.timer)

​    }

 

​    render() {

​        return (

​            <View style={S.container}>

 

​                <StatusBar hidden={true} translucent={true}/>

​                <ScrollView horizontal={true} showsHorizontalScrollIndicator={false}

​                            onMomentumScrollEnd={this.move}

​                            ref={'scroll'}

​                            onScrollBeginDrag={this.drag}

​                            onScrollEndDrag={this.end}

​                            pagingEnabled={true}>

​                    <View style={{ width: 375, height: 200, backgroundColor: 'red'}}>

​                    </View>

​                    <View style={{ width: 375, height: 200, backgroundColor: 'orange'}}>

​                    </View>

​                    <View style={{ width: 375, height: 200, backgroundColor: 'blue'}}>

​                    </View>

​                </ScrollView>

​                <View style={S.num}>

​                    {this.createPointer()}

​                </View>

​            </View>

​        );

​    }

}

 

const S = StyleSheet.create({

 

​    container: {

​        position: 'relative',

​    },

​    num: {

​        position: 'absolute',

​        flexDirection: 'row',

​        bottom: 0,

​        width,

​        height: 30,

​        backgroundColor: 'rgba(0,0,0,0.5)',

​    },

​    dot: {

​        flexDirection: 'row',

​        width: 150,

​        height: 30,

​        marginLeft: 180,

 

​        //borderRadius:'50%', backgroundColor: 'white'

 

​    }

})
```

南山科技七