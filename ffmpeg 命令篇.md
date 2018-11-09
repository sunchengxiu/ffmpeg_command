# ffmpeg_command
ffmpeg 命令总结

### 1.录屏

#### 1.1 在 macOS 下查看设备

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

#### 1.2 录屏命令

`ffmpeg -f avfoundation -i 1 -r 30 screen.yuv`

### 2.播放录制的文件

`ffplay -s 2880x1800 -pix_fmt  uyvy422  screen.yuv`

或者

`ffplay -video_size 2880x1800 -pixel_format  uyvy422  screen.yuv`