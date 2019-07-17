---
title: sp_cycle_agent_errorlog (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
author: stevestein
ms.author: sstein
ms.openlocfilehash: c95cc2db84bdf059437a45e2719bbc63d6eb6829
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108355"
---
# <a name="spcycleagenterrorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  关闭当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志文件，并循环 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志扩展编号（就像重新启动服务器）。 新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志包含一个表示已创建新日志的行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 每次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理已启动，当前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理错误日志重命名为**SQLAgent.1**;**SQLAgent.1**变得**SQLAgent.2**， **SQLAgent.2**变得**SQLAgent.3**，依次类推。 **sp_cycle_agent_errorlog**使您能够循环错误日志文件，而不必停止和启动服务器。  
  
 必须从运行此存储的过程**msdb**数据库。  
  
## <a name="permissions"></a>权限  
 执行权限**sp_cycle_agent_errorlog**的成员仅限于**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将循环 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_cycle_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
