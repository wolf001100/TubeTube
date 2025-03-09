![Logo](tubetube/static/tubetube.png)


**TubeTube** 是一个好用的YouTube下载器


## Features:
- **多线程下载**
- **可定制下载格式** 
- **移动端UI** 
- **支持直播流**


## Docker Compose 范例：

Create a `docker-compose.yml` file:

```yaml
services:
  tubetube:
    image: ghcr.io/mattblackonly/tubetube:latest
    container_name: tubetube
    ports:
      - 6543:6543
    volumes:
      - /path/to/general:/data/General
      - /path/to/music:/data/Music
      - /path/to/podcasts:/data/Podcast
      - /path/to/videos:/data/Video
      - /path/to/config:/config
      - /path/to/temp:/temp # 可选 临时文件会在重启时删除
      - /etc/localtime:/etc/localtime:ro # 可选. 跟主机同步时间
      - /etc/timezone:/etc/timezone:ro # 可选，跟主机同步时区
    environment:
      - PUID=1000
      - PGID=1000
    restart: unless-stopped
```


## 目录设置：

在/path/to/config目录里创建一个setting.yaml，内容为：

```yaml
General:
  audio_ext: m4a
  audio_format_id: '140'
  video_ext: mp4
  video_format_id: '625'
Music:
  audio_ext: mp3
  audio_format_id: '140'
Podcast:
  audio_ext: m4a
  audio_format_id: '140'
Video:
  audio_format_id: '140'
  video_ext: mp4
  video_format_id: '625'

```


### 注解:

- 把'/path/to/general'替换为你需要的路径
- 确认'setting.yaml'在'/path/to/config'目录里
- 'docker-compose.yml'里的目设置要和'settings.yaml'里一致
- 你可以在'settings.yaml'使用多个目录，请确保跟'docker-compose.yaml'一致
- 如需要使用cookie，请在'/path/to/config'里创建cookies.txt

#### 字幕设置

- 当'WRITE_SUBS=True'时，下载的时候创建单独的字幕文件。如果没有字幕可用，就不会创建。
- 当'ALLOW_AUTO_SUBS=True'时，将默认单独创建字幕文件。
- 当'EMBED_SUBS=True'时，字幕文件给将会内封进视频文件。如果没有字幕可用，就不会内封。
- 当'ALLOW_AUTO_SUBS=True'时，将默认内封字幕文件。
- 当'ALLOW_AUTO_SUBS'和'WRITE_SUBS'或者'EMBED_SUBS'搭配使用时，下载器将尝试下载字幕，如果没有字幕可用，下载器将下载“实时翻译字幕”


## 环境变量设置


```yaml
environment:
  - PUID=1000                       # 用户ID(默认: 1000)
  - PGID=1000                       # 组ID(默认: 1000)
  - VERBOSE_LOGS=false              # 详细日志模式(默认：关闭)
  - TRIM_METADATA=false             # 提取元数据(默认: 关闭)
  - PREFERRED_LANGUAGE=en           # 偏好语言(默认: 英语)
  - PREFERRED_AUDIO_CODEC=aac       # 偏好音频编码 (默认: aac)
  - PREFERRED_VIDEO_CODEC=vp9       # 偏好视频编码 (默认: vp9)
  - PREFERRED_VIDEO_EXT=mp4         # 偏好封装容器 (默认: mp4)
  - EMBED_SUBS=false                # 内封字幕 (默认: 关闭)
  - WRITE_SUBS=false                # 单独输出字幕文件 (默认：关闭)
  - ALLOW_AUTO_SUBS=false           # 自动输出字幕文件 (默认: 打开)
  - SUBTITLE_FORMAT=vtt             # 字幕文件格式 (默认: vtt)
  - SUBTITLE_LANGUAGES=en           # 字幕语言 (默认: 英语)
  - THREAD_COUNT=4                  # 下载线程数 (默认: 4线程)
```

## 界面图

### 手机界面图 (暗黑模式)

![Phone](tubetube/static/phone-screenshot.png)



### Desktop (暗黑模式)

![Screenshot](tubetube/static/screenshot.png)

 </picture>
</a>
