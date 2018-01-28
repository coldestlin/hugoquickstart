
---
title: "Intro"
date: 2018-01-28T13:20:01+08:00
draft: true
---

# 简单运行


## 运行


### ENV
python3 ``latest python, latest airflow``


### 不依赖airflow运行一次性任务
    可以用于测试性目的，或者想快速运行的一次性任务。
- 在tasks中配置部署workflow json格式需要的一些sql
- 在executor.standard或executor.fast的main语句中引用，实例化process，process.flow()
- python -m executor.standard/fast 直接运行。


### 依赖airflow运行任务
    可以运行一次性任务，也可以自动识别cron任务，自动判断分隔区和合适的start date



- 在tasks中配置部署workflow json格式需要的一些sql
- 使用cli工具把json配置传递到数据库中【目前还比较简略】
- 等待airflow识别自动运行


#### airflow的配置
- 安装最新版的apache-airflow
- 启动之前环境变量中设置airflow home的位置为blu文件夹的airflow-home即可


#### airflow的注意点
-   自动识别周期日期运行间隔的功能实现上，airflow的start date + period 为运行的真正时间区间。
    比如weekly的execution date为2017-11-12（周日），那么实际运行区间为[2017-11-12 TO 2017-11-19）


#### 任务更新注意点
- 任务以dag id识别，如果修改了cron，建议修改dag id。
- 如果任务是@once一次性类型，若要再次运行要么在airflow上手动点击运行，要么修改dag id。
- 如果任务以前执行过在airflow中留下记录，修改了不少东西想要重新运行，最好修改dag id。
- 一句话，不懂的时候记得修改dag id。


## real 运行

gunicorn -w 8 -b 0.0.0.0:9527 -k gevent -t 900 manage:app


