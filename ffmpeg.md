<h3 align='center'> ffmpeg 常用 </h3>

### 图片

- 图片缩放
  - 等比

    ```shell
    ffmpeg -i INPUT -vf "scale=1920:-1" OUTPUT
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

### 视频

### 音频
