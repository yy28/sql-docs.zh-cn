---
title: "sp_setnetname (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- sp_setnetname
- sp_setnetname_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_setnetname
ms.assetid: f416ba81-3835-4588-b0a3-2fe75589490e
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e9f439854cc1d3af3ca5db09981f2eba2af7a4f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spsetnetname-transact-sql"></a>sp_setnetname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以设置网络名称**sys.servers**到它们的远程实例的实际网络计算机名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 该过程可用于启用对计算机（其网络名中包含无效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 标识符）的远程存储过程调用执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_setnetname  
@server = 'server',   
     @netname = 'network_name'  
```  
  
## <a name="arguments"></a>参数  
 **@server=** *服务器*   
 在用户编码的远程存储过程调用语法中引用的远程服务器名。 中的一行**sys.servers**必须已存在使用此*服务器*。 *server* 的数据类型为 **sysname**，无默认值。  
  
 **@netname=** *network_name*   
 对其执行远程存储过程调用的计算机网络名。 *network_name*是**sysname**，无默认值。  
  
 该名称必须与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 计算机名相匹配，并且该名称可以包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 标识符中不允许使用的字符。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 如果计算机名包含无效的标识符，对 Windows 计算机的一些远程存储过程调用则可能遇到问题。  
  
 因为链接服务器和远程服务器驻留在相同的命名空间内，所以它们的名称不能相同。 但是，你可以定义链接的服务器和对指定服务器的远程服务器通过分配不同的名称，并通过使用**sp_setnetname**其中之一的网络名称设置为基础的服务器的网络名称。  
  
```  
--Assume sqlserv2 is actual name of SQL Server   
--database server  
EXEC sp_addlinkedserver 'sqlserv2';  
GO  
EXEC sp_addserver 'rpcserv2';  
GO  
EXEC sp_setnetname 'rpcserv2', 'sqlserv2';  
```  
  
> [!NOTE]  
>  使用**sp_setnetname**为链接的服务器指回本地服务器不支持。 以这种方式引用的服务器不能参与分布式事务。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**sysadmin**和**setupadmin**固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
 以下示例显示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上发出远程存储过程调用所使用的典型管理序列。  
  
```  
USE master;  
GO  
EXEC sp_addserver 'Win_1';  
EXEC sp_setnetname 'Win_1','Win-1';  
EXEC Win_1.master.dbo.sp_who;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addserver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
