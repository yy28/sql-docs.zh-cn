---
title: Reporting Services 配置选项 (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.ins.instwizard.reportserverinstoptions.f1
helpviewer_keywords:
- Report Server Installation Options page [SQL Server Installation Wizard]
- report servers [Reporting Services], installing
- SQL Server Installation Wizard, Report Server Installation Options page
ms.assetid: e4561f6c-bc7f-467e-821a-cde8e5cd7391
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9afc4e179807d6cc10925d4fb4964cea857427d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185337"
---
# <a name="reporting-services-configuration-options-ssrs"></a>Reporting Services 配置选项 (SSRS)
  使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导中的“Reporting Services 配置”页来指定如何安装和配置报表服务器。 安装选项的可用性取决于您以前在 **“功能选择”** 页选择的选项以及在安装报表服务器的同时是否还安装了 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的本地实例。  
  
 在某些情况下，如果安全套接字层 (SSL) 证书安装在计算机上并绑定到一个强通配符，安装程序将使用 HTTPS 前缀创建 Reporting Services URL。 有关如何将证书映射到 Reporting Services Url 的详细信息，请参阅[配置安全套接字层 (SSL) 连接的报表服务器](http://go.microsoft.com/fwlink/?LinkId=199089)(http://go.microsoft.com/fwlink/?LinkId=199089) SQL Server 联机丛书中。  
  
 有关最新信息有关[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和的安装和配置此版本中，请参阅[其他安装信息](http://go.microsoft.com/fwlink/?LinkId=207425)(http://go.microsoft.com/fwlink/?LinkId=207425)。  
  
## <a name="options"></a>选项  
  
### <a name="reporting-services-native-mode"></a>Reporting Services 本机模式  
 如果安装程序由于一条或多条要求未得到满足而无法执行默认的报表服务器配置，那么安装向导只允许选择最小化安装选项；同时，它会复制所需的文件，但要求在安装结束后，使用 Reporting Services 配置管理器来配置本机模式报表服务器。  
  
> [!NOTE]  
>  如果选择默认安装选项之一，则现有的报表服务器数据库文件可能会导致安装失败。 当选择默认安装选项时，安装程序将尝试使用默认名称创建报表服务器数据库。 如果使用该名称的数据库已经存在，安装程序将失败，您必须回滚安装。 若要避免此问题，可在运行安装程序前重命名现有数据库，或选择 **“仅安装”** 选项，以便在安装完成后指定自定义数据库设置。  
  
#### <a name="install-and-configure"></a>安装和配置  
 在本机模式下使用报表服务器数据库、服务帐户和 URL 预留的默认值安装报表服务器实例。 如果选择此选项，那么当安装程序完成后，报表服务器实例即可使用。 安装程序通过使用本地 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例来创建报表服务器数据库，并配置报表服务器，使其使用默认值。  
  
 仅当报表服务器安装中使用的默认值对您的系统有效时，此选项才可用。 建议希望在本地安装所有组件的开发人员和评估软件的用户使用此选项。  
  
 若要查看关于安装程序所用默认设置的信息，或者要找出默认配置无法安装的原因，请单击 **“详细信息”**。 有关本机模式报表服务器的默认配置的详细信息，请参阅[默认配置为本机模式安装 (Reporting Services)](http://go.microsoft.com/fwlink/?LinkId=199091) (http://go.microsoft.com/fwlink/?LinkId=199091)。  
  
#### <a name="install-only"></a>“仅安装”  
 安装报表服务器程序文件，创建报表服务器服务帐户，并注册报表服务器 Windows Management Instrumentation (WMI) 提供程序。 此安装选项称为“仅文件”安装。 如果不希望使用默认配置，则选择此选项。 如果无法安装默认配置，或安装的是包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]故障转移群集，这将是唯一可用的选项。 有关仅文件安装的详细信息，请参阅[文件安装 (Reporting Services)](http://go.microsoft.com/fwlink/?LinkId=199093) (http://go.microsoft.com/fwlink/?LinkId=199093)。  
  
 安装程序完成后，必须先创建报表服务器数据库并配置报表服务器，服务器才可以使用。 若要配置报表服务器并创建数据库，请使用 Reporting Services 配置管理器。 有关详细信息，请参阅[如何： 创建报表服务器数据库 （Reporting Services 配置）](http://go.microsoft.com/fwlink/?LinkId=199094) (http://go.microsoft.com/fwlink/?LinkId=199094)并[配置报表服务器数据库连接](http://go.microsoft.com/fwlink/?LinkId=199095)(http://go.microsoft.com/fwlink/?LinkId=199095)。  
  
### <a name="reporting-services-sharepoint-mode"></a>Reporting Services SharePoint 模式  
  
#### <a name="install-only"></a>“仅安装”  
 安装报表服务器程序文件和 PowerShell cmdlet。 安装完成后您将需要启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服务并创建一个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。 有关详细信息，请参见以下内容：  
  
-   [安装 Reporting Services SharePoint 模式报表服务器用于 Power View 和数据警报](http://go.microsoft.com/fwlink/?LinkId=207543)(http://go.microsoft.com/fwlink/?LinkId=207543)。  
  
-   [安装 Reporting Services SharePoint 模式作为单服务器场](http://go.microsoft.com/fwlink/?LinkId=207544)(http://go.microsoft.com/fwlink/?LinkId=207544)。  
  
-   [Reporting Services 报表服务器 (SSRS)](http://go.microsoft.com/fwlink/?LinkID=207244) (http://go.microsoft.com/fwlink/?LinkID=207244)。  
  
## <a name="installing-the-reporting-services-add-in-for-sharepoint-technologies"></a>安装用于 SharePoint 技术的 Reporting Services 外接程序  
 从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本开始，可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导的功能选择页中将此外接程序作为 SQL Server 安装的一部分进行安装.  
  
 但是，您可以使用以下方法之一安装适用于 SharePoint 2010 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序：  
  
-   运行 SharePoint 2010 产品准备工具 **PreRequisiteInstaller.exe**。  
  
-   从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装介质安装。 在 **安装程序完成后，在** 安装介质上的 Setup 文件夹中单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rsSharePoint.msi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文件。  
  
-   下载并安装此外接程序。 有关详细信息，请参阅[在哪里可以找到 Reporting Services 外接程序用于 SharePoint 产品](http://go.microsoft.com/fwlink/?LinkID=208634)(http://go.microsoft.com/fwlink/?LinkID=208634)。  
  
## <a name="see-also"></a>请参阅  
 [启动 Reporting Services 配置管理器](http://go.microsoft.com/fwlink/?LinkId=199096)   
 [创建报表服务器数据库 (Reporting Services 配置)](http://go.microsoft.com/fwlink/?LinkId=199094)   
 [升级和迁移 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=245628)   
 [使用命令提示符安装 Reporting Services SharePoint 模式和本机模式](http://go.microsoft.com/fwlink/?LinkId=217620)  
  
  
