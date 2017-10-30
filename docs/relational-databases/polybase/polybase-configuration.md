---
title: "PolyBase 配置 | Microsoft Docs"
ms.custom: 
ms.date: 09/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: 17
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: 95a149c4a59de88373206f1b90419c0b7359bb90
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="polybase-configuration"></a>PolyBase 配置
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  使用以下过程配置 PolyBase。  
  
## <a name="external-data-source-configuration"></a>外部数据源配置  
 必须确保从 SQL Server 到外部数据源的连接。 连接类型会显著影响查询性能。 例如，10Gbit 以太网链接将使 PolyBase 查询的查询响应时间比 1Gbit 以太网链接更快。  
  
 必须使用 **sp_configure**配置 SQL Server，以连接到你的 Hadoop 版本或 Azure Blob 存储。 PolyBase 支持两种 Hadoop 分发：Hortonworks 数据平台 (HDP) 和 Cloudera 分布式 Hadoop (CDH)。  有关受支持的外部数据源的完整列表的详细信息，请参阅 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
1 请注意：PolyBase 不支持 Cloudera 加密的区域。 
  
### <a name="run-spconfigure"></a>运行 sp_configure  
  
1.  运行 sp_configure ‘hadoop connectivity’ 并设置适当的值。  若要查找值，请参阅 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
  
    ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  必须使用 **services.msc**重启 SQL Server。 重启 SQL Server 会重启这些服务：  
  
    -   SQL Server PolyBase 数据移动服务  
  
    -   SQL Server PolyBase 引擎  
  
## <a name="pushdown-configuration"></a>下推配置  
 若要提高查询性能，请启用到 Hadoop 群集的下推计算。需要向 SQL Server 提供一些特定于 Hadoop 环境的配置参数：  
  
1.  在 SQL Server 的安装路径中查找文件 **yarn-site.xml** 。 通常情况下，该路径为：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  对于 Hadoop 计算机，在 Hadoop 配置目录中查找类似文件。 在文件中，查找并复制配置密钥 yarn.application.classpath 的值。  
  
3.  对于 SQL Server 计算机，在 **yarn.site.xml 文件中，** 查找 **yarn.application.classpath** 属性。 将 Hadoop 计算机的值粘贴到值元素中。  

4. 对于所有 CDH 5.X 版本，你都需要将 **mapreduce.application.classpath** 配置参数添加到 **yarn.site.xml 文件**的末尾或添加到 **mapred-site.xml 文件**中。 HortonWorks 在 **yarn.application.classpath** 配置中包括了这些配置。

## <a name="connecting-to-hadoop-cluster-with-hadooprpcprotection-setting"></a>使用 Hadoop.RPC.Protection 设置连接到 Hadoop 群集
在 Hadoop 群集中保护通信的常用方法是将 hadoop.rpc.protection 配置更改为“隐私”或“完整性”。 默认情况下，PolyBase 假定配置设置为“身份验证”。 要替代此默认设置，需要将以下属性添加到 core-site.xml 文件。 通过更改此配置，可实现 hadoop 节点之间以及 SSL 到 SQL Server 的连接之间安全的数据传输。

```
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
  <property>
    <name>hadoop.rpc.protection</name>
    <value></value>
  </property> 
```




## <a name="example-yarn-sitexml-and-mapred-sitexml-files-for-cdh-5x-cluster"></a>CDH 5.X 群集的示例 yarn-site.xml 和 mapred-site.xml 文件。



包含 yarn.application.classpath 和 mapreduce.application.classpath 配置的 Yarn-site.xml。
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>

```
如果你选择将两个配置设置拆分为 mapred-site.xml 和 yarn-site.xml，则这两个文件将如下所示：

**yarn-site.xml**
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>
```

**mapred-site.xml**

注意，我们添加了属性 mapreduce.application.classpath。 在 CDH 5.x 中，你会发现遵守 Ambari 中的相同命名约定的配置值。

```
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
  <property>
    <name>mapred.min.split.size</name>
      <value>1073741824</value>
  </property>
  <property>
    <name>mapreduce.app-submission.cross-platform</name>
    <value>true</value>
  </property>
<property>
    <name>mapreduce.application.classpath</name>
    <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
  </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
    <name>mapreduce.jobhistory.principal</name>
    <value></value>
  </property>
  <property>
    <name>mapreduce.jobhistory.address</name>
    <value></value>
  </property>
-->
</configuration>
  
```
  
## <a name="kerberos-configuration"></a>Kerberos 配置  
请注意，当 PolyBase 向 Kerberos 保护的群集证明身份时，我们要求将 hadoop.rpc.protection 设置设为身份验证。 这会使 Hadoop 节点间的数据通信保持非加密状态。 

 连接到 Kerberos 保护的 Hadoop 群集 [使用 MIT KDC]：
   
  
1.  在 SQL Server 的安装路径中查找 Hadoop 配置目录。 通常情况下，该路径为：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  查找表中列出的配置密钥 Hadoop 端配置值。 （对于 Hadoop 计算机，在 Hadoop 配置目录中查找文件。）  
  
3.  将配置值复制到 SQL Server 计算机上对应文件的值属性中。  
  
    |**#**|**配置文件**|**配置密钥**|**操作**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|指定 KDC 主机名。 例如：kerberos.your-realm.com。|  
    |2|core-site.xml|polybase.kerberos.realm|指定 Kerberos 领域。 例如：YOUR-REALM.COM|  
    |3|core-site.xml|hadoop.security.authentication|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：KERBEROS<br></br>**安全说明：** KERBEROS 必须采用大写形式。 如果采用小写，则可能不会打开。|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如： hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如： mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：10.193.26.174:10020|  
    |7|yarn-site.xml yarn。|yarn.resourcemanager.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如： yarn/_HOST@YOUR-REALM.COM|  
  
4.  创建数据库范围内的凭据对象，以指定每个 Hadoop 用户的身份验证信息。 请参阅 [PolyBase T-SQL 对象](../../relational-databases/polybase/polybase-t-sql-objects.md)。  
  
## <a name="next-steps"></a>后续步骤  
 [PolyBase T-SQL 对象](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
  
  

