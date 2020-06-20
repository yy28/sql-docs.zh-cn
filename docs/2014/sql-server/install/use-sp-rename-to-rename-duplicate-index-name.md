---
title: 使用 sp_rename 重命名重复的索引名称 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- table names [SQL Server]
- duplicate table names
- index names [SQL Server]
- sp_rename
- duplicate index names
ms.assetid: ee66c7a5-eb6d-4fcf-970c-ab099d78c8d9
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b8ffe3b9befd0c7239d32094e5738e0fb2947c5a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058823"
---
# <a name="use-sp_rename-to-rename-duplicate-index-name"></a>使用 sp_rename 重命名重复的索引名称
  升级顾问检测到重复的表或视图索引名称。 请先重命名重复的索引以消除重复，然后再升级。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
  
1.  执行以下查询找出重复的索引。  
  
    ```  
    SELECT DISTINCT OBJECT_NAME(o.id), name  
    FROM sysindexes as o  
    WHERE EXISTS   
        (SELECT name FROM sysindexes  as i  
          WHERE i.id = o.id  
          AND i.name = o.name and i.indid < o.indid);  
    ```  
  
2.  使用**sp_rename**更改其中一个索引名称。 由于索引名称相同，因此无法确定哪个索引将被重命名。 可通过此步骤区分索引。  
  
    ```  
    EXEC sp_rename N'table_name.index_name', N'new_index_name', N'INDEX'  
    ```  
  
3.  通过执行以下查询来验证哪个索引进行了重命名。 此查询返回指定表或视图的所有索引（包括键列名）。  
  
    ```  
    SELECT i.name AS IndexName, c.name AS ColumnName, ik.colid, ik.keyno  
    FROM sysindexes i  
    JOIN sysindexkeys ik ON i.id = ik.id and i.indid = ik.indid   
    JOIN syscolumns c ON c.id = ik.id and ik.colid = c.colid  
    WHERE i.id = OBJECT_ID('table_or_view_name')  
    ```  
  
4.  如有必要，请再次使用**sp_rename**来更正索引名称。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
