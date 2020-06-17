# 服务器

## [命令与Shell](/server/shell)

## [Linux](/server/linux)

## 常用生产工具

### 团队开发必备

**gitea**

**gitlab**

### 监控统计相关

**InfluxDB**
>时序数据库，常用于监控数据统计、埋点数据统计

常用InfluxQL

```
-- 查看所有的数据库
show databases;
-- 使用特定的数据库
use database_name;
-- 查看所有的measurement
show measurements;
-- 查询10条数据
select * from measurement_name limit 10;
-- 数据中的时间字段默认显示的是一个纳秒时间戳，改成可读格式
precision rfc3339; -- 之后再查询，时间就是rfc3339标准格式
-- 或可以在连接数据库的时候，直接带该参数
influx -precision rfc3339
-- 查看一个measurement中所有的tag key
show tag keys
-- 查看一个measurement中所有的field key
show field keys
-- 查看一个measurement中所有的保存策略(可以有多个，一个标识为default)
show retention policies;
```

**Zabbix**
>监控与报警系统

**Prometheus**
>监控与报警系统，自带时序数据库

**Grafana**
>监控与度量数据分析与可视化工具，官方支持以下数据源:Graphite，Elasticsearch，InfluxDB，Prometheus，Cloudwatch，MySQL和OpenTSDB等
