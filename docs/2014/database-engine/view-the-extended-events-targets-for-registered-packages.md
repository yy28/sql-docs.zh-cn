---
title: 查看已注册包的扩展的事件目标 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- targets [SQL Server extended events]
- viewing event targets
- extended events [SQL Server], viewing targets
ms.assetid: 4985aa5f-ac99-49f6-852c-9d25916549e9
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1c5552ca54f3297226fad6a15de2d5c80bc49067
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014884"
---
# <a name="view-the-extended-events-targets-for-registered-packages"></a>查看已注册包的扩展事件目标
  在创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 扩展事件会话之前，确定可用的扩展事件目标将非常有用。 若要完成此任务，需使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查询编辑器执行以下过程。  
  
 此过程中的语句完成后，查询编辑器的 **“结果”** 选项卡将显示以下两列：  
  
-   package_name  
  
-   target_name  
  
## <a name="to-view-the-extended-events-targets-for-registered-packages-using-query-editor"></a>使用查询编辑器查看已注册包的扩展事件目标  
  
-   在查询编辑器中发出以下语句：  
  
    ```  
    USE msdb  
    SELECT p.name package_name, o.name target_name  
    FROM sys.dm_xe_objects o  
    JOIN sys.dm_xe_packages p  
         ON o.package_guid = p.guid  
    WHERE o.object_type = 'target'  
    ```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_objects (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
