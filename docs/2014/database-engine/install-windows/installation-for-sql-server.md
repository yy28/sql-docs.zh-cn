---
title: SQL Server 2014 安装 |Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- sql12.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5a7e72b429789477a9ae1245be30b18965560ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775356"
---
# <a name="installation-for-sql-server-2014"></a>SQL Server 2014 安装
 ## <a name="download-sql-server-2014-expresshttpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[下载 SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **感谢您参与到[Scott Hanselman](http://www.hanselman.com/)收集所有安装程序包链接在一个位置 ！**
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导提供一个功能树以用来安装所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   管理工具  
  
-   连接组件  
  
 您可以单独安装每个组件，也可以选择上面列出的组件的组合。 若要作出最佳选择的版本和组件中提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[各版本和 SQL Server 2014 的组件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[SQL Server 2014 各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 有 32 位和 64 位两种版本可用。
 
 **进行试用：**  
  
-   已经拥有 Azure 帐户？  然后转**[此处](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** 启动具有 SQL Server 2014 Service Pack 1 (SP1) 的虚拟机已安装。 SQL Server 2014 (SP1) 的详细信息，请参阅[SQL Server 2014 Service Pack 1 发布信息](https://support.microsoft.com/en-us/kb/3058865)。  
  
## <a name="in-this-section"></a>本节内容  
 无论使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导还是命令提示符安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，安装都包括下列步骤：  
  
 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)  
 说明如何为安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]而准备计算机：  
  
-   硬件和软件要求。  
  
-   系统配置检查器的要求和妨碍性问题。  
  
-   安全注意事项。  
  
 [安装 SQL Server 2014](install-sql-server.md)  
 说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的安装选项。  
  
 [升级到 SQL Server 2014](upgrade-sql-server.md)  
 介绍用于升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的选项。  
  
 [卸载 SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)  
 说明卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的过程。  
  
 [SQL Server 故障转移群集安装](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节介绍了如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集。  
  
 [安装 SQL Server 2014 BI 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft BI 平台的部分功能包括： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，以及用于创建或使用分析数据的若干客户端应用程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装文档中的本节说明如何安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
## <a name="related-sections"></a>相关章节  
 [安装操作指南主题](../../sql-server/install/installation-how-to-topics.md)  
 提供 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的各种安装方法的过程主题链接，这些方法包括使用安装向导、命令提示符、配置文件或 SysPrep。  
  
 [使用 SharePoint 安装 SQL Server BI 功能&#40;PowerPivot 和 Reporting Services&#41;](../../sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
 本节介绍如何在 SharePoint 环境中安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 它标识对于特定版本的 SharePoint，提供了哪些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 本节还包含在 SharePoint 模式下安装 PowerPivot for SharePoint 和 Reporting Services 的过程。  
  
 [安装 SQL Server 示例和示例数据库](http://sqlserversamples.codeplex.com/)  
 说明如何安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 示例和示例数据库。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 安装中的新增功能](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [安装 SQL Server 2014 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
  
