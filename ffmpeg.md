<h3 align='center'> ffmpeg 常用 </h3>

### 图片

- 图片缩放

  - 等比

    ```shell
    ffmpeg -i INPUT -vf "scale=1920:-1" OUTPUT
    ```

    等比并适应到一定的长宽

    ```shell
    ffmpeg \
      -i INPUT \
      -vf "scale=1920:1080:force_original_aspect_ratio=increase,crop=1920:1080" \
      -y OUTPUT

    ```

  - 非等比

    ```shell
    ffmpeg -i INPUT -vf "scale="iw*2:ih*3" OUTPUT
    ```

- 图片淡入淡出

  ```shell
  ffmpeg \
    -loop 1 -i IN1
    -loop 1 -i IN2
    -filter_complex "[1:v][0:v]blend=all_expr='A*(if(gte(T,3),1,T/3))+B*(1-(if(gte(T,3),1,T/3)))'" \
    -t 3 frames_%04d.png
  ```

### 音频

- flac -> alac

  ```shell
  ffmpeg \
    -i INPUT \
    -acodec alac \
    -vcodec copy \
    OUTPUT
  ```

- metadata
  ```shell
  ffmpeg \
    -i "file:{sound}" \
    -i "file:{img}" \
    -map 0:0 -map 1:0 \
    -id3v2_version 3 \
    -metadata:s:v title="Album cover" \
    -metadata:s:v comment="Cover (font)" \
    -metadata key1="value1" \
    -metadata key2="value2" \
    -codec copy \
    "file:{output}"
  ```

### 视频

- video -> image

  ```shell
  ffmpeg \
    -i INPUT \
    -vf fps=1/60,select='between(t,x,y)+between(t,x2,y2)' \
    out%04d.png
  ```

- cut

  ```shell
  ffmpeg
    -i INPUT \
    -ss hh:mm:ss \
    -to hh:mm:ss \
    OUTPUT
  ```
