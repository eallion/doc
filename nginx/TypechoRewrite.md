### Typecho Nginx Rewrite

- 方案一
```
if (!-e $request_filename) {
    rewrite ^(.*)$ /index.php$1 last;
}
```

- 方案二
```
if (!-e $request_filename) {
    rewrite ^(.*)$ /index.php$1 last;
}
```