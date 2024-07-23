

# Mquery

<!-- PROJECT LOGO -->
<br />

<p align="center">
    <img src="Mquery.png" alt="Logo" width="255" height="255">
  <h3 align="center">Mquery</h3>
  <p align="center">
    像使用 Jquery 一样，简单使用 MugedaApi
    <br />
    <br />
    <a href="https://github.com/AdhereDesign/MQuery/issues">报告BUG</a>  / <a href="https://github.com/AdhereDesign/MQuery/issues">提出建议</a>
  </p>

</p>

 
## 目录

- [简介](#简介)
  - [使用案例](#使用案例)
  - [安装步骤](#安装步骤)
- [功能说明](#功能说明)
- [作者](#作者)
- [更新日志](#更新日志)
<br>
<br>
<br>
<br>
<br>

## 简介

Mquery用于简化调用MugedaAPI编程<br>
基础版适用于未学习过或有一定JS基础的用户使用<br>
使用 `$("元素")` 即可获取元素，而不需要使用较长代码<br>

### 使用案例
例如获取修改所有元素#1 #2… 的属性

使用JS:

```
let elements = [];
let id = 1;
let element;

while ((element = scene.getObjectByName(`元素#${id}`))) {
    element.top = 100;
    elements.push(element);
    id++;
}
```

使用Mquery:
`$("元素*").top = 100;`

<br><br><br>

例如获取所有元件`元件#1 #2…`并且修改里面的文本

使用JS:

```
    const scene = mugeda.scene; let id = 1; let component;
    while ((component = scene.getObjectByName(`元件#${id}`))) {
        const textElement = component.scene.getObjectByName("文本");
        if (textElement) {textElement.text = "修改值";}id++;
    }
```

使用Mquery:
`$("元件*/文本").text = "修改值"`

<br>
<br>
<br>
<br>
<br>


### 使用Mquery前的注意

1. 对于Mugeda免费用户，根据平台要求，只能发布后才能使用查看带有JS的作品，否则只能在编辑器中查看
2. 对于刚接触Mugeda的用户，不建议使用Mquery，应先完全熟悉Mugeda编辑器
3. Mquery并非完全简化MugedaAPI所有操作，仅为一些基础操作，如复制元素，碰撞，动画，等功能需要自行查阅 [MugedaAPI](https://card.mugeda.com/mugedaApiDoc/index.html) 说明
4. 不规范使用或自己编写的JS代码BUG可能会导致网页浏览器卡死，因此需要注意及时保存
5. 作者不对任何非Mquery问题进行处理
6. 使用Mquery的一切后果由使用者承担
   
<br>
<br>

### 安装步骤

1. 获取Mquery代码 (暂未公布)
2. 根据自己的要求，修改简写表（shorthandMap）
3. 将代码放入![image](https://github.com/user-attachments/assets/ef92261c-5b1e-499e-93dc-180ed254bf60)中
   
<br>
<br>

### 作者

AdhereDesign | Hai_Xii@outlook.com

<br>
<br>

## 功能说明

### 回调函数

在Mugeda中，有多种触发JS的方式，自动回调，手动回调

自动回调一般是使用
```
mugeda.addEventListener("renderready", function () {

//代码部分

}
```
其中，
`renderready` 当动画准备完成，开始播放前的那一刻引发回调

可以更改为:

`imageready` 当动画预加载图片完成后引发回调<br>
`scriptready` 当动画脚本加载完成后引发回调


### 选择元素

`$("元素")` 可快速指定元素，效果等同于 `getObjectByName("命名物体的名字");`

`$("元素*")` 选取所有，仅限于在Mugeda编辑器中，元素名称后面以#1，#2结尾的

`$("元件/元素")` 选取元件内的元素，不支持嵌套，例如 `$("元件/元件/元件/元件/元素") `

支持三种全选，	`$("元件*/元素")`、`$("元件/元素*")`、`$("元件*/元素*")` 

### 获取或修改属性

`$("元素").属性名` 获取元素，可以简写，简写表：

```
        w: 'width',
        h: 'height',
        x: 'x',
        y: 'y',
        l: 'left',
        rgt: 'right',
        tp: 'top',
        btm: 'bottom',
        r: 'rotate',
        sx: 'scaleX',
        sy: 'scaleY',
        rx: 'rotateX',
        ry: 'rotateY',
        rcx: 'rotateCenterX',
        rcy: 'rotateCenterY',
        vb: 'visible',
        t: 'text', 
        a: 'alpha',
        p: 'pers',
        u: 'url',
        // 只读属性
        n: 'name',
        s: 'scene',
        cs: 'currentScene',
        ta: 'thisAni',
        grv: 'getRealVisible',
        aud: 'audio',
        vid: 'video',
        e: 'elements' // 新增简化形式,效果类似dom

```

`var width = $("元素").width` 获取元素属性<br>
` $("元素").width = 100` 修改元素属性<br>

`$("元素").text = $("元素").text + $("元素").text` 字符串(合并字符)<br>
`$("元素").text = $("元素").v + $("元素").v` 计算值(计算取值)<br>

### 监听事件 

`$("文本*").listener('click', function () { this.v++ });`<br>

### 帧动画控制

  `$("元件").pause()`<br>
  `pause()` 可以替换成：<br>
    `pause()`  暂停 <br>
    `play()`  继续播放 <br>
    `ToPlay(frame)`  跳转到帧并播放（frame支持帧号或帧名） <br>
    `ToPause(frame)`  跳转到帧并暂停（frame取值同上） <br>

Frame可以有多种输入方式； <br>
1.指定帧：指定一个数 <br>
2.随机范围：1-15 随机指定:1,2,3,4,5（需要带上" ",例如"1-5"或"1,3,5"）<br>

### 独立控制台

使用 `log()` 可以将信息输出到舞台中的 `console` 元素<br>
需要在配置文件开启`debug`模式<br>


## 更新日志
1.0
```
完成功能：元素选取、元件选取、字符或取值计算、监听、帧控制、控制台、简写表
```
