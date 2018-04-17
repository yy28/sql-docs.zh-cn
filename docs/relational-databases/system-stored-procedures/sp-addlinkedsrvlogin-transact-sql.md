---
title: sp_addlinkedsrvlogin (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ef468f7ea427e2e7226bccf45e1192c9a6abcc4b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spaddlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建或更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本地实例上的登录名与远程服务器中安全帐户之间的映射。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] 'TRUE' | 'FALSE' | NULL ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>参数  
 [ @rmtsrvname **=** ] **'***rmtsrvname***'**  
 应用登录映射的链接服务器的名称。 *rmtsrvname*是**sysname**，无默认值。  
  
 [ @useself **=** ] **'**TRUE**'** | 'FALSE' | 'NULL'  
 确定是否连接到*rmtsrvname*通过模拟本地登录名或显式提交登录名和密码。 数据类型是**varchar (**8**)**，默认值为 TRUE。  
  
 值为 TRUE 指定登录名使用其自己的凭据来连接到*rmtsrvname*，与*rmtuser*和*rmtpassword*自变量被忽略。 FALSE 指定*rmtuser*和*rmtpassword*参数用于连接到*rmtsrvname*指定*locallogin*. 如果*rmtuser*和*rmtpassword*也是设置为 NULL，任何登录名或密码用于连接到链接服务器。  
  
 [ @locallogin **=** ] **'***locallogin***'**  
 本地服务器上的登录。 *locallogin*是**sysname**，默认值为 NULL。 NULL 指定此项适用于所有连接到的本地登录名*rmtsrvname*。 如果不为 NULL， *locallogin*可以是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或 Windows 登录名。 对于 Windows 登录来说，必须以直接的方式或通过已被授权访问的 Windows 组成员身份授予其访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的权限。  
  
 [ @rmtuser **=** ] *****rmtuser*****  
 是用于连接到的远程登录名*rmtsrvname*时@useself为 FALSE。 远程服务器时的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不使用 Windows 身份验证， *rmtuser*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名。 *rmtuser*是**sysname**，默认值为 NULL。  
  
 [ @rmtpassword **=** ] *****rmtpassword*****  
 密码相关联*rmtuser*。 *rmtpassword*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 当用户登录到本地服务器并执行分布式查询，以访问链接服务器上的表时，本地服务器必须登录链接服务器上，代表该用户访问该表。 使用 sp_addlinkedsrvlogin 来指定本地服务器用于登录链接服务器的登录凭据。  
  
> [!NOTE]  
>  若要在某一链接服务器上使用表时创建最佳查询计划，查询处理器必须具有来自该链接服务器的数据分布统计。 对表的任何列具有有限权限的用户可能没有足够的权限来获取所有有用的统计，并且可能会收到效率较低的查询计划和经历不佳的性能。 如果链接服务器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，若要获取所有可用的统计，用户必须拥有该表或者是链接服务器上 sysadmin 固定服务器角色、db_owner 固定数据库角色或者 db_ddladmin 固定数据库角色的成员。 SQL Server 2012 SP1 修改了这些权限限制以获取统计信息，允许具有 SELECT 权限的用户访问通过 DBCC SHOW_STATISTICS 提供的统计信息。 有关详细信息，请参阅的权限部分[DBCC SHOW_STATISTICS &#40;TRANSACT-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)。  
  
 本地服务器上的所有登录和链接服务器上的远程登录之间的默认映射通过执行 sp_addlinkedserver 自动创建。 默认映射表示，当代表本地登录连接到链接服务器时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用本地登录的用户凭据。 这相当于执行与 sp_addlinkedsrvlogin@useself设置为**true**链接服务器，而无需指定本地用户名称。 使用 sp_addlinkedsrvlogin 只可以更改特定的本地服务器的默认映射或添加新映射。 若要删除默认映射或任何其他映射，请使用 sp_droplinkedsrvlogin。  
  
 当所有下列条件都存在时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以自动地使用正在发出查询的用户的 Windows 安全凭据（Windows 登录名和密码），以连接到链接服务器，而不必使用 sp_addlinkedsrvlogin 来创建一个预设的登录映射：  
  
-   使用 Windows 身份验证模式，用户连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   在客户端和发送服务器上安全帐户委托是可用的。  
  
-   提供程序支持 Windows 身份验证模式（例如，运行于 Windows 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）。  
  
> [!NOTE]  
>  对于单跃点方案，不必启用委托，但对于多跃点方案，则需要启用委托。  
  
 由链接服务器使用映射（此映射通过在本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上执行 sp_addlinkedsrvlogin 而定义）执行身份验证后，对于远程数据库中单个对象的权限将由链接服务器决定，而不是由本地服务器决定。  
  
 不能从用户定义的事务中执行 sp_addlinkedsrvlogin。  
  
## <a name="permissions"></a>权限  
 要求对服务器拥有 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>A. 使用各自的用户凭据将所有本地登录连接到链接服务器  
 以下示例将创建一个映射，以确保所有到本地服务器的登录都使用其各自的用户凭据连接到链接服务器 `Accounts`。  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 或  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  如果为单个登录创建了显式映射，则其优先于此链接服务器的任何全局映射。  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. 使用不同的用户凭据将特定的登录连接到链接服务器  
 以下示例将创建一个映射，以确保 Windows 用户 `Domain\Mary` 使用登录名 `Accounts` 和密码 `MaryP` 连接到链接服务器 `d89q3w4u`。  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  此示例不使用 Windows 身份验证。 密码未经加密而进行传输。 密码可能会显示在数据源定义和脚本保存到磁盘，在备份和日志文件中。 在此类连接中，切勿使用管理员密码。 有关特定于环境的安全指南，请咨询您的网络管理员。  
  
## <a name="see-also"></a>另请参阅  
 [链接的服务器目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
