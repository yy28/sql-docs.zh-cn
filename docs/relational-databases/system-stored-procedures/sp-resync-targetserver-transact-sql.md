---
title: "sp_resync_targetserver (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 893b053fc258eda26db679530a2a6c67f4fbc27b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spresynctargetserver-transact-sql"></a>sp_resync_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  重新同步指定目标服务器中的所有多服务器作业。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>参数  
 [  **@server_name =**] *服务器*  
 要重新同步的服务器的名称。 *server* 的数据类型为 **sysname**，无默认值。 如果**所有**指定，则所有目标服务器重新都同步。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 将报告的结果**sp_post_msx_operation**操作。  
  
## <a name="remarks"></a>注释  
 **sp_resync_targetserver**删除当前的一组指令的目标服务器并发布一组新的目标服务器以下载。 新指令集中包括一条删除所有多服务器作业的指令，随后是当前以该服务器为目标的每个作业的插入指令。  
  
## <a name="permissions"></a>Permissions  
 默认情况下授予 **sysadmin** 固定服务器角色的成员执行此过程的权限。  
  
## <a name="examples"></a>示例  
 以下示例重新同步 `SEATTLE1` 目标服务器。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_resync_targetserver  
    N'SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_help_downloadlist &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [sp_post_msx_operation &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
