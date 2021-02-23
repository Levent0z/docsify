# Noise Reduction in Video

1. Save video only
https://support.apple.com/guide/quicktime-player/remove-audio-or-video-qtp5a44f7279/mac

2. Open audio in Audacity
https://www.audacityteam.org/
(You'll have to install ffmpeg audio encoders, use Preferences > Libraries > FFMpeg )


3. Install ffmpeg
```sh
brew install ffmpeg
```

```sh
ffmpeg -i "video-only.mov" -i "audio.m4a" -c:v copy -c:a copy movie.mov
```


Reference
https://filmora.wondershare.com/video-editing-tips/remove-background-noise-from-video.html
http://howto-pages.org/ffmpeg/