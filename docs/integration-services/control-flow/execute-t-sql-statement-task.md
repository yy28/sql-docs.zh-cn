---
title: "执行 T-SQL 语句任务 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e156f49956a9eb4497a7860ba54f037f7a8ffc1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="execute-t-sql-statement-task"></a>执行 T-SQL 语句任务
  执行 T-SQL 语句任务运行 Transact-SQL 语句。 有关详细信息，请参阅 [Transact-SQL 引用（数据库引擎）](../../t-sql/transact-sql-reference-database-engine.md)和 [Integration Services (SSIS) 查询](../../integration-services/integration-services-ssis-queries.md)。  
  
 此任务类似于执行 SQL 任务。 但是，执行 T-SQL 语句任务只支持 SQL 语言的 Transact-SQL 版本，在使用 SQL 语言的其他方言的服务器上无法使用此任务来运行语句。 如果需要运行参数化查询，将查询结果保存到变量，或使用属性表达式，那么您应当使用执行 SQL 任务而不是执行 T-SQL 语句任务。 有关详细信息，请参阅 [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md)。  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>执行 T-SQL 任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“执行 T-SQL 语句”任务（维护计划）](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)   
 [在 Integration Services 包中执行 MERGE](../../integration-services/control-flow/merge-in-integration-services-packages.md)  
  
  
