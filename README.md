### 初始化流程
- 第一次先執行以下，初始化runner config
```
docker-compose -f init-docker-compose.yml up -d
```
- 接著執行，會移除上一個init container
```
docker-compose up -d --remove-orphans
```


### 已初始化
- 日後啟動只需執行
```
docker-compose up -d
```
### runner 要能支援docker
- config.toml 內含
```
    volumes = ["/cache", "/var/run/docker.sock:/run/docker.sock"]
    network_mode = "host"
    privileged = true
```
- 完整 config.toml
```
concurrent = 1
check_interval = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "docker-runner"
  url = "https://gitlab.com/"
  token = "2Fu1Kq5a9Djcu35YBaz_"
  executor = "docker"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
    [runners.cache.azure]
  [runners.docker]
    tls_verify = false
    image = "alpine:latest"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache", "/var/run/docker.sock:/run/docker.sock"]
    network_mode = "host"
    shm_size = 0
```

### 可能的問題
- dind 原來的參數可能有問題
- 解決方式
```
privileged = true
```
