### Hugo 构建命令

```
hugo --cleanDestinationDir --forceSyncStatic --gc --ignoreCache --minify
```

- `--cleanDestinationDir` 构建前先清理目标文件夹，即 public  
- `--forceSyncStatic` 强制同步 static 文件夹  
- `--gc` 构建后执行一些清理任务（删除掉一些没用的缓存文件）  
- `--ignoreCache` 构建时忽略缓存  
- `--minify` 压缩网页代码  
- `hugo --help` 查看所有命令  