# yt-dlp

yt-dlp[^1] 比 youtube-dl 還好用的 Youtube Downloader，個人常用 yt-dlp 指令組合整理


## Best video

下載最佳（重新定義）格式，Remux 成 mp4，將影片封面、標題及描述嵌入 tag，依照「上傳年月日+標題（最大長度32）+ Youtube-ID」方式命名

```bash
yt-dlp -S 'res,fps,vcodec:av01,abr,asr,acodec:flac,proto,br,id' -f 'bv*+ba/b' --remux-video 'mp4' --embed-thumbnail --embed-metadata -o '[%(upload_date)s] %(title).32s [%(id)s].%(ext)s' $URL
```


## Audio opus & m4a

同時下載最佳 opus + 最佳 m4a 雙格式，將影片封面、標題及描述嵌入 tag，依照「上傳年月日+標題（最大長度32）+ Youtube-ID」方式命名

```bash
yt-dlp -f 'ba[acodec^=opus],ba[acodec^=mp4a]' -x --embed-thumbnail --embed-metadata -o '[%(upload_date)s] %(title).32s [%(id)s].%(ext)s' $URL
```


## Browser cookie

下載須登入的影片（年齡限制、會員專屬）加入以下參數

```bash
--cookies-from-browser vivaldi
```

[^1]: https://github.com/yt-dlp/yt-dlp
