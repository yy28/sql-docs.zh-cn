---
title: MSmerge_settingshistory (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 25505e0b96c627feb51fd59abfe587851520b724
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026559"
---
# <a name="msmergesettingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_settingshistory**表用于维护项目和发布属性对于合并复制，每个所做的更改合并复制拓扑的一个行所做更改的历史记录。 此表还存储有关设置初始属性设置条件的信息。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|事件发生的日期时间。|  
|**pubid**|**uniqueidentifier**|给定发布的唯一标识号。|  
|**artid**|**uniqueidentifier**|给定项目的唯一标识号。|  
|**eventtype**|**tinyint**|指定要记录的事件类型，可以是下列类型之一：<br /><br /> **1** -初始发布级别属性设置。<br /><br /> **2** -更改发布属性中。<br /><br /> **101** -初始项目属性设置。<br /><br /> **102** -更改项目属性中。|  
|propertyname |**sysname**|设置或更改的属性的名称|  
|**previousvalue**|**sysname**|被更改的属性的以前的属性值。|  
|**newvalue**|**sysname**|更改后或创建时的属性值。|  
|**eventtext**|**nvarchar(2000)**|说明事件的字符串。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
