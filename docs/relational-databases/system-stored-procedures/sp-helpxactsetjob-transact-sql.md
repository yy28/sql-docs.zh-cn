---
title: sp_helpxactsetjob (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpxactsetjob
- sp_helpxactsetjob_TSQL
helpviewer_keywords:
- sp_helpxactsetjob
ms.assetid: 242cea3e-e6ac-4f84-a072-b003b920eb33
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bcea94b8d7e83d74ee9295658943ac41c619628
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpxactsetjob-transact-sql"></a>sp_helpxactsetjob (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示有关 Oracle 发布服务器的 Xactset 作业的信息。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpxactsetjob [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>参数  
 [**@publisher** =] *****发布服务器*****  
 作业所属的非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**jobnumber**|**int**|Oracle 作业编号。|  
|**lastdate**|**varchar(22)**|作业运行的最后日期。|  
|**thisdate**|**varchar(22)**|更改的时间。|  
|**nextdate**|**varchar(22)**|作业将要运行的下一个日期。|  
|**已中断**|**varchar(1)**|指示作业是否中断的标志。|  
|**间隔**|**varchar(200)**|作业的间隔。|  
|**失败**|**int**|作业失败的次数。|  
|**xactsetjobwhat**|**varchar(200)**|作业执行的过程的名称。|  
|**xactsetjob**|**varchar(1)**|作业的状态，可以是以下状态之一：<br /><br /> **1** -启用作业。<br /><br /> **0** -已禁用的作业。|  
|**xactsetlonginterval**|**int**|作业的长间隔。|  
|**xactsetlongthreshold**|**int**|作业的长阈值。|  
|**xactsetshortinterval**|**int**|作业的短间隔。|  
|**xactsetshortthreshold**|**int**|作业的短阈值。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpxactsetjob**快照复制和 Oracle 发布服务器的事务复制中使用。  
  
 **sp_helpxactsetjob**始终返回 Xactset 作业 (HREPL_XactSetJob) 发布服务器上的当前设置。 如果 Xactset 作业当前在作业队列中，它还会从 USER_JOB 数据字典视图（创建在 Oracle 发布服务器的管理员帐户下）返回作业的属性。  
  
## <a name="permissions"></a>权限  
 只有一个的成员**sysadmin**固定的服务器角色可以执行**sp_helpxactsetjob**。  
  
## <a name="see-also"></a>另请参阅  
 [为 Oracle 发布服务器配置事务集作业（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [sp_publisherproperty &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  
