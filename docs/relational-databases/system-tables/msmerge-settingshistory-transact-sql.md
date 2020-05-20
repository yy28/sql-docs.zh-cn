---
title: MSmerge_settingshistory （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9ac532e5212f32e5ee3bda029a2a7fb5a1231974
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829221"
---
# <a name="msmerge_settingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_settingshistory**表用于维护对合并复制的项目和发布属性所做更改的历史记录，其中每个更改合并复制拓扑。 此表还存储有关设置初始属性设置条件的信息。 该表存储在发布数据库和订阅数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|事件发生的日期时间。|  
|**pubid**|**uniqueidentifier**|给定发布的唯一标识号。|  
|**artid**|**uniqueidentifier**|给定项目的唯一标识号。|  
|**eventtype**|**tinyint**|指定要记录的事件类型，可以是下列类型之一：<br /><br /> **1** -初始发布级别属性设置。<br /><br /> **2** -更改发布属性。<br /><br /> **101** -初始项目属性设置。<br /><br /> **102** -项目属性中的更改。|  
|propertyname |**sysname**|设置或更改的属性的名称|  
|**previousvalue**|**sysname**|被更改的属性的以前的属性值。|  
|**newvalue**|**sysname**|更改后或创建时的属性值。|  
|**eventtext**|**nvarchar （2000）**|说明事件的字符串。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
