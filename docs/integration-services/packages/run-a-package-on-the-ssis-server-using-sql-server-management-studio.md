---
title: "使用 SQL Server Management Studio 在 SSIS 服务器上运行包 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# 使用 SQL Server Management Studio 在 SSIS 服务器上运行包
  在将您的项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器中之后，可以在该服务器上运行此包。  
  
 您可以使用操作报告查看有关服务器上已运行或当前正在运行的包的信息。 有关详细信息，请参阅 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)。  
  
### 使用 SQL Server Management Studio 在服务器上运行包  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并连接到包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 实例。  
  
2.  在对象资源管理器中，展开 **“Integration Services 目录”** 节点，再展开 **“SSISDB”** 节点，然后导航到包含在您部署的项目中的包。  
  
3.  右键单击包名称，然后选择“执行”。  
  
4.  使用 **“执行包”**对话框中的 **“参数”**、 **“连接管理器”** 和 **“高级”** 选项卡上的设置来配置包执行。  
  
5.  单击 **“确定”** 运行包。  
  
     - 或 -  
  
     使用存储过程来运行包。 单击“脚本”生成创建执行实例并启动执行实例的 Transact-SQL 语句。 该语句包含对 catalog.create_execution、catalog.set_execution_parameter_value 和 catalog.start_execution 存储过程的调用。 有关这些存储过程的详细信息，请参阅 [catalog.create_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)、[catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)和 [catalog.start_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。  
  
  