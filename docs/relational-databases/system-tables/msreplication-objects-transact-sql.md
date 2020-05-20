---
title: MSreplication_objects （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d09ff7f8a1be28c39345ecd56084ae6392ca66d8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829861"
---
# <a name="msreplication_objects-transact-sql"></a>MSreplication_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于与订阅服务器数据库中的复制相关联的每个对象， **MSreplication_objects**表在表中各占一行。 该表存储在订阅数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**器**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**object_name**|**sysname**|对象的名称。|  
|**object_type**|**char(2)**|对象类型：<br /><br /> **u** = 表。<br /><br /> **t** = 触发器。<br /><br /> **p** = 存储过程。|  
|**下文**|**sysname**|与对象关联的项目的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
