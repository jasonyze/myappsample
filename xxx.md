# dble-maxConnections  

## ISSUE

- [Err] 3009 - java.io.IOException: the max activeConnnections size can not be max than maxconnections. 

## Resolution

1. 检查是否使用了过多的短链，导致频繁建立连接，链接池不够用 
>**注意**：不要过多的使用短链，容易消耗dble资源  
2.  maxCon配置过小，调大maxCon 

| 配置名称 | 配置内容 | 默认值/单位 | 作用原理或应用 |
| ---- | ---- | ---- | ----|
| maxCon | 控制最大连接数 | 默认1024 | 大于此连接数之后,建立连接会失败.注意当各个用户的maxcon总和值大于此值时，以当前值为准 全局maxCon不作用于manager用户 |
