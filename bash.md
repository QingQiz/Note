<h3 align='center'> Bash / Zsh 的奇技淫巧 </h3>

#### 历史记录

- `!-n:a-b`

    上 **n** 条命令的第 **a** 个到第 **b** 个参数
    
    - 省略 `-n` 表示上一条命令
    - `-n` 为 **#** 表示当前命令
    - `a` 或 `b` 为 **$** 表示最后一个参数
    - `-b` 可以省略

- `!xxxx:y`

    - 其中 `!xxxx` 是取出来的历史参数 

    - `y` 为 **h** 表示将文件排除，取前缀目录
        > /etc/xxx.yyy -> /etc

    - `y` 为 **gs/a/b** 表示正则替换，将 **a** 替换为 **b**

