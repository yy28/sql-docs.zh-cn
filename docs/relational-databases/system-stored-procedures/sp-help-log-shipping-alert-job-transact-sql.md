---
title: sp_help_log_shipping_alert_job (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_alert_job_TSQL
- sp_help_log_shipping_alert_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_alert_job
ms.assetid: 4d4b4577-c393-4961-b2d3-b56e980b787b
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc50fac70f531643cb39f584426e245fd0c232b8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sphelplogshippingalertjob-transact-sql"></a>sp_help_log_shipping_alert_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程将从日志传送监视器返回警报作业的作业 ID。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_log_shipping_alert_job  
  
```  
  
## <a name="arguments"></a>参数  
 InclusionThresholdSetting  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 此存储过程返回[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理的日志传送警报作业的作业 ID。 如果不存在任何日志传送警报作业，则将返回空结果集。  
  
## <a name="remarks"></a>注释  
 **sp_help_log_shipping_alert_job**必须从运行**master**监视服务器上的数据库。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 & #40;SQL server& #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
