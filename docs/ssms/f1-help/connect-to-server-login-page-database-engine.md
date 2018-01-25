---
title: "连接到服务器（“登录”页）数据库引擎 | Microsoft Docs"
ms.custom: 
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-f1
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: "6"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f3824ace141704fb08b29ddbf08890d5299f494
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="connect-to-server-login-page-database-engine"></a>连接到服务器（“登录”页）数据库引擎
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 时，使用此选项卡可查看或指定选项。 大多数情况下，可以通过在“服务器名称”框中输入数据库服务器的计算机名称并单击“连接”来进行连接。 如果连接到命名实例，请使用计算机名称后跟反斜杠，然后是实例名。 例如， `mycomputer\myinstance`。 如果要连接到 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，请使用后面跟有 **\sqlexpress**的计算机名称。  
  
许多因素都会对您能否连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]产生影响。 有关详细信息，请参阅以下资源：  
- [教程第 1 课：连接到数据库引擎](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [排查连接到 SQL Server 数据库引擎时的问题](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [解决 SQL Server 连接错误](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)    
  
> [!NOTE]  
> 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接，必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证和 Windows 身份验证模式下配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 。 有关如何确定身份验证模式和更改身份验证模式的详细信息，请参阅 [如何更改服务器身份验证模式](http://msdn.microsoft.com/en-us/79babcf8-19fd-4495-b8eb-453dc575cac0)。  
  
## <a name="options"></a>“常规”  
**服务器类型**  
从对象资源管理器进行服务器注册时，请选择要连接到何种类型的服务器： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择[!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。  
  
在通过 [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证，并且必须在“连接到服务器”对话框的“连接属性”选项卡上指定一个数据库。请确保选中“加密连接”复选框。  
  
默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将连接到 **master**。 如果指定用户数据库，则对象资源管理器中仅显示该数据库及其对象。 如果连接到 master，则会显示所有数据库。 有关详细信息，请参阅 [Windows Azure SQL 数据库概述](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
**服务器名称**  
选择要连接到的服务器实例。 默认情况下，显示上次连接到的服务器实例。  
  
**身份验证**  
当前版本的 SSMS 中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的实例时提供五种身份验证模式。 如果你的“身份验证”对话框中与以下列表中的不匹配，请从 [下载 SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) 下载最新版本的 SSMS。     
  
在通过 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证，并且必须在“连接到服务器”对话框的“连接属性”选项卡上指定一个数据库。请确保选中“加密连接”复选框。  
  
默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将连接到 **master**。 如果在连接到 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 时指定用户数据库，则对象资源管理器中仅显示该数据库及其对象。 如果连接到 master，则会显示所有数据库。 有关详细信息，请参阅 [Windows Azure SQL 数据库概述](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
  > **Windows 身份验证**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。  
  
  > **SQL Server 身份验证**  
当用户使用指定的登录名和密码从不可信连接进行连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将通过检查是否已设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登录帐户以及指定的密码是否与以前记录的密码匹配，自行进行身份验证。 如果未设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登录帐户，则身份验证失败，并且用户会收到一条错误消息。 请尽可能使用 Windows 身份验证。  
  
  > **Active Directory - 含 MFA 支持的通用身份验证**  
Active Directory - 含 MFA 支持的通用身份验证是交互式的工作流，支持 Azure 多重身份验证 (MFA)。 Azure MFA 可满足用户简单登录过程的需求，同时可帮助保护数据访问权限和应用程序。 通过一系列的简单验证（电话、短信、带有 PIN 的智能卡或移动应用通知）提供强身份验证，用户可选择喜欢的验证方式。 用户帐户配置 MFA 后，该交互式身份验证工作流需要通过弹出式对话框、智能卡等进行额外用户交互。用户帐户配置 MFA 后，用户必须选择 Azure 通用身份验证进行连接。 如果用户帐户不需要 MFA，用户仍可使用其他两个 Azure Active Directory 身份验证选项。 有关详细信息，请参阅 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)（SSMS 支持使用 SQL 数据库和 SQL 数据仓库的 Azure AD MFA）。 如有必要，可通过单击“选项”，选择“连接属性”选项卡，并完成“AD 域名或租户 ID”框，更改对登录名进行身份验证的域。  

  > **Active Directory - 密码**  
Azure Active Directory 身份验证是一种使用 Azure Active Directory (Azure AD) 中的标识连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 的机制。  如果是使用凭证从未与 Azure 联合的域登录到 Windows，或使用基于初始域或客户端域的 Azure AD 进行 Azure AD 身份验证，请使用此方法连接到 [!INCLUDE[ssSDS](../../includes/sssds_md.md)]。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
  > **Active Directory - 集成**  
Azure Active Directory 身份验证是一种使用 Azure Active Directory (Azure AD) 中的标识连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 的机制。 如果使用 Azure Active Directory 凭证从联合域登录到 Windows，请使用此方法连接到 [!INCLUDE[ssSDS](../../includes/sssds_md.md)]。 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**User name**  
连接所使用的 Windows 用户名。 只有选择使用 **Active Directory 密码身份验证**进行连接时，此选项才可用。 选择“Windows 身份验证”或“Active Directory - 集成身份验证”时，它是只读的。  
  
**登录**  
输入连接所用的登录名。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证或 Active Directory 密码身份验证进行连接时，此选项才可用。  
  
**密码**  
输入登录名的密码。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证或 Active Directory - 密码身份验证进行连接时，才可编辑此选项。  
  
**记住密码**  
单击此项可使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 存储您所输入的密码。 只有在已选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证进行连接时，才会显示此选项。  
  
**“连接”**  
单击以连接到服务器。  
  
**选项**  
单击以显示“连接属性”和“其他连接参数”选项卡。  
   
  
