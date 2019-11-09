---
title: sys. dm_xe_database_session_targets
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 860faaa6c9e574feda8d5c28be17a265707fd72e
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844426"
---
# <a name="sysdm_xe_database_session_targets-azure-sql-database"></a>sys.dm_xe_database_session_targets（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关会话目标的信息。  
  
||  
|-|  
|**适用**于： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何将来的版本。|  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 与 sys. dm_xe_database_sessions 之间具有多对一关系。 不可为 null。|  
|target_name|**nvarchar(60)**|会话中目标的名称。 不可为 null。|  
|target_package_guid|**uniqueidentifier**|包含目标的包的 GUID。 不可为 null。|  
|execution_count|**bigint**|已为该会话执行目标的次数。 不可为 null。|  
|execution_duration_ms|**bigint**|目标已经执行的总时间（以毫秒为单位）。 不可为 null。|  
|target_data|**nvarchar(max)**|目标维护的数据，例如事件聚合信息。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求拥有 VIEW DATABASE STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|“关系”|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_targets.event_session_address|sys. dm_xe_database_sessions|多对一|  
  
  
