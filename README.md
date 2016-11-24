# FMmusic


## 线上预览网址：http://wkfmmusic.applinzi.com/；
## 新浪云：1031666476@qq.com；
## 分支：sae master:4
## 新浪云远程库地址：```$ git remote add sae https://git.sinacloud.com/wkfmmusic```


#### 在```audio```中放了好几个```source```，为什么运行时只播放第一个音频就停止了？添加```audio```的```loop```属性也只是使其第一个循环播放。
- audio标签的source属性不是说第一个播放完播放第二个，它是用来兼容浏览器的。不同浏览器兼容html5的播放格式是不同的。简单的说，如果浏览器第一个无法播放会用第二个，第二个不行就用第三个。目前html5只支持三种播放格式。基本上两种就能兼容全部浏览器。
  而想要播放完第一个播放第二个应该要写js来控制加载。
#### 如何使其在播放完第一段音频时继续播放下一段？
- 不要设定```audio```的```loop```属性，当音频播放结束时即可触发```ended```事件。监听该事件，改变```audio.src```的值并通过```audio.load```方法重新加载音频并播放。应该注意的时要设定```audio```的```autoplay```属性；
- ```
audio.addEventListener('ended', function() {
    audio.src = "../MP3/music (2).mp3";
    audio.load();
})```

#### 进度条完整功能
- 显示已播放时间、全部时长；
- 显示进度；
- 可拖动控制钮调整进度；
- 可点击进度条调整进度且进度条随之改变，注意点击区域应足够宽。

#### 音量控制功能
- 点击```volume-button```可实现静音/取消静音效果；
 - 静音改变同时图标也发声变化；
 - 取消静音后音量恢复之前大小
- 显示音量的进度条；
- 可拖动```volume-handle```控制音量大小；
- 可点击进度条改变音量大小；
- （待定）当鼠标放在```volume```元素上时，可服滚动滚轮控制音量。

#### 黑胶旋转功能
- 音频播放时唱针转至唱片上，唱片旋转；
- 唱片中心封面为歌曲图片，随着歌曲改变而改变；
- 音频播放时唱片旋转，唱针在唱片上；暂停时唱片停止转动，唱针移开；
- 歌词显示按钮可控制唱片消失（歌词显示）和出现（歌词消失）。

#### CSS3 的动画功能的使用(范例)
```
@keyframes rotate {
    0% {
        -webkit-transform: rotate(0deg);
        -moz-transform: rotate(0deg);
    }
    100% {
        -webkit-transform: rotate(360deg);
        -moz-transform: rotate(360deg);
    }
}
#fm .colorful-min {
        animation-name: rotate;
        animation-duration: 7s;
        animation-timing-function: linear;
        animation-fill-mode: forwards;
        animation-direction: normal;
        animation-iteration-count: infinite;
        color: #fff;
        text-shadow: 0 0 10px #fff;
}
```

#### 鼠标点击事件```click```和拖拽事件的冲突（即```mouse down```和```mouse up```事件)
- ```click```事件在```mouse up```事件发声时触发，通过设一个布尔值参数，在```mouse down``` 和``` mouse up ```事件之间改变其值，监听到```click```事件时判断此```click up```是点击后的还是拖动后的。

```
    var isMoving = true;

    $node.on('click',function() {
        if (!isMoving) {
            // do something
        }
    })

    $node.on('mousemove', function() {
        isMoving = true;
    });
    $node.on('mouseup'', function() {
        isMoving = false;
    });

```
