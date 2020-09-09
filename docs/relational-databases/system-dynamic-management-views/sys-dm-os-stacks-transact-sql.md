---
description: sys.dm_os_stacks (Transact-SQL)
title: sys. dm_os_stacks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_stacks
- dm_os_stacks_TSQL
- sys.dm_os_stacks
- sys.dm_os_stacks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_stacks dynamic management view
ms.assetid: a69b06c4-28f0-4535-8fa1-9f132db4d916
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83b694a70145637dce66e33ea417d1afc660af8e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542108"
---
# <a name="sysdm_os_stacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  此动态管理视图供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部使用以执行下列操作：  
  
-   跟踪调试数据（例如，未完成的分配）。  
  
-   在组件认为已经进行一个调用的地方，假定或验证由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件使用的逻辑。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|是该堆栈分配的唯一地址。 不可为 null。|  
|**frame_index**|**int**|每行表示一个函数调用，该函数调用在特定 **stack_address**按帧索引的升序排序时，返回完整调用堆栈。 不可为 null。|  
|**frame_address**|**varbinary(8)**|函数调用的地址。 不可为 null。|  
  
## <a name="remarks"></a>备注  
 **sys. dm_os_stacks** 要求服务器和其他组件的符号在服务器上出现，才能正确显示信息。  
  
## <a name="permissions"></a>权限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高级层上，需要具有 `VIEW DATABASE STATE` 数据库中的权限。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 标准层和基本层上，需要  **服务器管理员** 或 **Azure Active Directory 管理员** 帐户。   


## <a name="see-also"></a>另请参阅  
  [&#40;Transact-sql 的与操作系统相关的动态管理视图 SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
