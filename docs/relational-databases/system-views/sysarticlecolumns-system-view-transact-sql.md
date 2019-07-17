---
title: sysarticlecolumns （系统视图） (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a0505b8316254090fe5f2310fa68011d8289679
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129549"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns（系统视图）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysarticlecolumns**视图显示有关已发布的文章中的列的其他信息。 此视图存储在分发数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|标识项目。|  
|**列 id**|**int**|标识项目中的列。|  
|**is_udt**|**int**|表示列是否为用户定义数据类型 (UDT) 列。 值为**1**指示 UDT 列。|  
|**is_xml**|**int**|是如果列为**xml**列。 值为**1**指示**xml**列。|  
|**is_max**|**int**|如果列是大值数据类型列 (**varchar （max)** ， **nvarchar （max)** 或**varbinary （max)** )。 值为**1**指示大型值列。|  
  
## <a name="see-also"></a>请参阅  
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
