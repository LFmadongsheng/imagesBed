# Cookie



全部后台处理 当前端静态资源与后端接口产生跨域的情况下，后台两步 一步设置cookie 然后读取cookie

当跨域的时候前端代码增加两行代码

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180918161951.png)

后台代码

设置cookie

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/new%20image%20-%206eqj0.jpg)

读取cookie

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/new%20image%20-%20ci2vq.jpg)


当跨域产生时，前端访问的当前域下可能是没有cookie的 比如

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180918162609.png)

但是 chrome下设置里面  ——> 高级 ——> 内容设置——>cookie

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180918162914.png)

发现他是有了的 并且后端的可以读取到 。
