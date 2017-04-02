---
title: "执行 T-SQL 语句任务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executetsqlstatementtask.f1"
helpviewer_keywords: 
  - "Transact-SQL 语句, SSIS"
  - "语句 [Integration Services]"
  - "执行 T-SQL 语句任务 [Integration Services]"
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# 执行 T-SQL 语句任务
  执行 T-SQL 语句任务运行 Transact-SQL 语句。 有关详细信息，请参阅 [Transact-SQL 引用（数据库引擎）](../../t-sql/transact-sql-reference-database-engine.md)和 [Integration Services (SSIS) 查询](../../integration-services/integration-services-ssis-queries.md)。  
  
 此任务类似于执行 SQL 任务。 但是，执行 T-SQL 语句任务只支持 SQL 语言的 Transact-SQL 版本，在使用 SQL 语言的其他方言的服务器上无法使用此任务来运行语句。 如果需要运行参数化查询，将查询结果保存到变量，或使用属性表达式，那么您应当使用执行 SQL 任务而不是执行 T-SQL 语句任务。 有关详细信息，请参阅 [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md)。  
  
## 执行 T-SQL 任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“执行 T-SQL 语句”任务（维护计划）](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## 另请参阅  
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)   
 [在 Integration Services 包中执行 MERGE](../../integration-services/control-flow/merge-in-integration-services-packages.md)  
  
  