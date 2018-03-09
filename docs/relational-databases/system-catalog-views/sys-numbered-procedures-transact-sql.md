---
title: "sys.numbered_procedure (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6a8dbd0f26b39c4fda367d2057cb9eb361586c5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysnumberedprocedures-transact-sql"></a>sys.numbered_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  每个作为带编号的过程而创建的 SQL Server 存储过程都占一行。 对于基（编号 = 1）存储过程，它不显示行。 基的存储过程的条目可以找到在视图中比如**sys.objects**和**sys.procedures**。  
  
> [!IMPORTANT]  
>  不推荐使用带编号的过程。 建议您不要使用带编号过程。 当编译使用此目录视图的查询时，将会激发 DEPRECATION_ANNOUNCEMENT 事件。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|存储过程的对象的 ID。|  
|**procedure_number**|**int**|对象中这种过程的数目（2 或更多）。|  
|**定义**|**nvarchar(max)**|用于定义此过程的 SQL Server 文本。<br /><br /> NULL = 已加密。|  
  
> [!NOTE]  
>  带编号的过程不支持 XML 和 CLR 参数。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
