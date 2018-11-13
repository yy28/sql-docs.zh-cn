---
title: sp_addscriptexec (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42bc6c0c89c5f697eabec38485a70a955ffe456e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722755"
---
# <a name="spaddscriptexec-transact-sql"></a>sp_addscriptexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将 SQL 脚本（.sql 文件）发布到发布的所有订阅服务器。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=** ] **'***发布*****  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@scriptfile=** ] **'***scriptfile*****  
 SQL 脚本文件的完整路径。 *scriptfile*是**nvarchar(4000)**，无默认值。  
  
 [ **@skiperror=** ] **'***skiperror*****  
 指示在脚本处理过程中遇到错误时是否停止分发代理或合并代理。 *SkipError*是**位**，默认值为 0。  
  
 **0** = 代理将停止。  
  
 **1** = 代理继续处理脚本并将忽略该错误。  
  
 [ **@publisher=** ] **'***发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*从发布时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_addscriptexec**事务复制和合并复制中使用。  
  
 **sp_addscriptexec**不用于快照复制。  
  
 若要使用**sp_addscriptexec**，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务帐户必须具有读取和写入所有脚本的位置的快照位置和读取权限的权限存储。  
  
 [Sqlcmd 实用工具](../../tools/sqlcmd-utility.md)用于在订阅服务器上，执行脚本和连接到订阅数据库时使用的分发代理或合并代理的安全上下文中执行脚本。 代理的以前版本上的运行时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则[osql 实用工具](../../tools/osql-utility.md)而不是[sqlcmd](../../tools/sqlcmd-utility.md)。  
  
 **sp_addscriptexec**可将脚本应用到订阅服务器，并使用[sqlcmd](../../tools/sqlcmd-utility.md)要应用于订阅服务器上的脚本的内容。 但是，因为订阅服务器的配置可以改变，所以在投递到发布服务器前测试的脚本仍可能导致订阅服务器出错。 *skiperror*提供的功能使分发代理或合并代理忽略错误并继续。 使用[sqlcmd](../../tools/sqlcmd-utility.md)若要测试脚本在运行前先**sp_addscriptexec**。  
  
> [!NOTE]  
>  跳过的错误将继续记录在代理历史记录中以供参考。  
  
 使用**sp_addscriptexec**发布使用 FTP 进行快照传递仅支持的脚本文件[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addscriptexec**。  
  
## <a name="see-also"></a>请参阅  
 [同步期间执行脚本&#40;复制 TRANSACT-SQL 编程&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [同步数据](../../relational-databases/replication/synchronize-data.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
