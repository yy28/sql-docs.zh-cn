---
title: "sys.sysconstraints (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysconstraints
- sys.sysconstraints
- sysconstraints_TSQL
- sys.sysconstraints_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.sysconstraints compatibility view
- sysconstraints system table
ms.assetid: f2b2e2ad-ba24-48a1-913c-8ee4e0895dc4
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 99b213b6b385a1551dda2daeac21c856b70d0284
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="syssysconstraints-transact-sql"></a>sys.sysconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  包含约束映射，映射到数据库中拥有该约束的对象。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|约束号。|  
|**id**|**int**|拥有该约束的表 ID。|  
|**colid**|**int**|在其中定义约束的列 ID。<br /><br /> 0 = 表约束|  
|**spare1**|**tinyint**|保留|  
|**status**|**int**|Pseudo-bit-mask 指示状态。 可能的值包括：<br /><br /> 1 = PRIMARY KEY 约束<br /><br /> 2 = UNIQUE KEY 约束<br /><br /> 3 = FOREIGN KEY 约束<br /><br /> 4 = CHECK 约束<br /><br /> 5 = DEFAULT 约束<br /><br /> 16 = 列级约束<br /><br /> 32 = 表级约束|  
|**操作**|**int**|保留|  
|**错误**|**int**|保留|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
