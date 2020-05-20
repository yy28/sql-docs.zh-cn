---
title: sys. dm_xe_database_sessions （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a0c79bba20d6885297e59c20e54141c0f99ccf76
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826646"
---
# <a name="sysdm_xe_database_sessions-azure-sql-database"></a>sys.dm_xe_database_sessions（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关会话事件的信息。 事件是离散执行点。 如果事件不包含所需的信息，则可对事件应用谓词以阻止其激发。  
  
||  
|-|  
|**适用**于： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 不可为 null。|  
|event_name|**nvarchar(60)**|操作绑定到的事件的名称。 不可为 null。|  
|event_package_guid|**uniqueidentifier**|包含事件的包的 GUID。 不可为 null。|  
|event_predicate|**nvarchar(2048)**|应用于事件的谓词树的 XML 表示形式。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求拥有 VIEW DATABASE STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
从2015-07-13，dm_xe_objects "XEvents" 是在其名称中不包含 "_database" 的其中一个 Dmv。 不是下表的右侧列中的错误键入或错误。 Microsoft SQL Server 和 Azure SQL 数据库中的名称相同。  
  
|From|功能|关系|  
|--------|------|----------------|  
|sys. dm_xe_database_session_events event_session_address|sys. dm_xe_database_sessions|多对一|  
|sys. dm_xe_database_session_events event_package_guid，dm_xe_database_session_events event_name|sys.dm_xe_objects.name、sys.dm_xe_objects.package_guid|多对一|  
  
## <a name="see-also"></a>另请参阅  
[Azure SQL 数据库中的扩展事件](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
 
