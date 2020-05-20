---
title: sp_helpxactsetjob （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpxactsetjob
- sp_helpxactsetjob_TSQL
helpviewer_keywords:
- sp_helpxactsetjob
ms.assetid: 242cea3e-e6ac-4f84-a072-b003b920eb33
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9fbc18b737c4c901527e6dc1684b75c2f5ddedda
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826049"
---
# <a name="sp_helpxactsetjob-transact-sql"></a>sp_helpxactsetjob (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示有关 Oracle 发布服务器的 Xactset 作业的信息。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpxactsetjob [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作业所属的非发布服务器的名称。 *发布服务器*的**sysname**，无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**jobnumber**|**int**|Oracle 作业编号。|  
|**lastdate**|**varchar （22）**|作业运行的最后日期。|  
|**thisdate**|**varchar （22）**|更改的时间。|  
|**nextdate**|**varchar （22）**|作业将要运行的下一个日期。|  
|**broken**|**varchar(1)**|指示作业是否中断的标志。|  
|**interval**|**varchar （200）**|作业的间隔。|  
|**故障**|**int**|作业失败的次数。|  
|**xactsetjobwhat**|**varchar （200）**|作业执行的过程的名称。|  
|**xactsetjob**|**varchar(1)**|作业的状态，可以是以下状态之一：<br /><br /> **1** -作业已启用。<br /><br /> **0** -作业已禁用。|  
|**xactsetlonginterval**|**int**|作业的长间隔。|  
|**xactsetlongthreshold**|**int**|作业的长阈值。|  
|**xactsetshortinterval**|**int**|作业的短间隔。|  
|**xactsetshortthreshold**|**int**|作业的短阈值。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helpxactsetjob**用于 Oracle 发布服务器的快照复制和事务复制。  
  
 **sp_helpxactsetjob**始终在发布服务器上返回 Xactset 作业（HREPL_XactSetJob）的当前设置。 如果 Xactset 作业当前在作业队列中，它还会从 USER_JOB 数据字典视图（创建在 Oracle 发布服务器的管理员帐户下）返回作业的属性。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_helpxactsetjob**执行。  
  
## <a name="see-also"></a>另请参阅  
 [为 Oracle 发布服务器配置事务集作业 &#40;复制 Transact-sql 编程&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [sp_publisherproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  
