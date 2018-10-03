---
title: 获取有关 DDL 触发器的信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- metadata [SQL Server], triggers
- status information [SQL Server], DDL triggers
- DDL triggers, metadata
ms.assetid: 462becea-292a-4b9e-bb98-533e89733911
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 35fdba2dff5f4b68040007c8c5d21c127bd1548c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113759"
---
# <a name="get-information-about-ddl-triggers"></a>获取有关 DDL 触发器的信息
  本节列出的目录视图可用于获取有关 DDL 触发器的信息。  
  
 **获取有关 DDL 触发器可触发的事件或事件组的信息。**  
  
-   [sys.trigger_event_types (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-trigger-event-types-transact-sql)  
  
 **查看触发器的依赖关系**  
  
-   [sys.sql_expression_dependencies (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
-   [sys.dm_sql_referenced_entities (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
-   [sys.dm_sql_referencing_entities (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
## <a name="database-scoped-ddl-triggers"></a>数据库范围内的 DDL 触发器  
 **获取有关数据库范围内的触发器的信息**  
  
-   [sys.triggers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)  
  
 **获取有关激发触发器的数据库事件的信息**  
  
-   [sys.trigger_events (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)  
  
 **查看数据库范围内的触发器的定义**  
  
-   [sys.sql_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
 **获取有关 CLR 数据库范围内的触发器的信息**  
  
-   [sys.assembly_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
## <a name="server-scoped-ddl-triggers"></a>服务器范围内的 DDL 触发器  
 **获取有关服务器范围内的触发器的信息**  
  
-   [sys.server_triggers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)  
  
 **获取有关激发触发器的服务器事件的信息**  
  
-   [sys.server_trigger_events (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)  
  
 **查看服务器范围内的触发器的定义**  
  
-   [sys.server_sql_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)  
  
 **获取有关 CLR 服务器范围内的触发器的信息**  
  
-   [sys.server_assembly_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [DDL 触发器](../triggers/ddl-triggers.md)  
  
  
