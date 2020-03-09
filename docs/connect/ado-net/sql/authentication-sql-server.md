---
title: SQL Server 中的身份验证
description: 介绍了 SQL Server 登录和身份验证，并收录了其他资源的链接。
ms.date: 09/26/2019
dev_langs:
- csharp
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 13676265a7e468065506c31bc2362baf25612512
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897051"
---
# <a name="authentication-in-sql-server"></a>SQL Server 中的身份验证

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 支持两种身份验证模式，即 Windows 身份验证模式和混合模式。  
  
- Windows 身份验证是默认模式（通常称为集成安全），因为此 SQL Server 安全模型与 Windows 紧密集成。 特定的 Windows 用户和组帐户可信任，可以登录 SQL Server。 已经过身份验证的 Windows 用户无需提供其他凭据。  
  
- 混合模式支持由 Windows 和 SQL Server 进行身份验证。 用户名和密码保留在 SQL Server 内。  
  
> [!IMPORTANT]
> 建议尽可能使用 Windows 身份验证。 Windows 身份验证使用一系列加密消息来验证 SQL Server 中的用户。 使用 SQL Server 登录时，会通过网络传递 SQL Server 登录名和加密的密码，这样会降低它们的安全性。  
  
使用 Windows 身份验证时，用户已登录到 Windows，无需另外登录到 SQL Server。 下面的 `SqlConnection.ConnectionString` 可指定 Windows 身份验证，而无需用户提供用户名或密码。  
  
```csharp
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
> 登录名不同于数据库用户。 必须在单独的操作中将登录名或 Windows 组映射到数据库用户或角色。 然后，向用户或角色授予对数据库对象的访问权限。  
  
## <a name="authentication-scenarios"></a>身份验证方案  
在以下情况下，Windows 身份验证通常是最佳选择：  
  
- 有域控制器。  
  
- 应用程序和数据库位于同一台计算机上。  
  
- 你正在使用 SQL Server Express 或 LocalDB 的实例。  
  
SQL Server 登录通常用于以下情况：  
  
- 有工作组。  
  
- 用户从不受信任的其他域连接。  
  
- Internet 应用程序（如 ASP.NET）。  
  
> [!NOTE]
> 指定 Windows 身份验证不会禁用 SQL Server 登录。 使用 ALTER LOGIN DISABLE Transact-SQL 语句会禁用具有高级权限的 SQL Server 登录。  
  
## <a name="login-types"></a>登录类型  
SQL Server 支持三种登录类型：  
  
- 本地 Windows 用户帐户或受信任的域帐户。 SQL Server 依靠 Windows 来对 Windows 用户帐户进行身份验证。  
  
- Windows 组。 向 Windows 组授予访问权限会向作为组成员的所有 Windows 用户登录名授予访问权限。  
  
- SQL Server 登录。 SQL Server 将用户名和密码的哈希都存储在 master 数据库中，使用内部身份验证方法来验证登录尝试。  
  
> [!NOTE]
> SQL Server 提供了从证书或非对称密钥创建的登录名，仅用于代码签名。 不能用于连接到 SQL Server。  
  
## <a name="mixed-mode-authentication"></a>混合模式身份验证  
如果必须使用混合模式身份验证，则必须创建 SQL Server 登录名，这些登录名存储在 SQL Server 中。 然后，必须在运行时提供 SQL Server 用户名和密码。  
  
> [!IMPORTANT]
> SQL Server 安装有名为 `sa`（“系统管理员”的首字母缩写）的 SQL Server 登录名。 请向 `sa` 登录名分配强密码，并且不在应用程序中使用 `sa` 登录名。 `sa` 登录名映射到 `sysadmin` 固定服务器角色，此角色在整个服务器上具有不可撤销的管理凭据。 如果攻击者以系统管理员身份获得访问权限，潜在损害是无限的。 默认情况下，Windows `BUILTIN\Administrators` 组（本地管理员组）的所有成员均为 `sysadmin` 角色的成员，但可以从该角色中移除这些成员。  
  
> [!IMPORTANT]
> 连接用户输入中的连接字符串可能会让你易受到连接字符串注入攻击。 请使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> 在运行时创建语法有效的连接字符串。 
  
## <a name="external-resources"></a>外部资源  
有关详细信息，请参阅以下资源。  
  
|资源|说明|  
|--------------|-----------------|  
|[主体](../../../relational-databases/security/authentication-access/principals-database-engine.md)|描述 SQL Server 中的登录名和其他安全主体。|  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 中的应用程序安全方案](application-security-scenarios-sql-server.md)
