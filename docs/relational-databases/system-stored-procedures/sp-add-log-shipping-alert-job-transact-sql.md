---
title: sp_add_log_shipping_alert_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_alert_job_TSQL
- sp_add_log_shipping_alert_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_alert_job
ms.assetid: dd95d96e-8963-4aa9-bdcc-3e4b1bc002d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c654f8e76a25c0588011afecc632d3f85a33455
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492915"
---
# <a name="spaddlogshippingalertjob-transact-sql"></a>sp_add_log_shipping_alert_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程用于检查是否已在此服务器上创建了警报作业。 如果警报作业不存在，此存储的过程创建的警报作业，并将添加到其作业 ID **log_shipping_monitor_alert**表。 默认情况下，将启用警报作业并按计划每两分钟运行一次。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_log_shipping_alert_job  
[, [ @alert_job_id = ] alert_job_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
`[ @alert_job_id = ] alert_job_id OUTPUT` [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志传送警报作业的代理作业 ID。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_add_log_shipping_alert_job**必须从运行**主**在监视服务器上的数据库。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示执行**sp_add_log_shipping_alert_job**若要创建一个警报作业 id。  
  
```  
USE master  
GO  
EXEC sp_add_log_shipping_alert_job;  
```  
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
