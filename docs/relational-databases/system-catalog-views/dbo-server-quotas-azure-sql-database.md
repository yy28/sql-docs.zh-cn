---
title: dbo.server_quotas （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: ''
ms.reviewer: ''
ms.prod_service: sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 02a1d28025fd88694ea4538dc352bc8b7fea51d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662605"
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **重要说明!!** 这适用于 **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 仅 ！**  
>   
>  此功能处于预览状态。 请不要依赖于此功能的特定实现，因为此功能在将来的版本中可能更改或删除。  
  
 返回服务器上可用的数据库配额类型。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|服务器的配额类型。 类型**Premium_database**等效于具有资源保留数据库。|  
|quota_value|**int**|服务器中允许的配额类型数。|  
  
## <a name="permissions"></a>Permissions  
 此视图可供所有用户角色有权连接到虚拟**主**数据库。  
  
## <a name="see-also"></a>请参阅  
 [管理高级数据库](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
