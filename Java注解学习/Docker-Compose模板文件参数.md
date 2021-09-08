## ulimits

指定容器的 ulimits 限制值。
例如，指定最大进程数为 65535，指定文件句柄数为 20000（软限制，应用可以随时修改，不能超过硬限制） 和 40000（系统硬限制，只能 root 用户提高）。

```dockerfile
  ulimits:
    nproc: 65535
    nofile:
      soft: 20000
      hard: 40000
```

