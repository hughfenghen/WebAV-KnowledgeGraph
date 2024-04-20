# Web 音视频知识图谱

整理（索引） Web 音视频相关的 API、SDK、文章、对外产品，帮助前端开发者入门/进阶音视频领域，推动音视频技术在 Web 平台的应用实践。

## 动机

音视频技术在 Web 平台应用有限，资料也相对较少；  
Web 平台处理音视频的基础能力已具备，但涉及的 API 非常多，熟知 API 间错综复杂关系的开发也很少。

所以，先整理一份音视频相关的 Web API 知识图谱，降低在 Web 平台开发音视频应用的门槛；  
然后，索引互联网公开的文章、工具、开源项目；  
目标是让前端开发初学者也能通过自学，掌握在 Web 平台开发音视频应用的基础技能。

## Web API 图谱

[完整图谱](https://www.processon.com/view/link/661b519329eb742733da24fb?cid=661b50541c0cb632e514c499)

由于 API 太多，为了不干扰阅读，侧重各个模块间的协作（数据转换）对象，许多模块内 API 并没有列出。  
_有人反馈初看图谱感觉很乱，笔者已经尽量简化，若有更好的建议可以提出来。_

### 如何阅读图谱

1. 注意红色高亮节点，它们是不同场景数据转换的核心对象
2. 注意相同颜色的线条，它们串联某些场景下的数据转换循环
3. 以关注的模块为中心，观察节点连线，就能知道**数据能从哪里来（被箭头指向）、数据能到哪里去（箭头指向）**

#### 场景举例

**音视频文件处理**

1. 图中可发现是用 `WebCodecs API` 能解析处理或合成输出音视频文件（封装/接封装需借助第三方库）
2. WebCodecs 最终能得到代表原始音（`AudioData`）视（`VideoFrame`）频数据的对象
3. 若需对音视频内容进行处理（比如图像滤镜或声音变调）则需参考其他可利用 API（观察箭头指向）

**音频处理**

1. 音频处理的核心模块是 `AudioContext`
2. 观察箭头可发现，能通过网络远程加载数据、或将 `html` 的 `video/audio` 标签作为输入源
3. 处理后直接渲染到扬声器或 html 标签中
4. 音频处理相关的 API 被隐藏了，这里只能看到跟 `AudioNode` 相关，感兴趣的同学可进一步深究

**低延迟音视频通信**

1. 低延迟通信跟 `WebRTC` 模块相关
2. `RTCPeerConnection` 下的 `addTrack` 可以发送音视频流到远端，来源可以是从摄像头、html 标签（video/canvas）捕获的流
3. `RTCPeerConnection` 下的 `getReceivers` 可以从远端接收流，输出到 html 标签（video/canvas）播放出来
4. 若发送前、接收后需要对流数据加工处理（如移除视频背景、降噪），则可利用 `MediaStreamTrackProcessor, MediaStreamTrackGenerator` 相关 API

### 图谱概览

<img width="1138" src="https://github.com/hughfenghen/WebAV-KnowledgeGraph/assets/3307051/bc722748-ec7e-4f32-a60b-7d165be3aad6">

## SDK & DEMO

在 Web 平台处理（合成、剪辑、导出）音视频数据开源项目。

- [WebAV](https://github.com/hughfenghen/WebAV): Process audio/video data in the browser using WebCodecs. 基于 WebCodecs 在浏览器中处理音视频数据。
  - 特点：支持硬件加速编解码，速度快、兼容性差，API 友好；丰富的在线可体验 [DEMO](https://hughfenghen.github.io/WebAV/demo/)
- [ffmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm): FFmpeg for browser, powered by WebAssembly
  - 特点：FFmpeg 编译的 WASM 版，兼容性更好、速度慢；[Playground](https://ffmpegwasm.netlify.app/playground)
- [mp4box.js](https://github.com/gpac/mp4box.js): JavaScript version of GPAC's MP4Box tool
  - js 实现的 mp4 muxer/demuxer（封装/解封装） SDK
  - [文档](https://gpac.github.io/mp4box.js/)包含在线 DEMO，其中 [inspection tool](https://gpac.github.io/mp4box.js/test/filereader.html) 在线解析视频文件（mp4、m4a、mov）信息，特别方便好用
- [hls.js](https://github.com/video-dev/hls.js): HLS.js is a JavaScript library that plays HLS in browsers with support for MSE. [DEMO](https://hlsjs.video-dev.org/demo/)
- [howler.js](https://github.com/goldfire/howler.js): Javascript audio library for the modern web.
- [opfs-tools](https://github.com/hughfenghen/opfs-tools): A simple, high-performance, and comprehensive file system API running in the browser, built on OPFS. 在浏览器中运行的简单、高性能、完备的文件系统 API，基于 OPFS 构建。[DEMO](https://hughfenghen.github.io/opfs-tools-explorer/)
  - 音视频开发经常需要高频读写文件或处理大型文件，可能需要 OPFS API 来提高性能、降低内存消耗。

官方 DEMO

- [WebCodecs samples](https://w3c.github.io/webcodecs/samples/)
- [WebRTC samples](https://webrtc.github.io/samples)

## 文章

- 风痕的博客 [Web 音视频入门系列](https://hughfenghen.github.io/tag/WebCodecs/)
- 张鑫旭博客 [audio](https://www.zhangxinxu.com/wordpress/tag/audio/), [video](https://www.zhangxinxu.com/wordpress/tag/video/)
- [Waveforms](https://pudding.cool/2018/02/waveforms/)：可视化、交互式探索声音的形状
- [Learning Synths](https://learningsynths.ableton.com/en/get-started)：可视化学习音乐合成
- [Video processing with WebCodecs](https://developer.chrome.com/docs/web-platform/best-practices/webcodecs)

## 工具

- [FFmpeg](https://ffmpeg.org/): A complete, cross-platform solution to record, convert and stream audio and video.
  - 功能很强大、命令行参数很复杂，不会就问 ChatGPT
- [MP4 inspection tool](https://gpac.github.io/mp4box.js/test/filereader.html) 在线解析视频文件（mp4、m4a、mov）信息

## 产品

能在浏览器中运行的音视频产品。

- [剪映网页版](https://www.capcut.cn/web)：字节的视频剪辑产品
- [Scenery.video](https://scenery.video)：多人协同视频剪辑
- [Video tools. Online](https://clideo.com/)
- [花影](https://github.com/hughfenghen/bloom-shadow)：在浏览器中运行的录屏工具，可用于视频课程制作、直播推流工作台；基于 WebAV 实现

## 笔者简介

笔者花名**风痕**，大概做了 4 年 Web 音视频相关产品，2023 年初开始重点投入 WebCodecs，看好该技术应用前景。  
所以创建了当前项目，希望为 Web 音视频技术的应用与实践贡献力量。

此外，笔者还在积极维护 [WebAV](https://github.com/hughfenghen/WebAV)、[opfs-tools](https://github.com/hughfenghen/opfs-tools) 两个音视频相关项目，[个人博客](https://hughfenghen.github.io/)也会长期更新 Web 音视频相关文章。

_若你对该项目的内容感兴趣，可 Star 或转发给需要的同学。_  
_你也可以通过 issue 推荐内容（SDK、文章、工具）、提交反馈，与笔者一起完善该项目。_
