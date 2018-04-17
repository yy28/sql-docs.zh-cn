---
title: dbo.syssessions (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs:
- TSQL
helpviewer_keywords:
- syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c57fa0bcb9c7f8c8c359b8aab629be3d111d7d1a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理时，该代理都会创建一个新会话。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务意外重新启动或停止时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将使用该会话来保留作业的状态。 每一行**syssessions**表包含有关某个会话的信息。 使用**sysjobactivity**表若要查看在每个会话结束的作业状态。  
  
 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理会话的 ID。|  
|**agent_start_date**|**datetime**|为此会话启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务的日期和时间。|  
  
## <a name="remarks"></a>注释  
 只有成员的用户的**sysadmin**固定的服务器角色可以访问此表。  
  
## <a name="see-also"></a>另请参阅  
 [dbo.sysjobactivity &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
