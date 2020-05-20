---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e143c5f995c05b7bf23f62f36ea5681621cccab
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828140"
---
# <a name="sysfilegroups-transact-sql"></a>sys.filegroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  每个作为文件组的数据空间都在表中对应一行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**\<继承列>**|--|有关此视图所继承的列的列表，请参阅[sys.databases&#41;data_spaces &#40;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)。|  
|**filegroup_guid**|**uniqueidentifier**|文件组的 GUID。<br /><br /> NULL = PRIMARY 文件组|  
|**log_filegroup_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，其值为 NULL。|  
|**is_read_only**|**bit**|1 = 文件组为只读文件组。<br /><br /> 0 = 文件组为可读/写的文件组。|  
|**is_autogrow_all_files**|**bit**|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到[当前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658)）。<br /><br /> 1 = 当文件组中的某个文件达到自动增长阈值时，文件组中的所有文件都会增长。<br /><br /> 0 = 当文件组中的某个文件达到自动增长阈值时，只有该文件会增长。 这是默认设置。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [数据空间 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
  
