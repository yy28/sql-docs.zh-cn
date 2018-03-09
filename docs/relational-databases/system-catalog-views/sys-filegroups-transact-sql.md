---
title: "sys.filegroups (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.filegroups_TSQL
- filegroups
- sys.filegroups
- filegroups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filegroups catalog view
ms.assetid: 9e851f72-1f8e-4515-a25d-152ebc12ed56
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91198ea3ed94496ff116014e0df2b1b067e4bf16
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysfilegroups-transact-sql"></a>sys.filegroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  每个作为文件组的数据空间都在表中对应一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**|--|该视图继承的列的列表，请参阅[sys.data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**filegroup_guid**|**uniqueidentifier**|文件组的 GUID。<br /><br /> NULL = PRIMARY 文件组|  
|**log_filegroup_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，其值为 NULL。|  
|**is_read_only**|**bit**|1 = 文件组为只读文件组。<br /><br /> 0 = 文件组为可读/写的文件组。|  
|**is_autogrow_all_files**|**bit**|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。<br /><br /> 1 = 时自动增长阈值，文件组中的所有文件增长文件组符合中的文件。<br /><br /> 0 = 时自动增长阈值，只将该文件增长文件组符合中的文件。 这是默认设置。|  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [数据空间 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
  
