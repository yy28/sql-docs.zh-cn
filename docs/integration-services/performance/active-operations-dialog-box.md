---
title: "“活动操作”对话框 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.isoperations.executions.f1"
  - "sql13.ssis.ssms.isoperations.general.f1"
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# “活动操作”对话框
  使用 **“活动操作”** 对话框可以查看 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上当前运行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作的状态，例如部署、验证和包执行。 此数据存储在 SSISDB 目录中。  
  
 有关相关 [!INCLUDE[tsql](../../includes/tsql-md.md)] 视图的详细信息，请参阅 [catalog.operations（SSISDB 数据库）](../../integration-services/system-views/catalog-operations-ssisdb-database.md)、[catalog.validations（SSISDB 数据库）](../../integration-services/system-views/catalog-validations-ssisdb-database.md)和 [catalog.executions（SSISDB 数据库）](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
 **您希望做什么？**  
  
-   [打开“活动操作”对话框](../../integration-services/performance/active-operations-dialog-box.md#open_dialog)  
  
-   [选项](#options)  
  
##  <a name="open_dialog"></a> 打开“活动操作”对话框  
  
1.  打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
2.  连接 Microsoft SQL Server 数据库引擎  
  
3.  在对象资源管理器中，展开“Integration Services”节点，右键单击“SSISDB”，然后单击“活动操作”。  
  
## 配置选项  
  
###  <a name="options"></a> 选项  
 **类型**  
 指定操作的类型。 下面是“类型”字段的可能值以及 Transact-SQL **catalog.operations** 视图的 operations_type 列中的相应值。  
  
|||  
|-|-|  
|Integration Services 初始化|1|  
|操作清除（SQL 代理作业）|2|  
|项目版本清除（SQL 代理作业）|3|  
|部署项目|101|  
|还原项目|106|  
|创建和启动包执行|200|  
|停止操作（停止验证或执行）|202|  
|验证项目|300|  
|验证包|301|  
|配置目录|1000|  
  
 **停止**  
 单击以停止当前正在运行的操作。  
  
  