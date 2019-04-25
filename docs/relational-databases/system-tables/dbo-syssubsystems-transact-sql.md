---
title: dbo.syssubsystems (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d685f5e8837feebffeeeade95697f4f3bfea4c81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470497"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含有关所有可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理子系统的信息。 **Syssubsystems**表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系统的 ID。|  
|**subsystem**|**nvarchar(40)**|子系统的名称。|  
|**description_id**|**int**|消息中的行的 ID **sys.messages**目录包含子系统说明的视图。|  
|**subsystem_dll**|**nvarchar(255)**|子系统 DLL 的位置。|  
|**agent_exe**|**nvarchar(255)**|使用子系统的可执行文件的完整路径。|  
|**start_entry_point**|**nvarchar(30)**|初始化子系统时调用的函数。|  
|**event_entry_point**|**nvarchar(30)**|运行子系统步骤时调用的函数。|  
|**stop_entry_point**|**nvarchar(30)**|子系统运行完成时调用的函数。|  
|**max_worker_threads**|**int**|给定子系统的最大并发步骤数。|  
  
## <a name="remarks"></a>备注  
 只有的成员**sysadmin**固定的服务器角色才能访问此表。  
  
## <a name="see-also"></a>请参阅  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
