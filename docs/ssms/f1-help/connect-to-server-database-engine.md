---
title: "连接到服务器（数据库引擎）| Microsoft Docs"
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
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d421bcb09ec7ebde28b5d1cce6eca2263cfb1c48
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-database-engine"></a>连接到服务器（数据库引擎）
连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 时，可使用此对话框查看或指定选项。 大多数情况下，可以通过在“服务器名称”框中输入数据库服务器的计算机名称并单击“连接”来进行连接。 如果要连接到 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，请使用后面跟有 **\sqlexpress** 的计算机名称。  
  
许多因素都会对您能否连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]产生影响。  
  
## <a name="options"></a>选项  
**服务器类型**  
从对象资源管理器注册服务器时，请选择要连接到的服务器的类型： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择“ [!INCLUDE[ssDE](../../includes/ssde_md.md)]”、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]、 [!INCLUDE[ssEW](../../includes/ssew_md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] 。  
  
**服务器名称**  
选择要连接到的服务器实例。 默认情况下，显示上次连接到的服务器实例。  
  
> [!NOTE]  
> 若要连接到 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 的活动用户实例，请使用指定管道名称的 Named Pipes 协议进行连接，例如：np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query。有关详细信息，请参阅 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文档。  
  
**身份验证**  
连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例时，有三种可用的身份验证模式。  
  
**Windows 身份验证**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。  
  
**SQL Server 身份验证**  
当用户使用指定的登录名和密码从不可信连接进行连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将通过检查是否已设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登录帐户以及指定的密码是否与以前记录的密码匹配，自行进行身份验证。 如果未设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登录帐户，则身份验证失败，并且用户会收到一条错误消息。  
  
> [!IMPORTANT]  
> 如果可以，请使用 Windows 身份验证或 Active Directory 密码身份验证。  
  
**Active Directory 通用身份验证**  
Active Directory 通用身份验证是交互式的工作流，支持 Azure 多重身份验证 (MFA)。 Azure MFA 可满足用户简单登录过程的需求，同时可帮助保护数据访问权限和应用程序。 通过一系列的简单验证（电话、短信、带有 PIN 的智能卡或移动应用通知）提供强身份验证，用户可选择喜欢的验证方式。 用户帐户配置 MFA 后，该交互式身份验证工作流需要通过弹出式对话框、智能卡等进行额外用户交互。用户帐户配置 MFA 后，用户必须选择 Azure 通用身份验证进行连接。 如果用户帐户不需要 MFA，用户仍可使用其他两个 Azure Active Directory 身份验证选项。 有关详细信息，请参阅 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)（SSMS 支持使用 SQL 数据库和 SQL 数据仓库的 Azure AD MFA）。 要求至少为 SSMS 版本 16.3（2016 年 8 月）

**Active Directory 密码身份验证**  
Azure Active Directory 身份验证是一种使用 Azure Active Directory (Azure AD) 中的标识连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 的机制。  如果是使用未与 Azure 联合的域中的凭证登录的 Windows 或在使用 Azure AD 身份验证时，使用了基于初始域或客户端域的 Azure AD，请使用此方法连接到 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**Active Directory 集成身份验证**  
Azure Active Directory 身份验证是一种使用 Azure Active Directory (Azure AD) 中的标识连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 的机制。 如果是使用已联合域中的 Azure Active Directory 凭证登录的 Windows，请使用此方法连接到 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**用户名**  
连接所使用的 Windows 用户名。 只有选择使用 **Active Directory 密码身份验证**进行连接时，此选项才可用。 选择 **Windows 身份验证**时，此选项为只读。  
  
**登录**  
输入连接所用的登录名。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证或 Active Directory 密码身份验证进行连接时，此选项才可用。  
  
**密码**  
输入登录名的密码。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证或 Active Directory 密码身份验证进行连接时，才可编辑此选项。  
  
**Connect**  
单击此项可连接到在上面选择的服务器。  
  
**选项**  
单击此项可显示其他服务器连接选项，如注册服务器和记住密码。  
  

