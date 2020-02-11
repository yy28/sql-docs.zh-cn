---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f5a0707c599b70ec3c006b00eacb5f8c1a8a87b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018340"
---
# <a name="schemas-catalog-views---sysschemas"></a>架构目录视图-sys.databases
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  每个数据库架构都对应一行。  
  
> [!NOTE]  
>  数据库架构不同于 XML 架构，XML 架构用于定义 XML 文档的内容模型。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**路径名**|**sysname**|架构的名称。 在该数据库中是唯一的。|  
|**schema_id**|**int**|架构的 ID。 在该数据库中是唯一的。|  
|**principal_id**|**int**|此架构所属的主体数据库的 ID。|  
  
## <a name="remarks"></a>备注  
数据库架构充当可在**sys.databases**目录视图中找到的对象（如表、视图、过程和函数）的命名空间或容器。  

每个架构都有一个所有者。 所有者为安全[主体](../../relational-databases/security/authentication-access/principals-database-engine.md)。
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
[主体](../../relational-databases/security/authentication-access/principals-database-engine.md)

[目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[&#40;Transact-sql&#41;的架构目录视图](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   

[sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
