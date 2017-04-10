---
title: "创建 SSIS 目录 | Microsoft Docs"
ms.custom: 
  - "ssisdev020617"
ms.date: "11/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# 创建 SSIS 目录
  当您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中设计和测试包后，可将包含包的项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。 在可以将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器之前，该服务器必须包含 **SSISDB** 目录。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的安装程序并不会自动创建目录；您需要使用以下说明手动创建目录。  
  
 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中创建 SSISDB 目录。 还可以使用 Windows PowerShell 以编程方式创建目录。  
  
### 在 SQL Server Management Studio 中创建 SSISDB  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎。  
  
3.  在“对象资源管理器”中，展开服务器节点，右键单击“Integration Services 目录”节点，然后单击“创建目录”。  
  
4.  单击 **“启用 CLR 集成”**。  
  
     该目录使用 CLR 存储过程。  
  
5.  单击“在 SQL Server 启动时启用自动执行 Integration Services 存储过程”，使 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md) 存储过程在每次重启 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务器后运行。  
  
     该存储过程对 SSISDB 目录的操作状态进行维护。 它可以纠正当 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 服务器实例出现故障时正在运行的任何包的状态。  
  
6.  输入密码，然后单击 **“确定”**。  
  
     该密码保护用于对目录数据进行加密的数据库主密钥。 将该密码保存在安全的位置。 同时建议您也备份数据库主密钥。 有关详细信息，请参阅 [Back Up a Database Master Key](../../relational-databases/security/encryption/back-up-a-database-master-key.md)。  
  
### 以编程方式创建 SSISDB 目录  
  
1.  执行以下 PowerShell 脚本：  
  
    ```  
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()  
  
    ```  
  
     有关更多如何使用 Windows PowerShell 和 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间的示例，请参阅 blogs.msdn.com 上的博客文章 [SQL Server 2012 中的 SSIS 和 PowerShell](http://go.microsoft.com/fwlink/?LinkId=242539)。 有关命名空间和代码示例的概述，请参阅 blogs.msdn.com 上的博客文章 [SSIS 目录托管对象模型一瞥](http://go.microsoft.com/fwlink/?LinkId=254267)。  
  
## 另请参阅  
 [SSIS 目录](../../integration-services/service/ssis-catalog.md)   
 [备份、还原和移动 SSIS 目录](../../integration-services/service/backup-restore-and-move-the-ssis-catalog.md)  
  
  