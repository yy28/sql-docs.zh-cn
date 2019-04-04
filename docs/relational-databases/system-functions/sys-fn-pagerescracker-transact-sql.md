---
title: sys.fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Sys.fn_PageResCracker 系统函数的文档。
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 2fc7136b60dba47813b9942316ee6fdfbc64f307
ms.sourcegitcommit: fc1739be9b2735b2bb469979936e76ca2a3830f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58899703"
---
# <a name="sysfnpagerescracker-transact-sql"></a>sys.fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

返回`db_id`， `file_id`，并`page_id`为给定`page_resource`值。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>参数  
*page_resource*    
是 8 字节十六进制格式的数据库页资源。
  
## <a name="tables-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|db_id|**ssNoversion**|数据库 ID|  
|file_id|**ssNoversion**|文件 ID|  
|page_id|**ssNoversion**|页面 ID|  
  
## <a name="remarks"></a>备注  
`sys.fn_PageResCracker` 用于数据库页的 8 字节十六进制表示形式转换为行集包含的数据库 ID，文件 ID 和页的页 ID。   

你可以获取从获得一个有效的页面资源`page_resource`的列[sys.dm_exec_requests &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)动态管理视图或[sys.sysprocesses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)系统视图。 如果使用无效的页面资源返回为 NULL。  
主要用途`sys.fn_PageResCracker`是促进这些视图之间的联接和[sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)动态管理函数，以获取有关页的信息，例如它所属的对象。
  
## <a name="permissions"></a>权限  
用户需求`VIEW SERVER STATE`服务器上的权限。  
  
## <a name="examples"></a>示例  
`sys.fn_PageResCracker`函数可以结合使用[sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)进行故障排除页相关的等待和中阻止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  以下脚本是如何使用这些函数来收集当前正在等待某些类型的页资源的所有活动请求的数据库页信息的示例。 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys.sysprocesses (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
