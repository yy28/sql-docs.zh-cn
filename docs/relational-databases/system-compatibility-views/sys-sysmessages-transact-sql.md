---
title: sys. sysmessages （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 53f7abe7603430950f14ecad039419f8435cba28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076550"
---
# <a name="syssysmessages-transact-sql"></a>sys.sysmessages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  针对每个可由 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]返回的系统错误或警告都包含相应的一行。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]在用户屏幕上显示错误说明。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**条**|**int**|唯一错误号。|  
|**对应**|**tinyint**|错误的严重级别。|  
|**dlevel**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**2008**|**nvarchar(255)**|对参数占位符错误的解释。|  
|**msglangid**|**smallint**|系统消息组 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;的兼容性视图 &#40;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
