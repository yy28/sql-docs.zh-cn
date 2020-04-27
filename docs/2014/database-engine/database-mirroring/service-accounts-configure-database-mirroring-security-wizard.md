---
title: 服务帐户（配置数据库镜像安全向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69877c6a20e37e012925185d0b807e9579066e35
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754388"
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>服务帐户（配置数据库镜像安全向导）
  使用 Windows 身份验证时，如果服务器实例使用若干个不同的帐户，请为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定服务帐户。 这些服务帐户必须都是域帐户（在相同域或可信域中）。  
  
 如果所有服务器实例都使用同一域帐户或使用基于证书的身份验证，则请将这些字段留空。 只需单击 **“完成”**，向导将根据当前向导的帐户自动配置帐户。  
  
> [!IMPORTANT]  
>  如果将服务器实例的数据库镜像端点配置为使用证书，您必须将服务帐户字段保留为空。  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>选项  
 **主体**  
 指定主体服务器实例的服务帐户。 以大写形式输入域名：  
  
 *DOMAINNAME*\\*用户名*  
  
 **镜像**  
 指定镜像服务器实例的服务帐户。 以大写形式输入域名：  
  
 *DOMAINNAME*\\*用户名*  
  
 **见证**  
 指定见证服务器实例的服务帐户。 以大写形式输入域名：  
  
 *DOMAINNAME*\\*用户名*  
  
## <a name="see-also"></a>另请参阅  
 [&#41;的数据库属性 &#40;镜像页](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [开始数据库镜像监视器 &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [数据库镜像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [设置用于数据库镜像或 AlwaysOn 可用性组 &#40;SQL Server 的登录帐户&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
