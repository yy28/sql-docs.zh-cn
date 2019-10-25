---
title: SQL Server 中的身份验证
description: 介绍 SQL Server 中的登录名和身份验证，并提供指向其他资源的链接。
ms.date: 09/26/2019
dev_langs:
- csharp
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: eb528eb1045788469b0eb31491fd654997831468
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452314"
---
# <a name="authentication-in-sql-server"></a>SQL Server 中的身份验证

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 支持两种身份验证模式，即 Windows 身份验证模式和混合模式。  
  
- Windows 身份验证是默认模式（通常称为集成安全），因为此 SQL Server 安全模型与 Windows 紧密集成。 可信任特定的 Windows 用户和组帐户登录到 SQL Server。 已经过身份验证的 Windows 用户无需提供其他凭据。  
  
- 混合模式支持由 Windows 和 SQL Server 进行身份验证。 用户名和密码保留在 SQL Server 内。  
  
> [!IMPORTANT]
> 建议尽可能使用 Windows 身份验证。 Windows 身份验证使用一系列加密消息来验证 SQL Server 中的用户。 使用 SQL Server 登录时，会通过网络传递 SQL Server 登录名和加密的密码，这样会降低它们的安全性。  
  
使用 Windows 身份验证时，用户已登录到 Windows，无需另外登录到 SQL Server。 下面的 `SqlConnection.ConnectionString` 可指定 Windows 身份验证，而无需用户提供用户名或密码。  
  
```csharp
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
> 登录名不同于数据库用户。 您必须通过单独的操作将登录名或 Windows 组映射到数据库用户或角色。 然后向用户或角色授予访问数据库对象的权限。  
  
## <a name="authentication-scenarios"></a>身份验证方案  
通常，在下列情况下，Windows 身份验证是最佳选择：  
  
- 存在域控制器。  
  
- 应用程序和数据库位于同一台计算机上。  
  
- 你正在使用 SQL Server Express 或 LocalDB 的实例。  
  
SQL Server 登录名通常用于以下情况：  
  
- 如果有工作组。  
  
- 用户从不受信任的域进行连接。  
  
- Internet 应用程序，如 ASP.NET。  
  
> [!NOTE]
> 指定 Windows 身份验证不会禁用 SQL Server 登录。 使用 ALTER LOGIN DISABLE Transact-SQL 语句会禁用具有高级权限的 SQL Server 登录。  
  
## <a name="login-types"></a>登录类型  
SQL Server 支持三种登录类型：  
  
- 本地 Windows 用户帐户或受信任的域帐户。 SQL Server 依靠 Windows 来对 Windows 用户帐户进行身份验证。  
  
- Windows 组。 授予对 Windows 组的访问权限将授予对作为该组成员的所有 Windows 用户登录名的访问权限。  
  
- SQL Server 登录。 SQL Server 将用户名和密码的哈希都存储在 master 数据库中，使用内部身份验证方法来验证登录尝试。  
  
> [!NOTE]
> SQL Server 提供了从证书或非对称密钥创建的登录名，仅用于代码签名。 不能用于连接到 SQL Server。  
  
## <a name="mixed-mode-authentication"></a>混合模式身份验证  
如果必须使用混合模式身份验证，则必须创建 SQL Server 登录名，这些登录名存储在 SQL Server 中。 然后，必须在运行时提供 SQL Server 用户名和密码。  
  
> [!IMPORTANT]
> 使用名为 `sa` 的 SQL Server 登录名安装 SQL Server （"系统管理员" 的缩写形式）。 为 `sa` 登录名分配一个强密码，但不要在应用程序中使用 `sa` 登录名。 @No__t_0 登录名映射到 `sysadmin` 固定服务器角色，该角色在整个服务器上具有不可撤销的管理凭据。 如果攻击者以系统管理员的身份获得访问权限，则可能会损坏。 默认情况下，Windows `BUILTIN\Administrators` 组（本地管理员组）的所有成员均为 `sysadmin` 角色的成员，但可以从该角色中移除这些成员。  
  
> [!IMPORTANT]
> 连接来自用户输入的连接字符串可能会导致连接字符串注入攻击。 使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> 在运行时创建语法有效的连接字符串。 
  
## <a name="external-resources"></a>外部资源  
有关详细信息，请参阅下列资源。  
  
|资源|描述|  
|--------------|-----------------|  
|[主体](../../../relational-databases/security/authentication-access/principals-database-engine.md)|描述 SQL Server 中的登录名和其他安全主体。|  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 中的应用程序安全方案](application-security-scenarios-sql-server.md)
