---
title: DISCOVER_DB_CONNECTIONS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3ccdd4496b075c976bfaecb4d7eb9db43560f3c3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="discoverdbconnections-rowset"></a>DISCOVER_DB_CONNECTIONS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供当前打开的服务器到数据库连接的资源使用情况和活动信息。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_DB_CONNECTIONS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CONNECTION_CATALOG_NAME**|**DBTYPE_WSTR**||当前连接到的数据库的数据库名称。|  
|**CONNECTION_ID**|**DBTYPE_I4**||标识连接的唯一编号。|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**||自连接开始后的空闲时间（毫秒）。|  
|**CONNECTION_IN_USE**|**DBTYPE_I4**||指示连接是活动状态 (1) 还是空闲状态 (0)。|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||上次命令执行结束时的服务器 UTC 日期和时间。|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||上次命令启动执行时的服务器 UTC 日期和时间。|  
|**CONNECTION_SERVER_NAME**|**DBTYPE_WSTR**||当前连接到的服务器的名称。|  
|**CONNECTION_SPID**|**DBTYPE_I4**||会话 ID。|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||启动连接时的服务器 UTC 日期和时间。|  
|**CONNECTION_USAGE_TIME_MS**|**DBTYPE_I8**||自连接开始后的连接活动时间（毫秒）。|  
  
 未对此架构行集进行排序。  
  
> [!IMPORTANT]  
>  **DISCOVER_DB_CONNECTIONS**行集将仅显示信息时服务连接到关系数据源。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_DB_CONNECTIONS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|CONNECTION_ID|DBTYPE_I4|選擇性。|  
|CONNECTION_IN_USE|DBTYPE_I4|選擇性。|  
|CONNECTION_SERVER_NAME|DBTYPE_WSTR|選擇性。|  
|CONNECTION_CATALOG_NAME|DBTYPE_WSTR|必需的。|  
|CONNECTION_SPID|DBTYPE_I4|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
