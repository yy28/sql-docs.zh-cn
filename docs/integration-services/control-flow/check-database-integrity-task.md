---
title: "“检查数据库完整性”任务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.checkdatabaseintegritytask.f1"
helpviewer_keywords: 
  - "数据完整性 [Integration Services]"
  - "“检查数据库完整性”任务 [Integration Services]"
  - "检查数据库一致性"
  - "数据库一致性检查 [Integration Services]"
  - "验证数据库一致性"
  - "完整性检查 [Integration Services]"
ms.assetid: 5a82fe99-4503-429f-9337-e6bac7649fe4
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# “检查数据库完整性”任务
  “检查数据库完整性”任务检查指定数据库中所有对象的分配和结构完整性。 此任务可以检查单个数据库或多个数据库，您还可以选择是否也检查数据库索引。  
  
 “检查数据库完整性”任务封装 DBCC CHECKDB 语句。 有关详细信息，请参阅 [DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)。  
  
## “检查数据库完整性”任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“检查数据库完整性”任务（维护计划）](../../relational-databases/maintenance-plans/check-database-integrity-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
  