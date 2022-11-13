# CasaOS 一键安装 json 文件

### 配置文件规范

1. 容器名、大小写遵从镜像官方 Docker CLI 命名。
2. 程序配置存放在 `/DATA/AppData/APPNAME` 目录。
3. 重启策略一般为 `unless-stopped` ，按需启用。
4. 尽可能匹配图标，原则：png透明底、200px以上
5. 如有 WebUI 的，配置端口号。
6. json内容格式化，增强可读性。