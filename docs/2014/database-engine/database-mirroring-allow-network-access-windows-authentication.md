---
title: 对数据库镜像端点进行网络访问
description: 了解如何允许 windows authenticatino 网络访问数据库镜像端点 SQL Server。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e40a1eead54fe9d00eaf099410260023229796d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75228568"
---
# <a name="allow-network-access-to-a-database-mirroring-endpoint-using-windows-authentication-sql-server"></a>允许使用 Windows 身份验证对数据库镜像端点进行网络访问 (SQL Server)
  将 Windows 身份验证用于连接两个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的数据库镜像端点在以下条件下要求手动配置登录帐户：  
  
-   如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例基于不同的域帐户（在相同的域或受信任的域中）作为服务运行，则必须在每个远程服务器实例上的 **master** 中创建各帐户的登录名，并且必须授予该登录帐户对端点的 CONNECT 权限。  
  
-   如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例作为网络服务帐户运行，则必须在每个远程服务器实例上的 master ****中创建各主机帐户 (DomainName\\ComputerName$)****  的登录名，并且必须授予该登录帐户对端点的 CONNECT 权限。 其原因在于，基于网络服务帐户运行的服务器实例使用主机的域帐户进行身份验证。  
  
> [!NOTE]  
>  确保每个服务器实例都有一个端点。 有关详细信息，请参阅 [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)。  
  
### <a name="to-configure-logins-for-windows-authentication"></a>为 Windows 身份验证配置登录名  
  
1.  对于每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的用户帐户，在其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例上创建一个登录名。 将 [CREATE LOGIN](/sql/t-sql/statements/create-login-transact-sql) 语句与 FROM WINDOWS 子句一起使用。  
  
     有关详细信息，请参阅 [创建登录名](../relational-databases/security/authentication-access/create-a-login.md)。  
  
2.  另外，为了确保登录用户对端点具有访问权限，请使用 [GRANT](/sql/t-sql/statements/grant-transact-sql) 语句为登录授予对端点的连接权限。 注意，如果用户是管理员，则无需授予对端点的连接权限。  
  
     有关详细信息，请参阅 [Grant a Permission to a Principal](../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md)。  
  
## <a name="example"></a>示例  
 下面的 [!INCLUDE[tsql](../includes/tsql-md.md)] 示例为属于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 域的 `Otheruser` 用户帐户创建了一个 `Adomain`登录名。 并授予了此用户对预先存在的 `Mirroring_Endpoint`数据库镜像端点的连接权限。  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [数据库镜像 (SQL Server)](database-mirroring/database-mirroring-sql-server.md)   
 [用于数据库镜像和 AlwaysOn 可用性组 &#40;SQL Server 的传输安全&#41;](database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [数据库镜像终结点 (SQL Server)](database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
