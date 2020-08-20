---
description: sys.sysmessages (Transact-SQL)
title: " (Transact-sql) sys.sys消息 |Microsoft Docs"
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysmessages
- sysmessages
- sysmessages_TSQL
- sys.sysmessages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.sysmessages compatibility view
ms.assetid: 44bee7d9-7517-4071-99be-8b36f979c7cc
author: rothja
ms.author: jroth
ms.openlocfilehash: c54d1cd0db8de1753a6dd81bfbde71c6944df6e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475120"
---
# <a name="syssysmessages-transact-sql"></a>sys.sysmessages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  针对每个可由 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]返回的系统错误或警告都包含相应的一行。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]在用户屏幕上显示错误说明。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**error**|**int**|唯一错误号。|  
|severity |**tinyint**|错误的严重级别。|  
|**dlevel**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|description|**nvarchar(255)**|对参数占位符错误的解释。|  
|**msglangid**|**smallint**|系统消息组 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
