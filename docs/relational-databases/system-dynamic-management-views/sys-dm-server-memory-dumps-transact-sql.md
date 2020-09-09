---
description: sys.dm_server_memory_dumps (Transact-SQL)
title: sys. dm_server_memory_dumps (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cec8575270fd7068290cb24f88405453415b3020
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543818"
---
# <a name="sysdm_server_memory_dumps-transact-sql"></a>sys.dm_server_memory_dumps (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]生成的每个内存转储文件返回一行。 使用此动态管理视图解决潜在的问题。  
 
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**filename**|**nvarchar(256)**|内存转储文件的路径和名称。 不能为 null。|  
|**creation_time**|**datetimeoffset(7)**|创建文件的日期和时间。 不能为 null。|  
|**size_in_bytes**|**bigint**|文件的大小（以字节为单位）。 可以为 Null。|  
  
## <a name="general-remarks"></a>一般备注  
 转储类型可以是小型转储、所有线程转储或完整转储。 文件的扩展名为 .mdmp。  
  
## <a name="security"></a>安全性  
 转储文件可能包含敏感信息。 为了帮助保护敏感信息，可以使用访问控制列表 (ACL) 来限制对这些文件的访问，或将这些文件复制到具有受限访问权限的文件夹中。 例如，在将调试文件发送给 Microsoft 支持服务部门之前，建议删除任何敏感或机密信息。  
  
### <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  
  
  
