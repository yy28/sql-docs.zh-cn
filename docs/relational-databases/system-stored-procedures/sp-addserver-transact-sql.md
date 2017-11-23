---
title: "sp_addserver (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
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
- sp_addserver
- sp_addserver_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a1b6b77613f01605d693d9e2c3961c3278f8d26b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spaddserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本地实例的名称。 当计算机承载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是重命名，使用**sp_addserver**以通知的实例[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]新计算机的名称。 必须在该计算机承载的所有[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例上执行此过程。 无法更改[!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例名称。 若要更改命名实例的实例名称，安装具有所需名称的新实例、从旧实例中分离数据库文件、将数据库附加到新实例并删除旧实例。 或者，你可以在客户端计算机上创建客户端别名名称，无需更改服务器计算机上的实例名称即可将连接重定向到其他服务器和实例名称或 **服务器:端口** 组合。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@server =** ] *服务器*  
 服务器的名称。 服务器名称必须唯一且必须符合 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 计算机名称的规则，但不允许包含空格。 *server* 的数据类型为 **sysname**，无默认值。  
  
 如果计算机上安装了多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，则实例将如同在一个独立服务器上运行。 通过引用指定命名的实例*服务器*作为*servername\instancename*。  
  
 [  **@local =** ] **'LOCAL'**  
 将正添加的服务器指定为本地服务器。 **@local**是**varchar(10)**，默认值为 NULL。 指定 **@local** 作为**本地**定义 **@server** 作为名称的本地服务器并使 @@SERVERNAME函数返回值*服务器*。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会在安装过程中将此变量设置为计算机名称。 默认情况下，用户可通过计算机名连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例而无需额外的配置。  
  
 只有重新启动[!INCLUDE[ssDE](../../includes/ssde-md.md)]后，本地的定义才会生效。 每个[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例中只能定义一个本地服务器。  
  
 [  **@duplicate_ok =** ] **duplicate_OK**  
 指定是否允许重复的服务器名。 **@duplicate_OK**是**varchar(13)**，默认值为 NULL。 **@duplicate_OK**值只能**duplicate_OK**或 NULL。 如果**duplicate_OK**指定并且已添加的服务器名称存在，则不会引发错误。 如果未使用命名的参数，  **@local** 必须指定。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 若要设置或清除服务器选项，使用**sp_serveroption**。  
  
 **sp_addserver**不在用户定义的事务内使用。  
  
 使用**sp_addserver**添加远程服务器已停止使用。 改用 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 。  
  
## <a name="permissions"></a>Permissions  
  要求具有 setupadmin 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例将承载 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的计算机名称的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]条目更改为 `ACCOUNTS`。  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>另请参阅  
 [重命名承载 SQL Server 的独立实例的计算机](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropserver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
