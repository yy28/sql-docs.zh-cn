---
title: "连接到服务器（“登录”页）数据库引擎 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1556c7facc4a671767fe2d6c061b4f6655ba521b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="connect-to-server-login-page-database-engine"></a>连接到服务器（“登录”页）数据库引擎
连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 时，使用此选项卡可查看或指定选项。  
  
> [!NOTE]  
> 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接，必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证和 Windows 身份验证模式下配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 。 有关如何确定身份验证模式和更改身份验证模式的详细信息，请参阅 [如何更改服务器身份验证模式](http://msdn.microsoft.com/en-us/79babcf8-19fd-4495-b8eb-453dc575cac0)。  
  
## <a name="options"></a>选项  
**服务器类型**  
从对象资源管理器进行服务器注册时，请选择要连接到何种类型的服务器： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择[!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。  
  
在通过 [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证，并且必须在“连接到服务器”对话框的“连接属性”选项卡上指定一个数据库。 请确保选中“加密连接”复选框。  
  
默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将连接到 **master**。 如果您指定一个用户数据库，在对象资源管理器中将只会看到该数据库及其对象。 如果连接到 **master**，可以看到所有数据库。 有关详细信息，请参阅 [Windows Azure SQL 数据库概述](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
**服务器名称**  
选择要连接到的服务器实例。 默认情况下，显示上次连接到的服务器实例。  
  
**身份验证**  
在连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]实例时，可以使用两种身份验证模式。  
  
在通过 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证，并且必须在“连接到服务器”对话框的“连接属性”选项卡上指定一个数据库。 请确保选中“加密连接”复选框。  
  
默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将连接到 **master**。 如果您指定一个用户数据库，在对象资源管理器中将只会看到该数据库及其对象。 如果连接到 **master**，可以看到所有数据库。 有关详细信息，请参阅 [Windows Azure SQL 数据库概述](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
**Windows 身份验证**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。  
  
**SQL Server 身份验证**  
当用户使用指定的登录名和密码从不可信连接进行连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将通过检查是否已设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登录帐户以及指定的密码是否与以前记录的密码匹配，自行进行身份验证。 如果未设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登录帐户，则身份验证失败，并且用户会收到一条错误消息。  
  
> [!IMPORTANT]  
> 请尽可能使用 Windows 身份验证。  
  
**Active Directory 通用身份验证**  
Active Directory 通用身份验证是交互式的工作流，支持 Azure 多重身份验证 (MFA)。 Azure MFA 可满足用户简单登录过程的需求，同时可帮助保护数据访问权限和应用程序。 通过一系列的简单验证（电话、短信、带有 PIN 的智能卡或移动应用通知）提供强身份验证，用户可选择喜欢的验证方式。 用户帐户配置 MFA 后，该交互式身份验证工作流需要通过弹出式对话框、智能卡等进行额外用户交互。用户帐户配置 MFA 后，用户必须选择 Azure 通用身份验证进行连接。 如果用户帐户不需要 MFA，用户仍可使用其他两个 Azure Active Directory 身份验证选项。 有关详细信息，请参阅 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)（SSMS 支持使用 SQL 数据库和 SQL 数据仓库的 Azure AD MFA）。 要求至少为 SSMS 版本 16.3（2016 年 8 月）
  
**Active Directory 密码身份验证**  
Azure Active Directory 身份验证是一种使用 Azure Active Directory (Azure AD) 中的标识连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 的机制。  如果是使用未与 Azure 联合的域中的凭证登录的 Windows 或在使用 Azure AD 身份验证时，使用了基于初始域或客户端域的 Azure AD，请使用此方法连接到 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**Active Directory 集成身份验证**  
Azure Active Directory 身份验证是一种使用 Azure Active Directory (Azure AD) 中的标识连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 的机制。 如果是使用已联合域中的 Azure Active Directory 凭证登录的 Windows，请使用此方法连接到 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**用户名**  
连接所使用的 Windows 用户名。 只有选择使用 **Active Directory 密码身份验证**进行连接时，此选项才可用。 选择 **Windows 身份验证**时，此选项为只读。  
  
**登录**  
输入连接所用的登录名。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接时，此选项才可用。  
  
**密码**  
输入登录名的密码。 只有在已选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接的情况下，此选项才可用。  
  
**记住密码**  
单击此项可使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 存储您所输入的密码。 只有在已选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接时，才会显示此选项。  
  
**Connect**  
单击此项可连接到在上面选择的服务器。  
  
**选项**  
单击此选项更改对话框并隐藏其他服务器连接选项，例如记住密码。  
  

