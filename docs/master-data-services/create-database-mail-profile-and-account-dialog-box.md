---
title: “创建数据库邮件配置文件和帐户”对话框
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.dbmailprofileacct.f1
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b1bc67db4ebfe6d72b466562e7075fb93489ba29
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812413"
---
# <a name="create-database-mail-profile-and-account-dialog-box"></a>“创建数据库邮件配置文件和帐户”对话框

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  使用 **“创建数据库邮件配置文件和帐户”** 对话框可为 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库创建数据库邮件配置文件和数据库邮件帐户。 此配置文件将用于在业务规则验证失败时通过电子邮件通知用户和组。  
  
## <a name="database-mail-profile-and-account"></a>数据库邮件配置文件和帐户  
 *数据库邮件配置文件*是数据库邮件帐户的集合。 *数据库邮件帐户*包含用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将电子邮件发送到 SMTP 服务器的信息。 当您在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中创建配置文件和帐户时，帐户将自动添加到配置文件，并且帐户信息将用于发送电子邮件。  
  
> [!NOTE]  
>  您不能使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 更新现有的数据库邮件配置文件或帐户，也不能为某一配置文件配置多个帐户。 若要使用数据库邮件执行更高级的任务，可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 脚本。 有关详细信息，请参阅 SQL Server 联机丛书中的 [Database Mail Configuration Objects](../relational-databases/database-mail/database-mail-configuration-objects.md) 部分。  
  
|控件名称|描述|  
|------------------|-----------------|  
|**配置文件名称**|为新的数据库邮件配置文件键入名称。 在为 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库配置的数据库邮件配置文件中，此名称必须唯一。<br /><br /> 在创建此配置文件后，该配置文件在 **的** “数据库” [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]页上便可供使用和选择。|  
|**帐户名称**|为要与此配置文件相关联的新数据库邮件帐户键入名称。 在为 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库配置的数据库邮件帐户中，此名称必须唯一。 此帐户与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帐户或 Windows 用户帐户均不对应。|  
  
## <a name="outgoing-smtp-mail-server"></a>邮件发送服务器 (SMTP)  
  
|控件名称|描述|  
|------------------|-----------------|  
|**电子邮件地址**|键入帐户电子邮件地址的名称。 这是从其发送电子邮件的电子邮件地址，必须采用*email_name* @ *domain_name*格式。 电子邮件地址示例为 sales@contoso.com。|  
|**显示名称**|可选设置。 键入由此帐户发送的电子邮件上显示的名称。 显示名称的一个例子是 Contoso Sales Group。|  
|**答复电子邮件地址**|可选设置。 键入用于答复由此帐户发送的电子邮件的电子邮件地址。 一个示例答复电子邮件地址为 admin@contoso.com。|  
|**SMTP 服务器**|键入此帐户发送电子邮件所用的 SMTP 服务器的名称或 IP 地址。 SMTP 服务器格式示例：**smtp.***<company_name>***.com**。 如需相关帮助，请询问您的邮件管理员。|  
|**端口号**|键入此帐户的 SMTP 服务器的端口号。 默认 SMTP 端口为 25。|  
|**此服务器要求安全连接(SSL)**|使用传输层安全性（TLS）（以前称为安全套接字层（SSL））对通信进行加密。|  
  
## <a name="smtp-authentication"></a>SMTP 身份验证  
 可以利用 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]的凭据或您提供的其他凭据发送数据库邮件，也可以用匿名方式发送。 最佳做法是，如果您的电子邮件服务器要求身份验证，则创建要用于数据库邮件的特定用户帐户。 此用户帐户应具有最低权限，且不应用于其他任何用途。  
  
|控件名称|描述|  
|------------------|-----------------|  
|**使用数据库引擎服务凭据的 Windows 身份验证**|指定数据库邮件应该使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] Windows 服务帐户的凭据在 SMTP 服务器上进行身份验证。|  
|**基本身份验证**|指定数据库邮件应使用特定的用户名和密码在 SMTP 服务器上进行身份验证。 此信息仅用于针对电子邮件服务器的身份验证，并且帐户不需要与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用户或者运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的计算机上的用户相对应。|  
|**用户名**|键入数据库邮件登录到 SMTP 服务器所用的用户帐户的名称。 如果 SMTP 服务器要求基本身份验证，则需要提供用户名。|  
|**密码**|键入数据库邮件登录到 SMTP 服务器所用的密码。 如果 SMTP 服务器要求基本身份验证，则需要提供密码。|  
|**确认密码**|再次输入密码以进行确认。|  
|**匿名身份验证**|指定 SMTP 服务器不要求身份验证。 数据库邮件将不使用任何凭据在 SMTP 服务器上进行身份验证。|  
  
## <a name="see-also"></a>另请参阅  
 ["数据库配置" 页 &#40;Master Data Services 配置管理器&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services 的安装和配置](../master-data-services/master-data-services-installation-and-configuration.md)
  
  
