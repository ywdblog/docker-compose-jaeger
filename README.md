### 服务信息
 
1：jaeger 全家桶，hotrod微服务，使用的es和promethous不在本docker-compose上
 
### 安装说明

```
docker-compose build
docker-compose up
docker-compose down
```

UI配置：

```
service {
    server_name  jaeger.ui.net;
    location / {
        proxy_pass http://ip:16686;
    }
}
```

hotrod配置：

```
service {
    server_name  hotrod.net;
    location / {
        proxy_pass http://ip:9191;
    }
}
```

定时删除老的es索引：

```
/usr/bin/docker run -it --rm --net=host -e ROLLOVER=true jaegertracing/jaeger-es-index-cleaner:latest 1 http://ip:9200
```

### 参考
 
- [hotrod安装说明](https://github.com/jaegertracing/jaeger/tree/main/examples/hotrod)
- [jaegertracing 官方](https://www.jaegertracing.io/docs/1.29/getting-started/)
- [jaegertracing 官方deployment说明](https://www.jaegertracing.io/docs/1.29/deployment/)
- [uber官方对于jaegertracing的设计说明](https://eng.uber.com/distributed-tracing/)
- [通过一个微服务例子演示jaegertracing](https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941)
- [jaegertracing在promethouse上的dashboard](https://grafana.com/grafana/dashboards/12535)
- [jaegertracing监控](https://github.com/jaegertracing/jaeger/tree/main/docker-compose/monitor)
- [hub.docker上的jaeger](https://hub.docker.com/r/jaegertracing/jaeger-es-index-cleaner)