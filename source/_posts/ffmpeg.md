---
title: ffmpeg
date: 2016-11-30 13:04:14
tags: [video,dev]
---

## 相关链接
* 需求wiki ：http://172.30.10.223/x/IQEVAQ
* download： 
    * win https://ffmpeg.org/download.html
    * linux http://johnvansickle.com/ffmpeg/releases/ffmpeg-release-64bit-static.tar.xz
* doc:https://ffmpeg.org/ffmpeg.html
* demo： http://my.oschina.net/273579540/blog/111060

Cmd Example：
> ffmpeg -y -i foo.mp4 -vframes 1 -r 1 -ac 1 -ab 2 -s 320x240 -f image2 lh.jpg

## 实现过程
java调用命令行，并接收输出流，解析成Po。不同的参数对应不同的输出流，可以解析成不同的Po。目前只需要名称、时长，分辨率属性，以后按需扩展。