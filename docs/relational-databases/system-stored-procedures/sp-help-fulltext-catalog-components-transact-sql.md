---
title: sp_help_fulltext_catalog_components （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalog_components_TSQL
- sp_help_fulltext_catalog_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalog_components
ms.assetid: fbd6a3d4-6a4c-42a2-bff8-2a5eb0745e47
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6fae0542a38a215d79228674fa6b2a9fbe4b9eb7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728200"
---
# <a name="sp_help_fulltext_catalog_components-transact-sql"></a>sp_help_fulltext_catalog_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  返回用于当前数据库中所有全文目录的所有组件（筛选器、断字符和协议处理程序）的列表。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_fulltext_catalog_components  
```  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**全文目录名称**|**int**|全文目录的名称。|  
|**全文目录 id**|**sysname**|全文目录的 ID。|  
|**componenttype**|**sysname**|组件的类型。 下列情况之一：<br /><br /> 筛选器<br /><br /> 协议处理程序<br /><br /> 断字符|  
|**componentname**|**sysname**|组件的名称。|  
|**clsid**|**uniqueidentifier**|组件的类标识符。|  
|**fullpath**|**nvarchar(256)**|指向组件位置的路径。<br /><br /> NULL = 调用方不是**serveradmin**固定服务器角色的成员。|  
|**version**|**nvarchar(30)**|组件的版本。|  
|**提供**|**sysname**|组件制造商的名称。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的全文搜索和语义搜索存储过程](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [sys. fulltext_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_system_components &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)  
  
  
