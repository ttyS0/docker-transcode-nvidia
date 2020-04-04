# docker-transcode-nvidia

## About

[Don Melton](http://donmelton.com/) of [Video Transcoding](https://github.com/donmelton/video_transcoding) renown
has brought hardware acceleration to bear in the form of [Other Video Transcoding](https://github.com/donmelton/other_video_transcoding). While Don has well
covered the installation and usage of `other-transcode` for all normal desktop platforms, this repository's focus is using `other-transcode` as a Docker container.

I have leaned _heavily_ on [Julien Rottenberg's](https://github.com/jrottenberg) [ffmpeg](https://github.com/jrottenberg/ffmpeg) Dockerfiles. Basically I've taken them, pulled out some of the extraneous `ffmpeg`
compile options, added in the `other-transcode` dependencies, and finally bundled in `other-transcode` itself.

Hardware acceleration being hardware dependent, I again stole an idea from [Julien Rottenberg's](https://github.com/jrottenberg)
repositories, and narrowed the scope of each container to a specific hardware target. This container is for NVidia
GPUs, and leverages [NVENC](https://en.wikipedia.org/wiki/Nvidia_NVENC).

The container image version is hard aligned to `other-transcode`, with numerical suffixes representing container
modifications not directly related to `other-transcode` such as changes in `FFmpeg` compile options.


## Usage

In its current form, this container is intended to be used to directly run `other-transcode` as a container.
As such, the the [nvidia-docker](https://github.com/NVIDIA/nvidia-docker) runtime must be installed, as well as the current directory bind mounted. In order to
keep `other-transcode` from attempting to overwrite the source file that's being transcoded, the current working directory is considered the `output` directory, and source file(s) are placed in a
child directory. In short something like this:

```
output_dir
\_source_dir
  \_source_file.mkv
```

where `output_dir` is `$(pwd)`. Using that setup, to transcode `source_file.mkv`:

```
cd output_dir
docker run --runtime=nvidia -v $(pwd):$(pwd) -w $(pwd) \ 
  ttys0/other-transcode-nvidia \
  source_dir/source_file.mkv
```

If you want to pass `other-transcode` options, do so just as if `other-transcode` was being run outside of the
container. For example, to target a bitrate of 2000 the above example would look like this:

```
cd output_dir
docker run --runtime=nvidia -v $(pwd):$(pwd) -w $(pwd) \
  ttys0/other-transcode-nvidia \
  --hevc --nvenc-temporal-aq source_dir/source_file.mkv
```

## Potential Problems

* As I try to shave down the required FFmpeg compile options to only those that get used in video transcoding, I  may inadvertently remove some that are actually needed. If you find a codec missing that is "normally" available with `FFmpeg` please make an issue, and I'll add it back in.
