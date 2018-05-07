---
title: sp_cycle_errorlog (Transact SQL) |Microsoft 文档
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
- sp_cycle_errorlog_TSQL
- sp_cycle_errorlog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_errorlog
ms.assetid: 61a12cbf-78a3-4052-8604-3b29d07573fd
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42484c0855123181611bf4881c057dec05b8d1e5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spcycleerrorlog-transact-sql"></a>sp_cycle_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  关闭当前的错误日志文件，并循环错误日志扩展编号（就像重新启动服务器）。 新错误日志包含版本和版权信息，以及表明新日志已创建的一行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cycle_errorlog  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 每次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是启动，当前的错误日志将已重命名为**errorlog.1**;**errorlog.1**变得**errorlog.2**， **errorlog.2**变得**errorlog.3**，依次类推。 **sp_cycle_errorlog**使您能够循环错误日志文件，而停止和启动服务器。  
  
## <a name="permissions"></a>权限  
 执行权限**sp_cycle_errorlog**限于的成员**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将循环 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cycle_agent_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
