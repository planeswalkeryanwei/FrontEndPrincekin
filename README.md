# FrontEndPrincekin
比崽子们好好看好好学

### css中的[]
- span[class='test']

=>匹配所有带有class类名test的span标签

- span[class *='test']

=>匹配所有包含了test字符串的class类名的span标签

- span[class]

=>匹配所有带有class属性的span标签

- [class='all']

=>匹配页面上所有带有class='all'的标签

- [class *='as']

=>匹配页面上所有class类且类名带有as字符串的类的标签

<!-- ### Flutter

- [**推荐 4 个基于 Flutter 的重磅高仿开源项目**](https://github.com/FrontEndGitHub/FrontEndGitHub/issues/25)
- 精彩待续。。。

| 网站 | 说明 |
| --- | --- |
| [dy_flutter](https://github.com/yukilzw/dy_flutter) | 斗鱼 APP |
| [flutter_tiktok](https://github.com/mjl0602/flutter_tiktok) | 精仿抖音 |
| [flutter-osc](https://github.com/yubo725/flutter-osc) | 开源中国客户端 |
| [FlutterDouBan](https://github.com/kaina404/FlutterDouBan) | 豆瓣客户端 |
 -->

### createDocumentFragment()用法总结
- 写的非常详细易懂，createDocumentFragment方法是创建空的文档碎片，可以为其添加真实DOM节点，而createElement是创建真正DOM节点，同时会有变量接收例如var div =...，所以可以多次修改节点的数值，因为操作的就是实际的页面DOM元素，但是createDocumentFragment不同，他更像是一个容器类似于Vue语法中template，但是他没有 `` 这个语法来识别变量，所以一旦节点通过appendChild等属性加入到文本碎片中，就无法修改了，变成死数据了，如作者4的（3）中所说，由此体现出他们的部分优缺点，因为createElement每次增加元素都是在操作真正的DOM，容易导致页面的重绘与回流（重排），这样会造成很大的开销，但是createDocumentFragment能够避免这个问题，如果是多个标签加入，他们先将他们加入到createDocumentFragment创建的文档碎片中（这步是在数据层面操作，而不是真正操作DOM，所以不会导致重绘和回流），当全部操作完成的时候，最后appendChild（fragment）,这样页面只会进行一次重绘或者回流，相比直接操作DOM，降低了不少开销，所以在性能方面fragment更优秀，但是不能重复操作DOM是他的缺陷，所以还是需要根据业务场景


### 尽量减少多次修改DOM样式 最好一次性修改DOM的样式

比如下面的代码

const el = document.querySelector('#el')
el.style.backgroundColor = 'skyblue'
el.style.opicity = 0.5
el.style.width = 300 + 'px'
1
2
3
4
在之前提到过，浏览器是会将这些重绘与回流操作加入到队列中的，所以可能其最后只会执行一次，但是这里我改变了width，也就是会强制渲染并清空队列的属性，这时候就会触发三次回流与重绘，因此尽可能的将多次修改DOM样式合并成一次

可以使用cssText将其合并:

const el = document.querySelector('#el')
el.style.cssText += 'background-color: skyblue; opicity: 0.5; width: 300px;';
1
2
也可以通过添加class来实现:

.test {
    background-color: skyblue; 
    opicity: 0.5; 
    width: 300px;
}
1
2
3
4
5
const el = document.querySelector('#el')
el.className += ' test'
