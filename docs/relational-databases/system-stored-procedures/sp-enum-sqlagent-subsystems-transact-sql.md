---
title: sp_enum_sqlagent_subsystems (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c1f9d59f69c486816d289f0c30bd816987045574
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spenumsqlagentsubsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理子系统。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>参数  
 InclusionThresholdSetting  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**subsystem**|**nvarchar(40)**|子系统的名称。|  
|**说明**|**nvarchar(512)**|对子系统的说明。|  
|**subsystem_dll**|**nvarchar(510)**|包含子系统的 DLL 模块。|  
|**agent_exe**|**nvarchar(510)**|子系统所用的可执行模块。|  
|**start_entry_point**|**nvarchar(30)**|在作业步骤执行期间 SQL Server 代理调用的过程。|  
|**event_entry_point**|**nvarchar(30)**|在作业步骤执行期间 SQL Server 代理调用的过程。|  
|**stop_entry_point**|**nvarchar(30)**|在作业步骤执行期间 SQL Server 代理调用的过程。|  
|**max_worker_threads**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将为此子系统启动的最大线程数。|  
|**subsystem_id**|**int**|子系统的标识符。|  
  
## <a name="remarks"></a>注释  
 此过程列出实例中可用的子系统。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 **msdb** 数据库中的 **SQLAgentOperatorRole** 固定数据库角色的权限。  
  
 有关详细信息**SQLAgentOperatorRole**，请参阅[SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
## <a name="see-also"></a>另请参阅  
 [实现 SQL Server 代理安全性](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
