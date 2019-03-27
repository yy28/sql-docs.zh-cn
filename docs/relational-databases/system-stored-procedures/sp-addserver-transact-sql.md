---
title: sp_addserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addserver
- sp_addserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab5c15d15c77688c06eedec1d54e82c7b8199380
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492925"
---
# <a name="spaddserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定义  本地实例的名称。 当计算机承载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是重命名，使用**sp_addserver**以通知的实例[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的新计算机名称。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必须在该计算机承载的所有实例上执行此过程。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 无法更改的实例名称。 若要更改命名实例的实例名称，安装具有所需名称的新实例、从旧实例中分离数据库文件、将数据库附加到新实例并删除旧实例。 或者，你可以在客户端计算机上创建客户端别名名称，无需更改服务器计算机上的实例名称即可将连接重定向到其他服务器和实例名称或 **服务器:端口** 组合。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @server = ] 'server'` 是服务器的名称。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 服务器名称必须唯一且必须符合  Windows 计算机名称的规则，但不允许包含空格。 *server* 的数据类型为 **sysname**，无默认值。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果计算机上安装了多个  实例，则实例将如同在一个独立服务器上运行。 通过引用指定命名的实例*服务器*作为*servername\instancename*。  
  
`[ @local = ] 'LOCAL'` 指定要添加为本地服务器的服务器。 **@local** 是**varchar(10)**，默认值为 NULL。 指定**@local**作为**本地**定义**@server**作为名称的本地服务器和原因会 @@SERVERNAME函数返回值 *server* 。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会在安装过程中将此变量设置为计算机名称。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认情况下，用户可通过计算机名连接到  的实例而无需额外的配置。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 只有重新启动后，本地的定义才会生效。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]每个实例中只能定义一个本地服务器。  
  
`[ @duplicate_ok = ] 'duplicate_OK'` 指定是否允许重复的服务器名称。 **@duplicate_OK** 是**varchar(13)**，默认值为 NULL。 **@duplicate_OK** 只能具有值**duplicate_OK**或为 NULL。 如果**duplicate_OK**指定且已添加的服务器名称存在，则不会引发错误。 如果未使用命名的参数， **@local**必须指定。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 若要设置或清除服务器选项，请使用**sp_serveroption**。  
  
 **sp_addserver**不能在用户定义的事务内使用。  
  
 使用**sp_addserver**添加远程服务器已停止使用。 改用 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 。  
  
## <a name="permissions"></a>权限  
  要求具有 setupadmin 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 下面的示例将承载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机名称的 `ACCOUNTS`条目更改为 。  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>请参阅  
 [重命名承载 SQL Server 的独立实例的计算机](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
