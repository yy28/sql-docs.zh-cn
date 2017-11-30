---
title: "sys.xml_indexes (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_indexes_TSQL
- xml_indexes_TSQL
- sys.xml_indexes
- xml_indexes
dev_langs: TSQL
helpviewer_keywords: sys.xml_indexes catalog view
ms.assetid: 3408de72-b067-4fda-b5d5-8e856dfd9db3
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8656efb7be654a4249f36784995b6e3d904e53ac
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sysxmlindexes-transact-sql"></a>sys.xml_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个 XML 索引对应返回一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||继承中的列[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。|  
|**using_xml_index_id**|**int**|NULL = 主 XML 索引。<br /><br /> Nonnull = 辅助 XML 索引。<br /><br /> Nonnull 是对主 XML 索引的自我联接引用。|  
|**secondary_type**|**char （1)**|辅助索引的类型说明：<br /><br /> P = PATH 辅助 XML 索引<br /><br /> V = VALUE 辅助 XML 索引<br /><br /> R = PROPERTY 辅助 XML 索引<br /><br /> NULL = 主 XML 索引|  
|**secondary_type_desc**|**nvarchar(60)**|辅助索引的类型说明：<br /><br /> PATH = PATH 辅助 XML 索引<br /><br /> VALUE = VALUE 辅助 XML 索引<br /><br /> PROPERTY = PROPERTY 辅助 xml 索引。<br /><br /> NULL = 主 XML 索引|  
|**xml_index_type**|**tinyint**|索引类型：<br /><br /> 0 = 主 XML 索引<br /><br /> 1 = 辅助 XML 索引<br /><br /> 2 = 选择性 XML 索引<br /><br /> 3 = 辅助选择性 XML 索引|  
|**xml_index_type_description**|**nvarchar(60)**|索引类型的说明：<br /><br /> PRIMARY_XML<br /><br /> 辅助 XML 索引<br /><br /> 选择性 XML 索引<br /><br /> 辅助选择性 XML 索引|  
|**path_id**|**int**|对于除了辅助选择性 XML 索引以外的所有 XML 索引均为 NULL。<br /><br /> 否则为对其生成辅助选择性 XML 索引的已提升路径的 ID。 该值与来自 sys.selective_xml_index_paths 系统视图的 path_id 的值相同。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
