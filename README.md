
# Prism - H.264 decoder in pure javascript 

## 20180607
这个是同济的一个牛逼同学16年的设计，看起来是手工将解码器js化了。
实际测试，能解码，VGA单帧在40ms左右，但是很奇怪视频输出不连贯，我尝试用requestAnimationFrame包装了渲染部分，依然如此。

这个我很喜欢，我以前也尝试手工将 ARUCO的js代码C语言化，对于用心的设计很尊重。

可以配合 h264-live-player 的后端做测试

尚未联系到该同学，暂时搁置。



<img align="" height="200" src="http://cdn.cloudwarehub.com/42.pic_hd.jpg"> 

Logo by **Jiangnan Zhuang**

Prism is a H.264 decoder written in javascript(ES5), which is used in browser to decode H.264 stream data into RGBA/YCbCr format frames.

Prism can run in browsers support javascript ES5 or higher standard, and support H.264 realtime decoding profile which contains I/P frames.

Prism is a project of [CloudwareHub](http://www.cloudwarehub.com), aiming at providing cross platform video stream decoder.

----

## Build

Prism depends on [Node.js](http://nodejs.org/), [npm](http://npmjs.org/), [gruntjs](http://gruntjs.com/). 
Execute commands below to build prism, and the built file prism.min.js should be generated in build/ folder.
```
$ npm install
$ bower install
$ grunt
```
## Usage

Prism uses [requirejs/almod](https://github.com/requirejs/almond) to package, and export `window.prism` if not in AMD context.
The typical usage of prism should work with websocket, just read raw H.264 nal data from server via websocket and feed into prism, then prism will decode every frame into RGBA/YCbCr format pictures.
Sample code is as follows:
```
ws.onmessage = function(msg) {
  prism.decodeNal(msg);
  console.log(prism.SL) // decoded frame luma in xy format
  console.log(prism.SCb, prism.SCr) //decoded frame chroma cb/cr in xy format
}
```
The demo of prism is available at [CloudwareHub](http://www.cloudwarehub.com).
## License
BSD-2-Clause

## Resources
[H.264 standard](https://www.itu.int/rec/T-REC-H.264)

