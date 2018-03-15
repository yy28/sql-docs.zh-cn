---
title: "SQL Server Data Tools (SSDT) 中的 Azure Active Directory 支持 | Microsoft Docs"
ms.custom: 
ms.date: 03/05/2018
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssdt
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 14a6ae78a0ed5969ce3ab65dbd09b81680076fdb
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 中的 Azure Active Directory 支持

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md.md](../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

SQL Server Data Tools (SSDT) 提供了多种 [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) 身份验证方法。

![SSDT 连接对话框](media/azure-active-directory/interactive.png)

## <a name="active-directory-password-authentication"></a>Active Directory 密码身份验证

Active Directory 密码身份验证是一种使用 Azure Active Directory (Azure AD) 标识连接到 Azure SQL 数据库的机制。  如果是使用凭据从没有与 Azure 联盟的域登录 Windows，或使用基于初始域或客户端域的 Azure AD 进行 Azure AD 身份验证，请使用这种方法进行连接。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。  

## <a name="active-directory-integrated-authentication"></a>Active Directory 集成身份验证

Active Directory 集成身份验证是一种使用 Azure Active Directory (Azure AD) 标识连接到 Azure SQL 数据库的机制。 如果使用 Azure Active Directory 凭据从联盟域登录 Windows，请使用这种方法进行连接。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。

## <a name="active-directory-interactive-authentication-preview"></a>Active Directory 交互式身份验证（预览）

SSDT 提供一种新身份验证方法来连接到 Azure SQL 数据库，即 Active Directory 交互式身份验证。


> [!NOTE]
> 在 [Visual Studio 2017 预览版](https://www.visualstudio.com/vs/preview/)中使用 SSDT 进行连接时，可以使用 Active Directory 交互式身份验证，而且必须在运行 SSDT 的计算机上安装 [.NET 4.7.2 预览版 (KB4038188)](https://go.microsoft.com/fwlink/?linkid=867317)。 如果未安装 .NET 4.7.2 预览版 (KB4038188)，便无法使用 Active Directory 交互式身份验证选项。


Active Directory 交互式身份验证支持交互式身份验证，以便能够使用 Azure Active Directory (AD) 多重身份验证 (MFA) 向 Azure SQL 数据库进行身份验证。 此方法支持本机和联盟 Azure AD 用户，以及来自其他帐户的来宾用户（包括 B2B 用户、Microsft 帐户和非 Microsft 帐户，如 @outlook.com、@hotmail.com、@live.com 和 @gmail.com）。 如果指定此方法，必须指定“用户名”，“密码”字段将遭禁用。 

使用 Active Directory 交互式身份验证进行验证时，将看到打开的身份验证窗口，其中提示用户手动输入密码。

![登录对话框](media/azure-active-directory/sign-in.png)

在身份验证过程中，Azure AD 通过此附加 MFA 弹出窗口强制执行 MFA。

> [!NOTE]
> 由于 Active Directory 交互式身份验证要求用户手动（交互式）输入密码，因此不建议用于自动化工作流。


## <a name="known-issues-and-limitations"></a>已知问题和限制

- 只有当连接到 Azure SQL 数据库时，才支持使用 Active Directory 交互式身份验证。 SQL Server（本地或 VM 上）或 Azure SQL 数据仓库不支持它。
- 服务器资源管理器中的连接对话框不支持 Active Directory 交互式身份验证。必须结合使用 SSDT 和 SQL Server 对象资源管理器进行连接。
- SSDT 不支持将单一登录与当前登录 Visual Studio 的帐户集成。
- 在 Visual Studio 安装期间安装到扩展目录的 SQLPackage.exe 并不是从此位置进行使用。 若要同时使用 SQLpackage.exe 和 AAD，请转到 https://www.microsoft.com/en-us/download/details.aspx?id=55088 
- AAD 身份验证（包括新身份验证方法）不支持 SSDT 数据比较。  





## <a name="see-also"></a>另请参阅  
[多重身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[向 SQL 数据库进行Azure Active Directory 身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[Visual Studio 中的 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 论坛](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 团队博客](http://blogs.msdn.com/b/ssdt/)  
[DACFx API 参考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下载 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
