---
keyword: [Fair Scheduler, Fair]
---

# Fair Scheduler使用说明

Fair Scheduler称为公平调度器，是Apache YARN内置的调度器。公平调度器主要目标是实现YARN上运行的应用能公平的分配到资源，其中各个队列使用的资源根据设置的权重（weight）来实现资源的公平分配。

## 开启Fair Scheduler

**说明：** 开启集群资源队列后，YARN组件**配置**中的**fair-scheduler**配置区域将处于冻结状态，相关已有配置将会同步到**集群资源管理**页面中。如果需要继续在YARN服务的**配置**页面通过XML的方式设置集群资源，则需先在**集群资源管理**中关闭YARN资源队列。

1.  登录[阿里云E-MapReduce控制台](https://emr.console.aliyun.com/)。

2.  在顶部菜单栏处，根据实际情况选择地域（Region）和资源组。

3.  单击上方的**集群管理**页签。

4.  在**集群管理**页面，单击相应集群所在行的**详情**。

5.  在左侧导航栏中，单击**集群资源管理**。

6.  在**集群资源管理**页面，单击**开启YARN资源队列**。

7.  单击**Fair Scheduler**。

8.  单击**保存**。


## 配置Fair Scheduler

开启YARN资源队列后，可以执行以下步骤配置Fair Scheduler。

1.  在**集群资源管理**页面，单击上方的**资源队列配置**。

2.  在**队列配置**区域，配置队列信息。

    **root**为一级队列，是所有队列的父队列，管理YARN的所有资源，默认root下只有default队列。

    **说明：**

    -   同一个父队列下的同一级别的子队列Capacity之和必须为100。例如，root下有两个子队列default和department，两个子队列的Capacity求和必须为100，department下又设置了market和dev，这里department下两个子队列之和必须也是100。
    -   在程序运行时，如果不指定提交队列，默认会提交到default队列。
    -   新建root下一级队列无需重启ResourceManager，直接单击**部署生效**即可。
    -   新建和设置root下的二级队列需要重启ResourceManager。
    -   修改队列名称需要重启ResourceManager。
    **说明：** 由于队列配置是嵌套的，所以父队列的参数优先级会高于子队列。当子队列设置的资源用量大于父队列时，在调度器分配资源时，会以父队列的参数设置为限制。

    -   设置新队列名称，**资源队列名称**是必填项，队列名称中不能包含英文句号（.）。
    -   设置调度器权重，**权重**是必填项。调度器给队列分配资源时，达到设置的权重时，会认为达到公平状态。该权重同时在各个二级、三级以及更深级别的队列生效，如在同一父队列下面的两个子队列权重分别为2和1，则在2个子队列中都有任务运行时，达到2:1的资源分配比例，会认为达到了公平状态。
    -   **最大资源量**表示该队列能被分配到的最大资源量，应该大于**最小资源量**，小于集群YARN所能控制的资源规模。如果设置的大于集群资源规模，生效值是YARN所能控制的资源规模。例如，YARN管理的VCore为16个，但最大资源量设置为20，实际生效为16。
    -   在程序运行时，如果不指定提交队列，默认会提交到default队列。
    -   修改子队列名称，如果修改子节点队列名称后，没有重启ResourceManager，任务仍然能提交到原队列名称，但EMR控制台队列配置不会再显示。重启ResourceManager后，原队列将不再存在。
    -   删除队列时，如果删除的不是root的子队列（即非二级队列），删除后单击**部署生效**即可；如果删除的是root的子队列，需要单击**操作** \> **重启ResourceManager**，修改才能生效。

## 切换调度器类型

开启YARN资源队列后，可以执行以下步骤切换调度器类型。

1.  在**集群资源管理**页面，单击上方的**切换调度器**。

2.  单击需要切换的资源队列类型。

3.  单击**保存**。

4.  单击**操作** \> **重启ResourceManager**。

5.  在**执行集群操作**对话框中，设置相关参数，单击**确定**。

6.  在**确认**对话框中，单击**确定**。

    待提示操作成功时，表示切换调度器类型成功。


## 提交作业

提交到指定队列时需通过**mapreduce.job.queuename**来指定队列，示例如下。

```
`hadoop jar /usr/lib/hadoop-current/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.8.5.jar pi -Dmapreduce.job.queuename=test  2 2`
```

