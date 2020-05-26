## 0.3.1 (2020-05-26)

* bumpeg other_transcode to v0.3.1

## 0.3.0-2 (2020-05-22)

* bumped ffmpeg to v4.2.3

## 0.3.0-1 (2020-05-05)

* removed VAAPI compile flag, since there's [another container](https://github.com/ttyS0/docker-transcode-vaapi) for that
* added `--enable-cuda-sdk` to ffmpeg configure based on https://github.com/jrottenberg/ffmpeg/pull/234

## 0.3.0 (2020-04-03)

* started with a copy of [jrottenberg/ffmpeg/docker-images/4.2/nvidia1804/Dockerfile](https://github.com/jrottenberg/ffmpeg/blob/master/docker-images/4.2/nvidia1804/Dockerfile)
* removed various FFmpeg compile targets, such as X11 components
* added `mpv`, `mkvpropedit`, and `other-transcode`
* changed the `ENTRYPOINT` to be `other-transcode`

