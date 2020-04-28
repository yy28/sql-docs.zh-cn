---
title: IHsyscolumns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: a432685809676f997049940ea5aa1ce43dc38a60
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029636"
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHsyscolumns**视图显示从非 SQL Server 发布服务器发布的项目的列信息。 此视图存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name |**sysname**|列名或过程参数的名称。|  
|**id**|**int**|此列所属的表的对象 ID，或与此参数关联的存储过程的 ID。|  
|**xtype**|**tinyint**|Systypes 中的物理存储类型[&#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)。|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|扩展的用户定义数据类型的 ID。|  
|**length**|**bigint**|[Systypes &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)中的最大物理存储长度。|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|列或参数 ID。|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**保护**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|此列默认的 ID。|  
|**域名**|**int**|此列的规则的 ID 或 CHECK 约束的 ID。|  
|**数字**|**int**|对过程分组时的子过程号（**0**表示表示条目）。|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**偏移量**|**int**|此列显示在该行中的偏移量。|  
|**collationid**|**int**|列排序规则的 ID。 对于基于非字符的列为 NULL。|  
|**语言**|**int**|列的语言标识符。|  
|**status**|**int**|用于描述列或参数的属性的位图：<br /><br /> **0x08** = 列允许 null 值。<br /><br /> **0x10** = 在添加**varchar**或**varbinary**列后，ANSI 填充已生效。 为**varchar**保留尾随空格，并保留**varbinary**列的尾随零。<br /><br /> **0x40** = 参数是输出参数。<br /><br /> **0x80** = 列是标识列。|  
|**type**|**int**|Systypes 中的物理存储类型[&#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)。|  
|**usertype**|**tinyint**|[Systypes &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)中用户定义数据类型的 ID。|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|此列的精度级别。|  
|**scale**|**int**|此列的小数位数。|  
|**iscomputed**|**int**|指示该列是否为计算列的标志：<br /><br /> **0** = 非计算。<br /><br /> **1** = 计算所得。|  
|**isoutparam**|**int**|指示过程参数是否为输出参数：<br /><br /> **1** = True。<br /><br /> **0** = False。|  
|**isnullable**|**int**|指示列是否允许空值：<br /><br /> **1** = True。<br /><br /> **0** = False。|  
|**归类**|**int**|列排序规则的名称。 对于基于非字符的列为 NULL。|  
|**tdscollation**|**int**|在表格格式数据流 (TDS) 中返回的列的排序规则的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;复制视图](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
