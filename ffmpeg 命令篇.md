	# ffmpeg 命令，录屏，播放，提取视频 yuv，提取音频 pcm,滤镜命令,裁剪与合并命令,图片和视频互转命令
ffmpeg 命令总结

### 1.录屏

##### 1.1 在 macOS 下查看设备

` ffmpeg -f avfoundation -list_devices true -i ""`

输出 ：

```
ffmpeg version 4.1 Copyright (c) 2000-2018 the FFmpeg developers
  built with Apple LLVM version 10.0.0 (clang-1000.11.45.5)
  configuration: --prefix=/usr/local/Cellar/ffmpeg/4.1 --enable-shared --enable-pthreads --enable-version3 --enable-hardcoded-tables --enable-avresample --cc=clang --host-cflags= --host-ldflags= --enable-ffplay --enable-gpl --enable-libmp3lame --enable-libopus --enable-libsnappy --enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265 --enable-libxvid --enable-lzma --enable-opencl --enable-videotoolbox
  libavutil      56. 22.100 / 56. 22.100
  libavcodec     58. 35.100 / 58. 35.100
  libavformat    58. 20.100 / 58. 20.100
  libavdevice    58.  5.100 / 58.  5.100
  libavfilter     7. 40.101 /  7. 40.101
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  3.100 /  5.  3.100
  libswresample   3.  3.100 /  3.  3.100
  libpostproc    55.  3.100 / 55.  3.100
[AVFoundation input device @ 0x7f8698d041c0] AVFoundation video devices:
[AVFoundation input device @ 0x7f8698d041c0] [0] FaceTime HD Camera
[AVFoundation input device @ 0x7f8698d041c0] [1] Capture screen 0
[AVFoundation input device @ 0x7f8698d041c0] [2] Capture screen 1
[AVFoundation input device @ 0x7f8698d041c0] AVFoundation audio devices:

```

可以看到 video devices ：

```
[AVFoundation input device @ 0x7f8698d041c0] AVFoundation video devices:
[AVFoundation input device @ 0x7f8698d041c0] [0] FaceTime HD Camera
[AVFoundation input device @ 0x7f8698d041c0] [1] Capture screen 0
[AVFoundation input device @ 0x7f8698d041c0] [2] Capture screen 1
[AVFoundation input device @ 0x7f8698d041c0] AVFoundation audio devices:

``` 

##### 1.2 录屏命令

`ffmpeg -f avfoundation -i 1 -r 30 screen.yuv`

### 2.播放录制的文件

`ffplay -s 2880x1800 -pix_fmt  uyvy422  screen.yuv`

或者

`ffplay -video_size 2880x1800 -pixel_format  uyvy422  screen.yuv`

<<<<<<< HEAD

### 3.提取合并音视频

提取视频： `ffmpeg -i killer.mp4 -an -vcodec copy out.h264`

			`ffmpeg -i test.mp4 -pix_fmt yuv420p v.yuv`
			
		  `ffmpeg -i 2018.mp4 -codec copy -bsf: h264_mp4toannexb -f h264 tmp.264`
```
-i 2018.mp4：  是输入的MP4文件

-codec copy： 从mp4中拷贝

-bsf: h264_mp4toannexb： 从mp4拷贝到annexB封装

-f h264： 采用h264格式

tmp.264： 输出的文件

```

提取音频：`ffmpeg -i killer.mp4 -acodec copy -vn -y out.flv`


播放：`ffmpeg -i test.mp4 -pix_fmt yuv420p v.yuv`

合并：`ffmpeg -i v.mp4 -i a.aac -acodec copy -vcodec copy mix.mp4`
=======
### 3.ffmpeg 提取 yuv 数据

`ffmpeg -i out.mp4 -an -c:v rawvideo -pix_fmt yuv420p out.yuv`

-an:不要音频

-c:v:对视频进行编码，使用 rawvideo 原始视频进行编码

-pix_fmt:像素格式，yuv420p


播放 yuv 视频 ： ffplay -video_size 3360x2100  out.yuv


### 4.ffmpeg 提取 pcm 数据

##### 4.1 提取 pcm 数据


`ffmpeg -i 1.mp4 -vn -ar 44100 -ac 2 -f s16le out.pcm`

```
	-ar：音频的采样率 44100
	
	-ac2:双声道
	
	-f ： 音频的数据存储格式 
	
	s16le : s 代表 有符号的，有正有负，16 代表每一个数值用16位表示 
	
```


##### 4.2 播放 pcm 数据

`ffplay -ac 2 -ar 44100 -f s16le out.pcm`
	
### 5 滤镜命令

`ffmpeg -i 1.mp4 -vf crop=in_w-200:in_h-200 -c:v libx264 -c:a copy out1.mp4`


```
-vf： 视频滤镜 
crop=in_w-200:in_h-200 :
in_w:本身视频的宽度-200
in_h:本身视频的高度-200

-c:v:视频的编码

```

### 6 裁剪和合并命令

##### 6.1 裁剪


` ffmpeg -i 1.mp4 -ss 00:00:02 -t 3 out.ts`

```
-ss : 视频的其实时间

-t : 时长
```

##### 6.2 合并

` ffmpeg -f concat -i input.txt put.mp4`

```
-f concat : 告诉 ffmpeg 将后面的文件合并到一起

input.txt : 要合并的列表
file '1.ts'
file '2.ts'
```

### 7 图片与视频互转命令

##### 7.1 视频转图片

`ffmpeg -i 1.mp4 -r 1 -f image2 image-%3d.jpeg`


```
-r 1 :帧率，每秒钟转出一张图片

-f : 将输入文件 转成 image2
```


##### 7.2 图片转视频

` ffmpeg -f image2 -i image-%3d.jpeg  -vcodec libx264 image.mp4`


	
	
	
	
>>>>>>> 0f3516e2ea1e8dbd528b8bfb7075df8d8dd45005
