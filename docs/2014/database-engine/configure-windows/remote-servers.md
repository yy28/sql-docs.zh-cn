---
title: 远程服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e8fd1464857b77139ca0bef310eee8be949d77cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809755"
---
# <a name="remote-servers"></a>远程服务器
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中支持远程服务器只是为了向后兼容。 新应用程序应该改用链接服务器。 有关详细信息，请参阅 [链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)。  
  
 远程服务器配置使客户端能够连接到一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，以便在没有建立单独的连接的情况下在其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上执行存储过程。 此时，客户端所连接的服务器接受客户端的请求，并代表客户端将该请求发送到远程服务器。 远程服务器处理请求，并将所有结果返回到原始的服务器。 服务器再将那些结果传递给客户端。 当设置远程服务器配置时，还应考虑如何建立安全性。  
  
 如果要设置服务器配置以在另一台服务器上执行存储过程，但是没有现有的远程服务器配置，请使用链接服务器而不要使用远程服务器。 您可以对链接服务器执行存储过程和分布式查询；但对远程服务器只能执行存储过程。  
  
## <a name="remote-server-details"></a>远程服务器详细信息  
 远程服务器是成对设置的。 若要设置一对远程服务器，请将这两台服务器配置为彼此将对方识别为远程服务器。  
  
 大多数情况下，不需要为远程服务器设置配置选项。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组将在本地计算机和远程计算机上设置默认值以允许远程服务器连接。  
  
 为了能够进行远程访问，必须在本地和远程计算机上将 **remote access** 配置选项设置为 1。 （这是默认设置。）  **remote access** 控制远程服务器的登录。 可以通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_configure** 存储过程或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]重置此配置选项。 若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中设置选项，请在 **“服务器属性连接”** 页上，使用 **“允许远程连接到此服务器”**。 若要访问“服务器属性连接”页，请在对象资源管理器中右键单击服务器名称，再单击“属性”。 在 **“服务器属性”** 页上，单击 **“连接”** 页。  
  
 在本地服务器中，您可以禁用远程服务器配置，以防止远程服务器中的用户对与其配对的本地服务器进行访问。  
  
## <a name="security-for-remote-servers"></a>远程服务器的安全性  
 若要为远程服务器启用远程过程调用 (RPC)，必须在远程服务器中设置登录映射，并尽可能在运行有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的本地服务器中设置登录映射。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中禁用 RPC。 此配置通过减少服务器的可攻击外围应用来增强其安全性。 使用 RPC 前必须启用此功能。 有关详细信息，请参阅 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)。  
  
### <a name="setting-up-the-remote-server"></a>设置远程服务器  
 必须在远程服务器上设置远程登录映射。 使用这些映射，远程服务器可将某个特定服务器为建立 RPC 连接而传入的登录帐户映射到本地登录帐户。 可以使用 **sp_addremotelogin** 存储过程在远程服务器上设置远程登录映射。  
  
> [!NOTE]  
>  **中不支持** sp_remoteoption  **的** trusted [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项。  
  
### <a name="setting-up-the-local-server"></a>设置本地服务器  
 对于经过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的本地登录帐户，不必在本地服务器上设置登录映射。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用本地登录名和密码连接到远程服务器。 对于经过 Windows 身份验证的登录帐户，可以在定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例与远程服务器建立 RPC 连接时使用的登录名和密码的本地服务器上设置本地登录映射。  
  
 对于 Windows 身份验证创建的登录帐户，必须使用 **sp_addlinkedservlogin** 存储过程创建到登录名和密码的映射。 此登录名和密码必须与远程服务器预期的传入登录名和密码（由 **sp_addremotelogin**所创建）相匹配。  
  
> [!NOTE]  
>  请尽可能使用 Windows 身份验证。  
  
### <a name="remote-server-security-example"></a>远程服务器安全性示例  
 以下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装为例： **serverSend** 和 **serverReceive**。 配置 **serverReceive** 以将传入登录名从 **serverSend**（称为 **Sales_Mary**）映射到 **serverReceive**（称为 **Alice**）中的经过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录名。 将另一个传入帐户从 **serverSend**（称为 **Joe**）映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serverReceive _（称为_ Joe **）中的经过**身份验证的登录帐户。  
  
 下面的 Transact-SQL 代码示例将 `serverSend` 配置为对 `serverReceive` 执行 RPC。  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 在 `serverSend`上创建本地登录映射，以便将经过 Windows 身份验证的登录帐户 `Sales\Mary` 映射到登录帐户 `Sales_Mary`。 `Joe`不需要本地映射，因为默认设置使用相同的登录名和密码，并且 `serverReceive` 中有 `Joe`的映射。  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>查看本地或远程服务器属性  
 可以使用 **xp_msver** 扩展存储过程来查看本地或远程服务器属性。 这些属性包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的版本号、计算机中的处理器类型和数目以及操作系统的版本。 从本地服务器可以查看远程服务器的数据库、文件、登录和工具。 有关详细信息，请参阅 [xp_msver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/xp-msver-transact-sql)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>相关内容  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
 [配置远程访问服务器配置选项](configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
