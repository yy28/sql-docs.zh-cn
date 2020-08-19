---
description: sp_resync_targetserver (Transact-SQL)
title: sp_resync_targetserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 858c2ffe0740c43892ff2245047823c9cecbd12a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469199"
---
# <a name="sp_resync_targetserver-transact-sql"></a>sp_resync_targetserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  重新同步指定目标服务器中的所有多服务器作业。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>参数  
`[ @server_name = ] 'server'` 要重新同步的服务器的名称。 *server* 的数据类型为 **sysname**，无默认值。 如果指定 **all** ，则会重新同步所有目标服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="result-sets"></a>结果集  
 报告 **sp_post_msx_operation** 操作的结果。  
  
## <a name="remarks"></a>备注  
 **sp_resync_targetserver** 删除目标服务器的当前说明集，并为要下载的目标服务器发布新的一组指令。 新指令集中包括一条删除所有多服务器作业的指令，随后是当前以该服务器为目标的每个作业的插入指令。  
  
## <a name="permissions"></a>权限  
 默认情况下， **sysadmin** 固定服务器角色的成员执行此过程的权限。  
  
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
 [sp_help_downloadlist &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [sp_post_msx_operation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
