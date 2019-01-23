# DragableGridview
[![pub package](https://img.shields.io/pub/v/dragablegridview_flutter.svg)](https://pub.dartlang.org/packages/dragablegridview_flutter)

用GridView编写的可拖动排序View，可任意拖动位置.长按触发拖动，拖动到其他Item上时触发动画，为被拖动的Item腾出空间。松开手指重新排序

A dragable gridview,Long-pressed triggers draggable state,When  dragging until covere other items, other Items trigger the animation to make room for the draggable Item,GridView reordering after release your finger

HomePage：[https://github.com/baoolong/DragableGridview](https://github.com/baoolong/DragableGridview)

MoreWidght：[https://github.com/OpenFlutter/PullToRefresh](https://github.com/OpenFlutter/PullToRefresh)

<img width="38%" height="38%" src="https://raw.githubusercontent.com/OpenFlutter/PullToRefresh/master/demonstrationgif/20180821_094948.gif"/>

## Usage

Add this to your package's pubspec.yaml file:

	dependencies:
	  dragablegridview_flutter: ^0.1.3
	  
Add it to your dart file:

    import 'package:dragablegridview_flutter/dragablegridview_flutter.dart';
    
And GridView dataBin must extends DragAbleGridViewBin ,Add it to your dataBin file 
    
    import 'package:dragablegridview_flutter/dragablegridviewbin.dart';
    
## Example

#### DataBin example (must extends DragAbleGridViewBin)

    import 'package:dragablegridview_flutter/dragablegridviewbin.dart';
    
    class ItemBin extends DragAbleGridViewBin{
    
      ItemBin( this.data);
    
      String data;
    
      @override
      String toString() {
        return 'ItemBin{data: $data, dragPointX: $dragPointX, dragPointY: $dragPointY, lastTimePositionX: $lastTimePositionX, lastTimePositionY: $lastTimePositionY, containerKey: $containerKey, containerKeyChild: $containerKeyChild, isLongPress: $isLongPress, dragAble: $dragAble}';
      }
    
    }

#### Widget Usage Example

    import 'package:dragablegridview_flutter/dragablegridview_flutter.dart';
    import 'package:flutter/material.dart';
    
    import 'gridviewitembin.dart';
    
    
    class DragAbleGridViewDemo extends StatefulWidget{
      @override
      State<StatefulWidget> createState() {
        return new DragAbleGridViewDemoState();
      }
    
    }
    
    class DragAbleGridViewDemoState extends State<DragAbleGridViewDemo>{
    
      List<ItemBin> itemBins=new List();
      String actionTxtEdit="编辑";
      String actionTxtComplete="完成";
      String actionTxt;
      var editSwitchController=EditSwitchController();
    
      @override
      void initState() {
        super.initState();
        actionTxt=actionTxtEdit;
        itemBins.add(new ItemBin("鲁班"));
        itemBins.add(new ItemBin("虞姬"));
        itemBins.add(new ItemBin("甄姬"));
        itemBins.add(new ItemBin("黄盖"));
        itemBins.add(new ItemBin("张飞"));
        itemBins.add(new ItemBin("关羽"));
        itemBins.add(new ItemBin("刘备"));
        itemBins.add(new ItemBin("曹操"));
        itemBins.add(new ItemBin("赵云"));
        itemBins.add(new ItemBin("孙策"));
        itemBins.add(new ItemBin("庄周"));
        itemBins.add(new ItemBin("廉颇"));
        itemBins.add(new ItemBin("后裔"));
        itemBins.add(new ItemBin("妲己"));
        itemBins.add(new ItemBin("荆轲"));
      }
    
      @override
      Widget build(BuildContext context) {
        return new Scaffold(
          appBar: new AppBar(
            title: new Text("可拖拽GridView"),
            actions: <Widget>[
              new Center(
                  child: new GestureDetector(
                    child: new Container(
                      child: new Text(actionTxt,style: TextStyle(fontSize: 19.0),),
                      margin: EdgeInsets.only(right: 12),
                    ),
                    onTap: (){
                      changeActionState();
                      editSwitchController.editStateChanged();
                    },
                  )
              )
            ],
          ),
          body: new DragAbleGridView(
            decoration: new BoxDecoration(
              borderRadius: BorderRadius.all(new Radius.circular(3.0)),
              border: new Border.all(color: Colors.blue),
            ),
            mainAxisSpacing:10.0,
            crossAxisSpacing:10.0,
            deleteIconName: "images/close.png",
            deleteIconMarginTopAndRight: 6.0,
            itemPadding: EdgeInsets.fromLTRB(8.0, 5.0, 8.0, 5.0),
            childAspectRatio:1.8,
            crossAxisCount: 4,
            itemBins:itemBins,
            editSwitchController:editSwitchController,
            child: (int position){
              return new Text(
                itemBins[position].data,
                style: new TextStyle(fontSize: 16.0,color: Colors.blue),);
            },
            editChangeListener: (){
              changeActionState();
            },
          ),
        );
      }
    
      void changeActionState(){
        if(actionTxt==actionTxtEdit){
          setState(() {
            actionTxt=actionTxtComplete;
          });
        }else{
          setState(() {
            actionTxt=actionTxtEdit;
          });
        }
      }
    }

## Notice

No Notice

## LICENSE
    MIT License

	Copyright (c) 2018
	
	Permission is hereby granted, free of charge, to any person obtaining a copy
	of this software and associated documentation files (the "Software"), to deal
	in the Software without restriction, including without limitation the rights
	to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
	copies of the Software, and to permit persons to whom the Software is
	furnished to do so, subject to the following conditions:
	
	The above copyright notice and this permission notice shall be included in all
	copies or substantial portions of the Software.
	
	THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
	IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
	FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
	AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
	LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
	OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
	SOFTWARE.
