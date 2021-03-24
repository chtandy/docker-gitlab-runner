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
