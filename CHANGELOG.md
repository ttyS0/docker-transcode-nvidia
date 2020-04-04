## 0.3.0 (2020-04-03)

* started with a copy of [jrottenberg/ffmpeg/docker-images/4.2/nvidia1804/Dockerfile](https://github.com/jrottenberg/ffmpeg/blob/master/docker-images/4.2/nvidia1804/Dockerfile)
* removed various FFmpeg compile targets, such as X11 components
* added `mpv`, `mkvpropedit`, and `other-transcode`
* changed the `ENTRYPOINT` to be `other-transcode`

