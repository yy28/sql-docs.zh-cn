---
title: 获取所有事件的字段 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], getting fields
- xe
ms.assetid: 4e4ee03f-5bca-42ed-a37c-db1c82e3aad2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0838367ad699c1278bb6ec42f28161ba76c6fd5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064788"
---
# <a name="get-the-fields-for-all-events"></a>获取所有事件的字段
  完成此任务涉及在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中使用查询编辑器。  
  
 此过程中的语句完成后，查询编辑器的 **“结果”** 选项卡将显示以下列：  
  
-   package_name  
  
-   event_name  
  
-   event_field  
  
-   field_type  
  
-   column_type  
  
 当配置使用存入桶目标的事件会话时，可以使用上述信息。 有关详细信息，请参阅 [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md)。  
  
## <a name="before-you-begin"></a>开始之前  
 创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 扩展事件会话之前，获取有关事件关联字段的信息将非常有用。  
  
## <a name="to-get-the-fields-for-all-events-using-query-editor"></a>使用查询编辑器获取所有事件的字段  
  
-   在查询编辑器中发出以下语句：  
  
    ```  
    select p.name package_name, o.name event_name, c.name event_field, c.type_name field_type, c.column_type column_type  
    from sys.dm_xe_objects o  
    join sys.dm_xe_packages p  
          on o.package_guid = p.guid  
    join sys.dm_xe_object_columns c  
          on o.name = c.object_name  
    where o.object_type = 'event'  
    order by package_name, event_name  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [sys. dm_xe_objects &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
