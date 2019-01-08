---
title: 其他数据库引擎升级问题 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], upgrading
ms.assetid: 78a1d8e8-fa97-476f-8777-84617d145340
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4fe890744f546e02c91630c5bb0115f5b5c8cb9a
ms.sourcegitcommit: 98324d9803edfa52508b6d5d3554614d0350a0b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321633"
---
# <a name="other-database-engine-upgrade-issues"></a>其他数据库引擎升级问题
  升级顾问的当前版本无法检测到以下升级问题。 请检查以下列出的问题来评估它们对系统的潜在影响。  
  
## <a name="multiple-database-engine-deprecated-features"></a>不推荐使用的多数据库引擎功能  
 不推荐使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或选项：  
  
-   BACKUP LOG 的 NO_LOG 和 TRUNCATE_ONLY 选项  
  
-   BACKUP TRANSACTION  
  
-   RESTORE TRANSACTION  
  
-   DUMP  
  
-   LOAD  
  
-   DBCC CONCURRENCYVIOLATION  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
-   syssegments  
  
 不推荐使用 VIA 协议连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
## <a name="new-data-types"></a>新数据类型  
 以下类型将是保留的系统类型。 请在升级之前或之后重命名会产生冲突的现有用户定义类型。  
  
-   Geography  
  
-   Geometry  
  
-   Datetime2  
  
-   HierarchyID  
  
## <a name="target-table-of-the-output-into-clause-cannot-have-any-defined-triggers"></a>OUTPUT INTO 子句的目标表不能包含任何定义的触发器  
 不支持 OUTPUT INTO 表具有任何启用的触发器的目标表。  
  
## <a name="compile-time-error-for-udfs-when-the-target-of-an-output-into-clause-is-a-table"></a>当 OUTPUT INTO 子句的目标是表时发生 UDF 编译时错误  
 用户定义函数 (UDF) 不能用于执行修改数据库状态的操作。 例如，UDF 无法对任何对象（表变量除外）执行任何 DDL (CREATE/ALTER/DROP) 或 DML (INSERT/UPDATE/DELETE) 操作。  
  
## <a name="merge-is-a-reserved-keyword"></a>MERGE 是保留的关键字  
 MERGE 现在是完全保留的关键字。 应用程序不能再包含名为 MERGE 的对象（表、列等）。  
  
## <a name="rename-cdc-schema"></a>重命名 CDC 架构  
 存在名为 CDC 的架构。 如果此架构名称不能是**变更数据捕获**为数据库启用。  
  
 在启用之前，必须删除 CDC 架构**变更数据捕获**数据库。 此步骤可以在升级之前或之后完成。 若要删除该架构，请使用以下步骤：  
  
1.  使用 ALTER SCHEMA 将对象从 CDC 架构传输到新的架构名称。  
  
2.  验证对于新架构中的对象的权限。  
  
3.  对应用程序进行必要的修改。  
  
4.  使用 DROP SCHEMA 删除 CDC 架构。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
