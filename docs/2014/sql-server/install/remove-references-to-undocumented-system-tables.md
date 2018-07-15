---
title: 删除对未记录的系统表的引用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- undocumented system tables [SQL Server]
- system tables [SQL Server]
ms.assetid: 010b1236-2219-4bf4-a6db-e3fc3abfa37a
caps.latest.revision: 28
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d4f0c1789e4f352fe18fd50b6de739b82328a777
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226567"
---
# <a name="remove-references-to-undocumented-system-tables"></a>删除对未记录的系统表的引用
  在早期版本中未记录的许多系统表都已更改或不再存在，因此，如果使用这些表，在升级可能会出现错误。 由于升级顾问查找的是针对系统表名称的引用，因而它将报告任何与系统表同名的用户表。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 删除了以下未记录的系统表：  
  
-   **spt_datatype_info**  
  
-   **spt_datatype_info_ext**  
  
-   **spt_provider_types**  
  
-   **spt_server_info**  
  
-   **spt_values**  
  
-   **sysfulltextnotify**  
  
-   **syslocks**  
  
-   **sysproperties**  
  
-   **sysprotects_aux**  
  
-   **sysprotects_view**  
  
-   **SYSREMOTE_CATALOGS**  
  
-   **SYSREMOTE_COLUMN_PRIVILEGES**  
  
-   **SYSREMOTE_COLUMNS**  
  
-   **SYSREMOTE_FOREIGN_KEYS**  
  
-   **SYSREMOTE_INDEXES**  
  
-   **SYSREMOTE_PRIMARY_KEYS**  
  
-   **SYSREMOTE_PROVIDER_TYPES**  
  
-   **SYSREMOTE_SCHEMATA**  
  
-   **SYSREMOTE_STATISTICS**  
  
-   **SYSREMOTE_TABLE_PRIVILEGES**  
  
-   **SYSREMOTE_TABLES**  
  
-   **SYSREMOTE_VIEWS**  
  
-   **syssegments**  
  
-   **sysxlogins**  
  
## <a name="corrective-action"></a>纠正措施  
 按照下表修改应用程序。  
  
|不再使用|改用|  
|----------------|---------|  
|**sysfulltextnotify**|**TableFulltextPendingChanges** OBJECTPROPERTYEX 函数的属性。|  
|**syslocks**|**sys.dm_tran_locks**动态管理视图或 sp_lock，或**sys.syslockinfo**兼容性视图。|  
|**sysproperties**|**sys.extended_properties**目录视图或**fn_listextendedproperty**函数|  
|**sysxlogins**|**sys.server_principals**目录视图或**syslogins**兼容性视图。|  
|所有**spt_** 表|没有可以替换的表|  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
