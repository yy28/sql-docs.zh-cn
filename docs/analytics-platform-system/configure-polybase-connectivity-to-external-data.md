---
title: 配置 PolyBase 连接到外部数据 (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f14ac21-a086-4c05-861f-0a12bf278259
caps.latest.revision: 43
ms.openlocfilehash: 42dc008855ea9de61c67365ac81927808491de13
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="configure-polybase-connectivity-to-external-data"></a>配置 PolyBase 连接到外部数据
说明如何在 SQL Server PDW 连接到外部 Hadoop 或 Microsoft Azure 存储 blob 数据源中配置 PolyBase。 使用 PolyBase 将运行集成来自多个源，包括 Hadoop、 Azure blob 存储和 SQL Server PDW 的数据的查询。  
  
### <a name="to-configure-connectivity"></a>若要配置的连接  
  
1.  打开一个查询工具，如 sqlcmd 或 SQL Server Data Tools (SSDT)，并运行 sp_configure，若要查看当前的 'hadoop connectivity' 设置。  
  
    ![hadoop 连接设置](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  决定哪些 Hadoop 连接设置以及是否需要更改的当前设置。 此选项适用于整个 SQL Server PDW 区域。 有关配置设置和版本的完整列表，请参阅[sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
3.  若要更改 'hadoop connectivity' 设置，请使用 RECONFIGURE 运行 sp_configure。 下面是一些示例。  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP), HDInsight on Analytics Platform System, or HDInsight’s Microsoft Azure blob storage  
    EXEC sp_configure 'hadoop connectivity', 4;   
    RECONFIGURE;  
  
    -- Enable connectivity to Hortonworks Data Platform (HDP)for Linux   
    EXEC sp_configure 'hadoop connectivity', 5;   
    RECONFIGURE;  
  
    -- Enable connectivity to Cloudera CDH for Linux   
    EXEC sp_configure 'hadoop connectivity', 3;   
    RECONFIGURE;  
  
    -- Disable the Hadoop connectivity option   
    EXEC sp_configure 'hadoop connectivity', 0;  
    RECONFIGURE;  
    ```  
  
    运行 sp_configure 以及重新配置设置的配置值。 需要重新启动区域设置的运行的值。 重新启动后需要，则下一步停止还，因为你不必执行在下一步，这会更改 core-site.xml 之前重新启动。  
  
4.  若要启用 Microsoft Azure blob 存储作为外部数据源，将一个或多个 Microsoft Azure 存储帐户访问密钥添加到 PDW core-site.xml 文件中。 若要添加的键：  
  
    1.  查找你的 Microsoft Azure 存储帐户名称。 若要查看你的存储帐户，登录到[Azure 门户](https://portal.azure.com)单击**存储帐户 （经典）**。  
  
        ![Windows Azure 存储帐户名称](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  查找你的 Azure 存储帐户访问密钥。 若要执行此操作，单击你的存储帐户名称，并在设置边栏选项卡上单击**密钥**。 这将显示你的帐户名称和存储密钥。  
  
        ![Windows Azure 存储帐户访问密钥](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  打开远程桌面连接到 PDW 控件节点。  
  
    4.  打开文件 C:\Program Files\Microsoft SQL Server 并行数据 Warehouse\100\Hadoop\conf\core-site.xml。  
  
    5.  将具有名称和值属性的以下属性添加到 core-site.xml 中。  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        此示例使用的帐户的名称和访问密钥，如前面所述。  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > 存储访问密钥存储在 core-site.xml 中之前采取安全预防措施。 任何具有 CONTROL SERVER 或 ALTER ANY EXTERNAL DATA SOURCE 权限用户都可以创建外部数据源可访问此帐户。 创建外部数据源后，使用 CREATE TABLE 权限的所有 SQL Server PDW 用户可以都创建外部表访问此存储帐户。 然后，用户可以访问帐户数据并使用该帐户中的资源。  
  
    6.  将所做的更改保存到 core-site.xml 中。  
  
5.  将 yarn.application.classpath 属性和值添加到 yarn-site.xml 文件中。  
  
    如果要连接到外部的 Hadoop 1.3，跳过此步骤。  
  
    从 Hadoop 2.0 开始，yarn-site.xml 文件包含用于 Hadoop YARN 框架的配置设置。 此文件位于管理节点下**C:\program files\Microsoft SQL Server 并行数据 Warehouse\100\Hadoop\conf\\**。  
  
    若要在 Windows 或 Linux 上，针对外部 Hadoop 2.0 群集运行 PolyBase 查询，你需要配置 yarn.application.classpath 属性和值以与你外部的 Hadoop 群集上的 yarn-site.xml 设置保持一致。 即使外部的 Hadoop 群集使用的默认设置，则需要此配置。  
  
    默认设置示例：  
  
    ```xml  
    <property>  
        <name>yarn.application.classpath</name>  
        <value>  
          %HADOOP_CONF_DIR%,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/*,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*  
         </value>  
      </property>  
    ```  
  
    一旦 yarn-site.xml 中定义的任何属性，则 PolyBase 针对 HDInsight 区域运行查询时将使用这些属性设置。 如果你打算对 HDInsight 区域和外部 Hadoop 2.0 群集在 Windows 上运行 PolyBase 查询，必须在所有 yarn-site.xml 文件之间的一致性，否则 PolyBase 查询将失败。  
  
    若要对 HDInsight 区域和外部 Hadoop 2.0 群集运行 PolyBase，请在外部的 Hadoop 群集上使用 yarn-site.xml 默认设置。  
  
6.  重新启动 PDW 区域。 若要执行此操作，请使用 Configuration Manager 工具。 请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
7.  验证 Hadoop 连接的安全设置。 如果**弱的身份验证**端通过使用 Hadoop 上的启用`dfs.permission = true`，必须创建 Hadoop 用户**pdw_user**和授予完全读取并写入到此用户的权限。 SQL Server PDW 和来自 SQL Server PDW 的相应调用始终作为发出**pdw_user**。  这是固定的用户名，无法在此版本的 Hadoop 连接和 SQL Server PDW 发布更改。 如果通过禁用在 Hadoop 上的安全性`dfs.permission = false`，则不需要进行任何进一步操作。  
  
8.  决定哪些用户可以创建到 Microsoft Azure blob 存储的外部数据源。 为每个这些用户提供的存储帐户名称以及**ALTER ANY EXTERNAL DATA SOURCE**或**CONTROL SERVER**权限。  
  
9. 对于 Hadoop 连接，决定哪些用户可以创建到 Hadoop 的外部数据源。 为每个这些用户提供的 IP 地址和端口号的每个 Hadoop 名称节点，并给予他们**ALTER ANY EXTERNAL DATA SOURCE**或者**CONTROL SERVER**权限。  
  
10. 连接到 WASB 还需要在设备上配置的 DNS 转发。 若要配置 DNS 转发，请参阅[使用 DNS 转发器来解决非设备 DNS 名称&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
外部数据源、 外部文件格式和外部表，现在可以创建授权的用户。 它们可以使用它们来将数据从多个源，包括 Hadoop、 集成 Microsoft Azure blob 存储和 SQL Server PDW。  

## <a name="kerberos-configuration"></a>Kerberos 配置  
请注意，当 PolyBase 向 Kerberos 安全群集身份验证，hadoop.rpc.protection 设置必须设置为身份验证。 这会使 Hadoop 节点间的数据通信保持非加密状态。 

 若要连接到 [使用 MIT KDC] 的 Kerberos 保护的 Hadoop 群集：
   
  
1.  在管理节点上的安装路径中查找 Hadoop 配置目录：  
  
    ```  
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```  
  
2.  查找表中列出的配置密钥 Hadoop 端配置值。 （对于 Hadoop 计算机，在 Hadoop 配置目录中查找文件。）  
  
3.  将配置值复制到的值属性中的控件节点上的相应文件。  
  
    |**#**|**配置文件**|**配置密钥**|**操作**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|指定 KDC 主机名。 例如：kerberos.your-realm.com。|  
    |2|core-site.xml|polybase.kerberos.realm|指定 Kerberos 领域。 例如：YOUR-REALM.COM|  
    |3|core-site.xml|hadoop.security.authentication|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：KERBEROS<br></br>**安全说明：** KERBEROS 必须采用大写形式。 如果采用小写，则可能不会打开。|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如： hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如： mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如：10.193.26.174:10020|  
    |7|yarn-site.xml yarn。|yarn.resourcemanager.principal|查找 Hadoop 端配置并复制到 SQL Server 计算机。 例如： yarn/_HOST@YOUR-REALM.COM|  
  
4. 创建数据库范围内的凭据对象，以指定每个 Hadoop 用户的身份验证信息。 请参阅 [PolyBase T-SQL 对象](../relational-databases/polybase/polybase-t-sql-objects.md)。  

5. 重新启动 PDW 区域。 若要执行此操作，请使用 Configuration Manager 工具。 请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。
 
## <a name="see-also"></a>另请参阅  
[设备配置&#40;分析平台系统&#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
