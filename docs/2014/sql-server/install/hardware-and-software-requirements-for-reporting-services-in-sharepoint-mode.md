---
title: SharePoint 模式下 Reporting Services 的硬件和软件要求 |Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ed91877d-4f74-4266-a932-b824b4810c99
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 56ddfce4fc1812e99870c22eeb0e15be64c5decb
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245626"
---
# <a name="hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode"></a>SharePoint 模式下的 Reporting Services 的硬件和软件要求

  本主题介绍在 SharePoint 模式下运行的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]先决条件、硬件要求和安装注意事项。 因为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式需要 SharePoint 服务器，大多数要求均基于 SharePoint 环境。 对于本机模式的报表服务器，您的硬件应满足运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的最低硬件和软件要求。 有关详细信息，请参阅 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   [必备条件](#bkmk_prereq)  
  
-   [报表服务器数据库要求](#bkmk_report_server_database)  
  
-   [Power View 要求](#bkmk_powerview)  
  
-   [详细信息](#bkmk_more_information)  
  
##  <a name="bkmk_prereq"></a>先决条件  
  
-   对于本地安装，在安装 SharePoint 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 期间登录的帐户需要是本地操作系统 administrators 组的成员。 该安装帐户不需要是 SharePoint 场 administrators 组的成员。  
  
     有关详细信息，请参阅 [SharePoint 2013 中的帐户权限和安全设置](https://technet.microsoft.com/library/cc678863.aspx)。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 SharePoint 模式下运行需要 SharePoint Server。 有关 SharePoint 要求和配置的详细信息，请参阅以下文章：  
  
    -   [硬件和软件要求（SharePoint 2013）](https://go.microsoft.com/fwlink/p/?LinkId=256365) （https://go.microsoft.com/fwlink/p/?LinkId=256365)  
  
    -   [SharePoint Server 2013 的容量管理和大小调整](https://technet.microsoft.com/library/cc261700.aspx)  
  
    -   [针对商业智能的软件要求 (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256367)  
  
    -   [硬件和软件要求 (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262485\(v=office.14\))  
  
    -   [SharePoint Server 2010 的容量管理和大小](https://technet.microsoft.com/library/cc261700.aspx\(v=office.14\))  
  
-   如果要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升级或更新现有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]SharePoint 安装，请参阅 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)的最低硬件和软件要求。  
  
-   验证是否已在 Windows 服务器管理器中启动 **“SharePoint 2013 管理”** 服务。  
  
###  <a name="bkmk_report_server_database"></a>报表服务器数据库要求  
  
-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 SharePoint 产品及技术均使用 SQL Server 关系数据库来存储应用程序数据。  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]需要兼容 SQL Server 版本的[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例。 有关硬件和软件要求的详细信息，请参阅 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   SharePoint 产品可以使用现有的数据库实例。 如果未安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，则 SharePoint 产品安装程序将安装 SQL Server Express Edition 以用于 SharePoint 应用程序数据库。  
  
-   报表服务器实例不能将 SQL Server Express Edition 用于其数据库。 但是，由 SharePoint 产品安装的 SQL Server Express Edition 实例可与其他数据库引擎版本并存。  
  
##  <a name="bkmk_powerview"></a>[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]要求

 查看 Office.Microsoft.com 上的最新 [Power View 文档](https://office.microsoft.com/excel-help/power-view-explore-visualize-and-present-your-data-HA102835634.aspx) 。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]是 Microsoft Excel 2013 的一项功能，是 Microsoft SharePoint Server 2010 和[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 2013 Enterprise edition Reporting Services 外接程序的一部分。  
  
##  <a name="bkmk_more_information"></a>详细信息

 有关 SharePoint 更改的信息，请参阅[从 sharepoint 2010 到 sharepoint 2013 的更改](https://technet.microsoft.com/library/ff607742\(office.15\).aspx)（https://technet.microsoft.com/library/ff607742(office.15).aspx)。  
  
 [SQL Server 2014 发行说明](https://go.microsoft.com/fwlink/?LinkID=296445)。  
  
