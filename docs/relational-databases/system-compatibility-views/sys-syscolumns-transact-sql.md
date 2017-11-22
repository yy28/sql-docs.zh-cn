---
title: "sys.syscolumns (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-enginel, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscolumns
- sys.syscolumns_TSQL
- syscolumns_TSQL
- syscolumns
dev_langs: TSQL
helpviewer_keywords:
- syscolumns system table
- sys.syscolumns compatibility view
ms.assetid: 863fd87b-ff33-4ac5-9aa9-df21140681da
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 94f43de0bf804d366b599c053d8dddadf51d809f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syssyscolumns-transact-sql"></a>sys.syscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  为每个表和视图中的每列返回一行，并为数据库中的存储过程的每个参数返回一行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|列或过程参数的名称。|  
|**id**|**int**|此列所属表的对象 ID，或者与此参数关联的存储过程的 ID。|  
|**xtype**|**tinyint**|从物理存储类型**sys.types**。|  
|**typestat**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**int**|扩展的用户定义数据类型的 ID。 如果数据类型的数字超过 32,767，则溢出或返回 NULL。|  
|**长度**|**int**|从最大的物理存储长度**sys**。**类型**。|  
|**xprec**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|列 ID 或参数 ID。|  
|**拼音**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**保留**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|此列的默认值的 ID。|  
|**域**|**int**|此列的规则或 CHECK 约束的 ID。|  
|**数**|**int**|过程分组时的子过程号。<br /><br /> 0 = 非过程项|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**varbinary （8000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**偏移量**|**int**|此列所在行的偏移量。|  
|**collationid**|**int**|列的排序规则的 ID。 对于非字符列，此值为 NULL。|  
|**status**|**tinyint**|用于说明列或参数的属性的位图：<br /><br /> 0x08 = 列允许空值。<br /><br /> 0x10 = ANSI 填充已在时生效**varchar**或**varbinary**已将列添加。 尾随空格会保留，以便**varchar**和尾随零会保留，以便**varbinary**列。<br /><br /> 0x40 = 参数为 OUTPUT 参数。<br /><br /> 0x80 = 列为标识列。|  
|**type**|**tinyint**|从物理存储类型**sys**。**类型**。|  
|**usertype**|**int**|中的用户定义数据类型的 ID **sys.types**。 如果数据类型的数字超过 32,767，则溢出或返回 NULL。|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|此列的精度级别。<br /><br /> 为-1 = **xml**或较大的值类型。|  
|**缩放**|**int**|此列的小数位数。<br /><br /> NULL = 数据类型不是数值。|  
|**iscomputed**|**int**|指示列是否为计算列的标志：<br /><br /> 0 = 非计算列。<br /><br /> 1 = 计算列。|  
|**isoutparam**|**int**|指示过程参数是否为输出参数：<br /><br /> 1 = True<br /><br /> 0 = False|  
|**isnullable**|**int**|指示列是否允许空值：<br /><br /> 1 = True<br /><br /> 0 = False|  
|**排序规则**|**sysname**|列的排序规则的名称。 如果不是基于字符的列，则为 NULL。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
