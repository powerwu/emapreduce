# Hive统一元数据

EMR-2.4.0之前版本，所有集群采用的是集群本地的Mysql数据库作为Hive元数据库；EMR-2.4.0及后续版本，E-MapReduce（简称EMR）支持统一的高可靠的Hive元数据库。

创建集群时，元数据选择**统一meta数据库**，详情请参见[创建集群](/cn.zh-CN/集群管理/集群配置/创建集群.md)。

因为元数据库需要使用公网IP来连接，所以集群必须要有公网IP，同时请不要随意的切换公网IP地址，防止对应的数据库白名单失效。

如果是本地的元数据库，您可以使用集群上的Hue工具来管理。

E-MapReduce后台RDS统一管理元数据的方式，仅限小容量的用户使用。对于大容量场景，建议您自建RDS作为统一元数据。默认限制为：

-   总容量：200MiB。
-   小时query数量限制：720000/h。
-   小时update数量限制：144000/h。

## 介绍

![hive元数据库](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9311549951/p11067.png)

统一的元数据管理，可以实现：

-   持久化的元数据存储。

    支持统一元数据之前，元数据都是在集群内部的Mysql数据库，元数据会随着集群的释放而丢失，特别是EMR提供了灵活按量模式，集群可以按需创建用完就释放。如果您需要保留现有的元数据信息，必须登录集群手动将元数据信息导出。

    支持统一元数据之后，释放集群不会清理元数据信息。所以，在任何时候删除OSS上或者集群HDFS上数据（包括释放集群操作）的时候，需要先确认该数据对应的元数据已经删除（即要删掉数据对应的表和数据库），否则元数据库中可能出现一些脏数据。

-   计算存储分离。

    EMR上可以支持将数据存放在阿里云OSS中，在大数据量的情况下将数据存储在OSS上会大大降低使用的成本，EMR集群主要用来作为计算资源，在计算完成之后可以随时释放，数据在OSS上，同时也不用再考虑元数据迁移的问题。

-   数据共享。

    使用统一的元数据库，如果您的所有数据都存放在OSS之上，则不需要做任何元数据的迁移和重建，所有集群都是可以直接访问数据，这样每个EMR集群可以做不同的业务，但是可以很方便地实现数据的共享。


## 创建使用统一元数据的集群

支持以下两种方式创建统一元数据的集群：

-   页面方式。

    [创建集群](/cn.zh-CN/集群管理/集群配置/创建集群.md)时，在**基础配置**页面，选中**统一meta数据库**。

-   API方式。

    使用CreateClusterV2创建集群，详情请参见[CreateClusterV2](/cn.zh-CN/API参考/集群/CreateClusterV2.md)。

    **说明：** 需指定参数：useLocalMetaDb=false。


## 表管理

详细请参见[Hive元数据基本操作](/cn.zh-CN/元数据管理/Hive元数据管理/Hive元数据基本操作.md)。

## 查看元数据库信息

1.  登录[阿里云E-MapReduce控制台](https://emr.console.aliyun.com/)。

2.  在顶部菜单栏处，根据实际情况选择地域（Region）和资源组。

3.  单击上方的**元数据管理**页签。

4.  在左侧导航栏，单击**元数据库信息**。

    您可以查看当前RDS的用量和使用限制，如果需要修改，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex?spm=5176.2020520129.103.2.9Z8xg7)。

    ![元数据信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9311549951/p96744.png)


