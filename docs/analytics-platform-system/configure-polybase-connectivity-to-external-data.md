---
title: "配置 PolyBase 连接到外部数据 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f14ac21-a086-4c05-861f-0a12bf278259
caps.latest.revision: "43"
ms.openlocfilehash: 7d486992f688b5bc914508ef000f23209b4bde89
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
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
  
    运行 sp_configure 以及重新配置设置的配置值。 需要重新启动区域设置的运行的值。 重新启动后需要，则下一步停止还，因为你不必执行之前在下一步的步骤，这会更改 core-site.xml 完成之后重新启动。  
  
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
        > 存储访问密钥存储在 core-site.xml 中之前采取安全预防措施。 任何具有 CONTROL SERVER 或 ALTER ANY EXTERNAL DATA SOURCE 权限用户都可以创建外部数据源可访问此帐户。 创建外部数据源后，所有 SQL Server PDW 用户有权都创建表可以都创建外部表访问此存储帐户。 然后，用户将能够访问帐户数据和使用的帐户中的资源。  
  
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
  
6.  重新启动 PDW 区域。 若要执行此操作，请使用 Configuration Manager 工具。 请参阅[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md).  
  
7.  验证 Hadoop 连接的安全设置。 如果**弱的身份验证**端通过使用 Hadoop 上的启用`dfs.permission = true`，必须创建 Hadoop 用户**pdw_user**和授予完全读取并写入到此用户的权限。 SQL Server PDW 和来自 SQL Server PDW 的相应调用始终作为发出**pdw_user**其是固定的用户名且不能在此版本的 Hadoop 连接和 SQL Server PDW 发布更改。 如果通过禁用在 Hadoop 上的安全性`dfs.permission = false`，则不需要进行任何进一步操作。  
  
8.  决定哪些用户可以创建到 Microsoft Azure blob 存储的外部数据源。 为每个这些用户提供的存储帐户名称以及**ALTER ANY EXTERNAL DATA SOURCE**或**CONTROL SERVER**权限。  
  
9. 对于 Hadoop 连接，决定哪些用户可以创建到 Hadoop 的外部数据源。 为每个这些用户提供的 IP 地址和端口号的每个 Hadoop 名称节点，并给予他们**ALTER ANY EXTERNAL DATA SOURCE**或者**CONTROL SERVER**权限。  
  
10. 连接到 WASB 还需要在设备上配置的 DNS 转发。 若要配置 DNS 转发，请参阅[使用 DNS 转发器来解决非设备 DNS 名称 &#40;分析平台系统 &#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
外部数据源、 外部文件格式和外部表，现在可以创建授权的用户。 它们可以使用它们来将数据从多个源，包括 Hadoop、 集成 Microsoft Azure blob 存储和 SQL Server PDW。  
  
## <a name="see-also"></a>另请参阅  
[设备配置 &#40;分析平台系统 &#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
