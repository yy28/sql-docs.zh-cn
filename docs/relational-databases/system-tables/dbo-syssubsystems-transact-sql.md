---
title: "dbo.syssubsystems (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.syssubsystems
- syssubsystems
- syssubsystems_TSQL
- dbo.syssubsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syssubsystems system table
ms.assetid: 114b3d55-1ad6-4777-b868-8ef0c86ba596
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c525889c9cbb58b76c58da7b1302fcd3d50a4b45
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含有关所有可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理子系统的信息。 **Syssubsystems**表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系统的 ID。|  
|**subsystem**|**nvarchar(40)**|子系统的名称。|  
|**description_id**|**int**|消息中的行的 ID **sys.messages**目录视图，其中包含子系统说明。|  
|**subsystem_dll**|**nvarchar(255)**|子系统 DLL 的位置。|  
|**agent_exe**|**nvarchar(255)**|使用子系统的可执行文件的完整路径。|  
|**start_entry_point**|**nvarchar(30)**|初始化子系统时调用的函数。|  
|**event_entry_point**|**nvarchar(30)**|运行子系统步骤时调用的函数。|  
|**stop_entry_point**|**nvarchar(30)**|子系统运行完成时调用的函数。|  
|**max_worker_threads**|**int**|给定子系统的最大并发步骤数。|  
  
## <a name="remarks"></a>注释  
 只有的成员**sysadmin**固定的服务器角色可以访问此表。  
  
## <a name="see-also"></a>另请参阅  
 [dbo.sysproxysubsystem &#40;Transact SQL &#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact SQL &#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
