---
title: sp_cycle_agent_errorlog (Transact SQL) |Microsoft 文档
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
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 74b0bc568dfa883b6b2eb4c6b19fcf3a38512e9e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238008"
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
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 每次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]启动代理时，当前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理错误日志已重命名为**SQLAgent.1**;**SQLAgent.1**变得**SQLAgent.2**， **SQLAgent.2**变得**SQLAgent.3**，依次类推。 **sp_cycle_agent_errorlog**使您能够循环错误日志文件，而停止和启动服务器。  
  
 必须从运行此存储的过程**msdb**数据库。  
  
## <a name="permissions"></a>权限  
 执行权限**sp_cycle_agent_errorlog**限于的成员**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将循环 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_cycle_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
