### 本地调试（~~Web Server~~）

```
hugo server -w -D -p 8080 -t hello-friend
```
- `hugo server` 把 Hugo 当作 Web 服务器，而非构建静态网页  
- `-w` 有文件变化立即刷新（默认开启）  
- `-D` 构建草稿，撰写新文章时很有用  
- `-p 8080` 端口+端口号（默认 1313）  
- `-t hello-friend` 使用 hello-friend 主题    
- `hugo --help` 查看所有命令  