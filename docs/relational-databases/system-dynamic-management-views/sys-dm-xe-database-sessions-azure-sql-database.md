---
title: sys.dm_xe_database_sessions （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 28759d7101a8a798223a92b9201e0e9aa930a4fa
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984196"
---
# <a name="sysdmxedatabasesessions-azure-sql-database"></a>sys.dm_xe_database_sessions （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关会话事件的信息。 事件是离散执行点。 如果事件不包含所需的信息，则可对事件应用谓词以阻止其激发。  
  
||  
|-|  
|**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 不可为 null。|  
|event_name|**nvarchar(60)**|操作绑定到的事件的名称。 不可为 null。|  
|event_package_guid|**uniqueidentifier**|包含事件的包的 GUID。 不可为 null。|  
|event_predicate|**nvarchar(2048)**|应用于事件的谓词树的 XML 表示形式。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求拥有 VIEW DATABASE STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
截至 2015年-07-13 sys.dm_xe_objects 是一个不包含其名称中的 _database 这些 XEvents Dmv。 不是拼写错误或以下表的右侧列中的错误。 名称是 Microsoft SQL Server 和 Azure SQL 数据库中相同的。 GeneMi。  
  
|From|若要|关系|  
|--------|------|----------------|  
|sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions.address|多对一|  
|sys.dm_xe_database_session_events.event_package_guid、 sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name、sys.dm_xe_objects.package_guid|多对一|  
  
## <a name="see-also"></a>请参阅  
[Azure SQL 数据库中扩展的事件](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
 
