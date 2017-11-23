---
title: "sys.partition_schemes (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partition_schemes_TSQL
- partition_schemes
- sys.partition_schemes_TSQL
- sys.partition_schemes
dev_langs: TSQL
helpviewer_keywords: sys.partition_schemes catalog view
ms.assetid: ed557fd5-12b0-4cef-9e4f-440b02e99d1f
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c77fcc9083c46921197554b256ca1af46e159e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionschemes-transact-sql"></a>sys.partition_schemes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  是与分区方案，每个数据空间表中占一行**类型**= ps。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||继承中的列[sys.data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**function_id**|**int**|方案中使用的分区函数的 ID。|  
  
 该视图继承的列的列表，请参阅[sys.data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
