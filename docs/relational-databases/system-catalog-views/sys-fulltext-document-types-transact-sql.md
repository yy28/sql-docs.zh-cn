---
title: sys.fulltext_document_types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fulltext_document_types_TSQL
- fulltext_document_types
- fulltext_document_types_TSQL
- sys.fulltext_document_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_document_types catalog view
ms.assetid: 156fcfa4-7304-4a5c-b96f-1c3e061e5df0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26a1729aac9094d0b0f150d64772229d7f89c20a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysfulltextdocumenttypes-transact-sql"></a>sys.fulltext_document_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为可用于全文索引操作的每个文档类型返回一行。 每行表示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中注册的 IFilter 接口。  
  
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|支持的文档类型的文件扩展名。<br /><br /> 此值可用于标识在全文索引的类型的列期间将使用的筛选器**varbinary （max)**或**映像**。|  
|**class_id**|**uniqueidentifier**|支持文件扩展名的 IFilter 类的 GUID。|  
|**path**|nvarchar(260)|IFilter DLL 的路径。 路径是仅对成员的可见**serveradmin**固定的服务器角色。|  
|**version**|**sysname**|IFilter DLL 的版本。|  
|**manufacturer**|**sysname**|IFilter 制造商的名称。<br /><br /> 注意： 仅记录与为制造商[!INCLUDE[msCoName](../../includes/msconame-md.md)]上支持[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
