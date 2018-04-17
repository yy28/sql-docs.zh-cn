---
title: sysarticlecolumns （系统视图） (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9817b7bcdf407ce359ed903e56de636613ff7478
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns（系统视图）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysarticlecolumns**视图将显示有关已发布的文章中的列的其他信息。 此视图存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|标识项目。|  
|**colid**|**int**|标识项目中的列。|  
|**is_udt**|**int**|表示列是否为用户定义数据类型 (UDT) 列。 值为**1**表示 UDT 列。|  
|**is_xml**|**int**|如果列是**xml**列。 值为**1**指示**xml**列。|  
|**is_max**|**int**|如果列是较大的值数据类型列 (**varchar （max)**， **nvarchar (max)**或**varbinary （max)**)。 值为**1**表示较大的值列。|  
  
## <a name="see-also"></a>另请参阅  
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
