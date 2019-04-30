---
title: 安装、 卸载和报表生成器支持 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- administering Report Builder
ms.assetid: 2c9a5814-17bf-4947-8fb3-6269e7caa416
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0272c7598e34d7ba920484b3d2b9c504587212cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261326"
---
# <a name="install-uninstall-and-report-builder-support"></a>安装、卸载和报表生成器支持
  报表生成器是一种可用于创建、更新和共享报表、报表部件和共享数据集的报表创作工具。 报表生成器有两个版本：独立版本和 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]版本。 独立版本由您或管理员安装到您的计算机上。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本随 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 自动安装，是从报表管理器或与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]集成的 SharePoint 站点下载到您的计算机中的。  
  
 报表生成器的独立版本不随 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]一起安装。 您必须从 [Microsoft® SQL Server® 2012 报表生成器](https://go.microsoft.com/fwlink/?LinkId=401502)进行单独下载并安装。  
  
> [!NOTE]  
>  报表生成器不能安装在基于 Itanium 的计算机中。 这适用于报表生成器的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本和独立版本。  
  
 通常，由管理员安装和配置 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、授予使用报表生成器的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本的权限，以及管理文件夹与对报表、报表部件和保存到报表服务器的共享数据集的权限。 有关详细信息[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]管理，请参阅[Reporting Services 报表服务器&#40;本机模式&#41;](report-server/reporting-services-report-server-native-mode.md)中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][联机丛书](https://go.microsoft.com/fwlink/?LinkId=154888)msdn.microsoft.com 上。  
  
##  <a name="Installing"></a> 安装报表生成器  
 报表生成器有独立版本和 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本。 您或管理员将独立版本下载并安装到您的计算机上，而 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本则随 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]一起安装。 可以从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkID=186083)下载报表生成器。  
  
> [!NOTE]  
>  报表生成器不能安装在基于 Itanium 64 的计算机中。 这适用于报表生成器的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本和独立版本。  
  
 在安装报表生成器的任一版本前，请先确认系统要求并安装所有必备组件。  
  
### <a name="system-requirements"></a>系统要求  
 报表生成器需要在本地计算机上安装 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 3.5 版。 如果在安装报表生成器时本地计算机上未安装 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ，系统会提示您安装它，然后才能继续并完成报表生成器的安装。  
  
 .NET Framework 3.5 是免费的。 您可以从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkID=110520)下载 .NET Framework 3.5。  
  
 可以在支持 [!INCLUDE[msCoName](../includes/msconame-md.md)] 3.5 的任何 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Windows 操作系统上安装报表生成器。 例如，可以在 Windows Vista 或 Windows 7 上安装报表生成器。  
  
 建议将要运行报表生成器的计算机具有 512 MB 的 RAM。 但是，根据所运行的报表的复杂性，可能需要更少或更多的 RAM。  
  
### <a name="installing-the-stand-alone-version-of-report-builder-directly-on-your-computer"></a>直接在计算机上安装报表生成器的独立版本  
 您可以从下载站点、 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkID=186083)下载并安装报表生成器，或者管理员将 ReportBuilder3.msi 文件（报表生成器的 Windows Installer 包）放在某个共享位置上，您可以从中进行安装。  
  
 还可以执行命令行安装，并包括进行静默安装和写入安装的日志文件等选项。 Windows Installer（用于运行 .msi 文件）的文档提供了有关可用选项的信息。  
  
 有关详细信息，请参阅[安装报表生成器独立版本&#40;报表生成器&#41;](install-windows/install-report-builder.md)。  
  
 管理员还可以使用 Microsoft Systems Manager Server (SMS) 等软件将程序推送到您的计算机上。 若要了解如何使用特定软件安装报表生成器，请查阅该软件的文档。   
  
### <a name="installing-the-clickonce-version-of-report-builder-on-your-computer"></a>在计算机上安装报表生成器 ClickOnce 版本  
 报表生成器的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本随 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]一起安装。 它通过 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]的本机安装和 SharePoint 集成安装进行安装。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 是 Microsoft 用于部署 Windows 应用程序的一种技术。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使得用户可以通过在网页上单击链接来安装和运行 Windows 应用程序（例如报表生成器）。 有关部署的详细信息[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序、 应用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序安全性或运行[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序在 Internet 区域中，请参阅"ClickOnce 部署的 Windows 窗体应用程序""中的安全性Windows 窗体概述"受信任的应用程序部署概述"文章[!INCLUDE[msCoName](../includes/msconame-md.md)]开发人员网络网站，网址[ https://developer.microsoft.com/ ](https://developer.microsoft.com/)。  
  
 报表生成器的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本位于报表服务器上，并且在您单击报表管理器中的 **“报表生成器”** 按钮或单击 SharePoint 库中的 **“新建文档”** 菜单中的 **“报表生成器报表”** 选项时，将会安装在您的计算机上。  
  
> [!NOTE]  
>  如果 **“新建文档”** 菜单未列出 **“报表生成器报表”**、 **“报表生成器模型”** 和 **“报表数据源”** 选项，则需要将其内容类型添加到 SharePoint 库中。   
  
 可以从报表管理器或 SharePoint 库打开报表生成器。 打开报表生成器的详细信息，请参阅[启动报表生成器&#40;报表生成器&#41;](report-builder/start-report-builder.md)。  
  
### <a name="report-builder-languages"></a>报表生成器语言  
 除了英语版本外，报表生成器另外还有 21 种语言的版本。 下载报表生成器独立版本时，请选择要安装的语言版本。 对于要使用的每种语言版本，必须重复下载。  
  
 对于 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本，在安装 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]时，所有语言版本都会安装在报表服务器上。 用户计算机的区域性决定了要在计算机上安装的语言版本。 如果区域性与可用的报表生成器语言都不同，则会安装英语版本。  
  
 下表是有关可用语言版本的信息。  
  
|LCID|语言|Culture|  
|----------|--------------|-------------|  
|1028|繁体中文|zh-TW|  
|1029|捷克语|cs-CZ|  
|1030|丹麦语|da-DK|  
|1031|德语|de-DE|  
|1032|希腊语|el-GR|  
|2052|英语|zh-CN|  
|1035|芬兰语|fi-FI|  
|1036|法语|fr-FR|  
|1038|匈牙利语|hu-HU|  
|1040|意大利语|it-IT|  
|1041|日语|ja-JP|  
|1042|朝鲜语|ko-KR|  
|1043|荷兰语|nl-NL|  
|1044|挪威语（博克马尔）|nb-NO|  
|1045|波兰语|pl-PLl|  
|1046|葡萄牙语（巴西）|pt-BR|  
|1049|俄语|ru-RU|  
|1053|瑞典语|sv-SE|  
|1055|土耳其语|tr-TR|  
|2052|简体中文|zh-CN|  
|2070|葡萄牙语（葡萄牙）|pt-PT|  
|3082|西班牙语（西班牙）|es-ES|  
  
  
##  <a name="Uninstalling"></a> 卸载报表生成器  
 可以从控制面板或命令行卸载报表生成器的独立版本。 这仅适用于报表生成器的独立版本。 无法单独卸载报表生成器的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本。 它总是与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]一起安装和卸载。  
  
 有关详细信息，请参阅[卸载报表生成器独立版本&#40;报表生成器&#41;](install-windows/uninstall-report-builder.md)。  
  
  
##  <a name="Supporting"></a> 支持报表生成器  
 为了支持报表作者，管理员负责管理报表服务器上的文件夹、报表及报表相关的项，授予对报表服务器上资源的权限，以及配置要访问的报表服务器。  
  
### <a name="folders-reports-and-report-related-items"></a>文件夹、报表和报表相关的项  
 以下文件夹、报表和与报表相关的项均在报表服务器上管理：  
  
-   存储报表、共享数据源、模型等的文件夹。  
  
-   “我的报表”，存储报表和与报表相关的项的专用文件夹。  
  
-   共享数据源，使报表作者能够使用在报表外部存储的数据源。  
  
-   共享数据集，可为多个用户提供多个报表的现成可用的查询数据。  
  
-   报表部件（如表和图表），使用户能够在协作环境中增强和重用由其他用户创建的报表部件。  
  
-   报表模型，可使从复杂数据源为报表获取数据更加简便。  
  
-   图像（如背景图像和徽标），可在多个报表中使用且可存储在报表外部以便于维护。  
  
 有关详细信息，请参阅[报表服务器内容管理&#40;SSRS 本机模式&#41;](report-server/report-server-content-management-ssrs-native-mode.md)中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][联机丛书](https://go.microsoft.com/fwlink/?LinkId=154888)msdn.microsoft.com 上。  
  
### <a name="permissions"></a>权限  
 管理员会授予针对报表服务器的权限。 作为报表生成器用户，您需要先具有报表服务器的权限，然后才能访问报表服务器的内容和功能。 例如，您可能希望使用存储在报表服务器上的报表部件，更新报表然后将它们重新保存到报表服务器，在报表管理器中运行报表。 根据您的需要和所执行的任务，可能会授予更低或更高的权限。 例如，与需要修改共享报表的用户相比，应将具有更低特权的权限授予那些只需打开共享报表的用户。  
  
 在本机模式下安装 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 时，管理员可以：  
  
-   启用“我的报表”功能，从而为您提供专用文件夹，用以创建和保存您自己的报表。  
  
-   在公用文件夹上使用报表生成者角色，可允许您打开共享报表的副本，然后将修改后的版本保存到专用文件夹。  
  
-   使用发布者角色可允许您管理公用文件夹中的报表和共享数据源。 此角色将授予更有经验的用户。  
  
 在 SharePoint 集成模式下安装 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 时，管理员可以：  
  
-   使用“读取”权限级别（默认情况下授予“访问者”组），可允许您打开公用文件夹中的报表副本，然后将报表的修改版本保存到专用文件夹或您的计算机。  
  
-   使用“参与讨论”权限级别（默认情况下授予“成员”组），可允许您管理公用文件夹中的报表和共享数据源。 此权限级别将授予更有经验的用户。  
  
 有关权限以及创建和使用角色的常规信息，请参阅 msdn.microsoft.com 上 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 联机丛书 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [中的](https://go.microsoft.com/fwlink/?LinkId=154888) 。  
  
### <a name="configuration-of-report-server"></a>报表服务器的配置  
 如果您在报表生成器中创作报表并且连接到在 Windows Vista、Windows Server 2008 或 Windows 7 上安装的某一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，则在尝试访问报表服务器以便打开或保存某一报表时，可能会遇到访问拒绝错误。 产生此错误的原因在于，Windows Vista、Windows Server 2008 和 Windows 7 中的安全功能用户帐户控制 (UAC) 会通过在访问应用程序时删除管理员权限，限制过度使用提升权限。  
  
 但是，通过附加配置，报表服务器可供报表生成器用户使用。 您可以将 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] URL 添加到受信任站点。 默认情况下，Internet Explorer 7.0 或更高版本在 Windows Vista、Windows Server 2008 和 Windows 7 上是以保护模式运行的。 保护模式是一种可阻止浏览器请求到达运行在同一计算机上的高级别进程的功能。 通过将报表服务器应用程序添加为受信任站点，可以禁用这些应用程序的保护模式。 您必须拥有管理员权限才能进行此更改。  
  
 有关配置详细信息[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，请参阅[Reporting Services 配置管理器&#40;del&#41; ](/sql/2014/sql-server/install/reporting-services-configuration-manager-native-mode)中[Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312)msdn.microsoft.com 上。  
  
  
##  <a name="SampleDatabases"></a> SQL Server 示例数据库  
 Adventure Works 系列示例数据库提供您可以用来了解报表创作和编写示例报表的数据。  
  
 这些数据库采用以下版本：  
  
-   Adventure Works OLTP 数据库支持虚构自行车制造商 (Adventure Works Cycles) 的标准联机事务处理应用场景。 应用场景包括制造、销售、采购、产品管理、联系人管理和人力资源。  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库演示如何生成数据仓库。  
  
-   [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 项目可用于为商业智能应用场景生成 AS 数据库。  
  
 该示例数据库未包含在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，且在安装报表生成器的 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 版本或独立版本时，也不会随之安装。 您而是应该从 [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843)下载示例数据库。 示例数据库的所有版本将会一起下载。 您也可以下载随 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]和 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]一起发布的早期数据库版本。  
  
 有关下载和安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 示例数据库的必备组件和说明，请参阅 CodePlex 上的 [SQL Server 2008 示例数据库的安装必备组件](https://go.microsoft.com/fwlink/?LinkId=166648) 和 [安装示例数据库](https://go.microsoft.com/fwlink/?LinkId=166649) 。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节列出的过程介绍如何安装和卸载报表生成器。  
  
 [安装报表生成器的独立版本&#40;报表生成器&#41;](install-windows/install-report-builder.md)  
  
 [卸载报表生成器的独立版本&#40;报表生成器&#41;](install-windows/uninstall-report-builder.md)  
  
 [启动报表生成器&#40;报表生成器&#41;](report-builder/start-report-builder.md)  
  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
