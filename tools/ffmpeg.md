ffmpeg
======
**Convert `MTS` to `mp4`**

```
cp /Volumes/NO\ NAME/PRIVATE/AVCHD/BDMV/STREAM/* .
rm -rf /Volumes/NO\ NAME/PRIVATE/AVCHD
ffmpeg -i concat:"00001.MTS|00004.MTS|00005.MTS" -vcodec copy -acodec copy result.mp4
```
