---
title: sysmergesubsetfilters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sysmergesubsetfilters
- sysmergesubsetfilters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubsetfilters system table
ms.assetid: f91d1c6c-3132-47f6-926c-88f56848cafe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0b87c85c3d45c87aed84604bb0b7732c47ffa5e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783275"
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含分区项目的联接筛选信息。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**filtername**|**sysname**|用于创建项目的筛选器名称。|  
|**join_filterid**|**int**|表示联接筛选器的对象 ID。|  
|**pubid**|**uniqueidentifier**|发布 ID。|  
|**artid**|**uniqueidentifier**|项目的 ID。|  
|**art_nickname**|**int**|项目的别名。|  
|**join_articlename**|**sysname**|表名，要联接该表以确定行是否属于该表。|  
|**join_nickname**|**int**|表的别名，要联接该表以确定行是否属于该表。|  
|**join_unique_key**|**int**|表示的唯一键上联接**join_tablename**:<br /><br /> 0 = 不是唯一键。<br /><br /> 1 = 是唯一键。|  
|**expand_proc**|**sysname**|存储过程名，合并代理使用该存储过程识别需要向订阅服务器发送或从订阅服务器中删除的行。|  
|**join_filterclause**|**nvarchar(1000)**|用于联接的筛选子句。|  
|**filter_type**|**tinyint**|指定筛选器类型，可以为下面的一种：<br /><br /> 1 = 联接筛选器。<br /><br /> 2 = 逻辑记录链接。<br /><br /> 3 = 同时为联接筛选器和逻辑记录链接。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
