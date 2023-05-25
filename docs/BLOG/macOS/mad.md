# MAD production workflow on macOS

## Conclusion

### Extract and Format

- origin: `mkv (HEVC & FLAC)`
- mkvextract: `HEVC` `FLAC`
- (Permute: edit FLAC with wrong timestamp)
- ffmpeg: `ALAC`
- mp4box: `mp4 (HEVC & ALAC)`

### Import

For me, a MAD producer, import `mp4 (HEVC & ALAC)` into FCP (copy original media to library) and then create proxy media with `mov (ProRes 422 Proxy & PCM)`.

#### Advantages

* **Output with the best quality** What I import has the best quality. So, output has the least loss. I can even use ProRes 422 or ProRes 422 HQ to export my project.
* **Great performance when editing video** The performance will be satisfying by creating proxy media instead of directly using original media to edit.
* **Less space and Faster encoding time** Contrast to ProRes 422, encoding ProRes 422 Proxy is faster and spends less space. Creating proxy media also allows me to use half frame size, which save storage more. Also I can delete all proxy files after finishing the project without affecting original media. After deleting these proxy media, if I want to restart the project I can easily recreate proxy media.
* **No error if original media disappear** I choose the option `copy to library` so I won't be worried if original media moved or deleted. 

### Export

#### Upload

`mp4 (HEVC & AAC)` with the best quality

#### Archive

`mov (ProRes 422 & PCM)` with the best quality

## Original Media

`mkv (HEVC & FLAC)`

incompatible with Compressor and FCPX

## Transcode and Re-format

- mkvextract: `HEVC` `FLAC`
- (Permute: edit FLAC with wrong timestamp)
- ffmpeg: `ALAC`
- mp4box: `mp4 (HEVC & ALAC)`

**See script at **[my GitHub repo](https://github.com/Yang-Xijie/mkv2mp4_fcp)

## Import

### Import only

not recommend

### Transcode then Import

Compressor: `mov (ProRes 422 / ProRes 422 LT / Prores 422 Proxy & PCM)`

If you really concern about the quality, use `ProRes 422` or `ProRes 422 HQ`. Otherwise if you don't have enough disk storage, `ProRes 422 LT` or `ProRes 422 Proxy` is also good for video editing.

### Import then Create proxy media

FCPX: Create proxy media `mov (ProRes 422 Proxy & PCM (less bits))` with the same/lower frame size.

## Export

### Upload

`mp4 (HEVC & AAC)` both the best quality, automatic

### Archive

`mov (ProRes 422 / ProRes 422 LT & PCM)`

## References

- [About Apple ProRes](https://support.apple.com/en-us/HT202410)
- [关于 Apple ProRes](https://support.apple.com/zh-cn/HT202410)
- [Media formats supported in Final Cut Pro](https://support.apple.com/guide/final-cut-pro/supported-media-formats-ver2833f855/mac)
- [Create optimized and proxy files in Final Cut Pro](https://support.apple.com/guide/final-cut-pro/create-optimized-and-proxy-files-verb8e5f6fd/mac)
- [What's new in FCP 10.5](https://larryjordan.com/articles/final-cut-pro-x-new-improved-proxy-workflow/)