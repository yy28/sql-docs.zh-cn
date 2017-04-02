---
title: "PolyBase 配置 | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: 17
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 12
---
# PolyBase 配置
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  使用以下过程配置 PolyBase。  
  
## <a name="external-data-source-configuration"></a>外部数据源配置  
 必须确保从 SQL Server 到外部数据源的连接。 连接类型会显著影响预期的查询性能。 例如，10Gbit 以太网链接将使 PolyBase 查询的查询响应时间比 1Gbit 以太网链接更快。  
  
 必须使用 **sp_configure** 配置 SQL Server，以连接到你的 Hadoop 版本或 Azure Blob 存储。 PolyBase 支持两种 Hadoop 分发：Hortonworks 数据平台 (HDP) 和 Cloudera 分布式 Hadoop (CDH)。  有关受支持的外部数据源的完整列表的详细信息，请参阅 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
  
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
 若要提高查询性能，请对 Hadoop 群集启用下推计算：  
  
1.  在 SQL Server 的安装路径中查找文件 **yarn-site.xml**。 通常情况下，该路径为：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  对于 Hadoop 计算机，在 Hadoop 配置目录中查找类似文件。 在文件中，查找并复制配置密钥 yarn.application.classpath 的值。  
  
3.  对于 SQL Server 计算机，在 **yarn.site.xml 文件中，** 查找 **yarn.application.classpath** 属性。 将 Hadoop 计算机的值粘贴到值元素中。  
  
## <a name="kerberos-configuration"></a>Kerberos 配置  
 连接到 Kerberos 保护的 Hadoop 群集 [使用 MIT KDC]：  
  
1.  在 SQL Server 的安装路径中查找 Hadoop 配置目录。 通常情况下，该路径为：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  查找表中列出的配置密钥 Hadoop 端配置值。 （对于 Hadoop 计算机，在 Hadoop 配置目录中查找文件。）  
  
3.  将配置值复制到 SQL Server 计算机上对应文件的值属性中。  
  
    |**#**|**配置文件**|**配置密钥**|**操作**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|指定 Kerberos 领域。 例如：YOUR-REALM.COM|  
    |2|core-site.xml|polybase.kerberos.realm|指定 KDC 主机名。 例如：kerberos.your-realm.com。|  
    |3|core-site.xml|hadoop.security.authentication|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：KERBEROS<br></br>**安全说明：**KERBEROS 必须采用大写形式。 如果采用小写，则可能不会打开。|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.address|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：10.193.26.174:10020|  
    |7|yarn-site.xml yarn。|yarn.resourcemanager.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：yarn/_HOST@YOUR-REALM.COM|  
  
4.  创建数据库范围内的凭据对象，以指定每个 Hadoop 用户的身份验证信息。 请参阅 [PolyBase T-SQL 对象](../../relational-databases/polybase/polybase-t-sql-objects.md)。  
  
## <a name="next-steps"></a>后续步骤  
 [PolyBase T-SQL 对象](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
  
  