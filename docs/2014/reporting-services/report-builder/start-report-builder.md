---
title: 启动报表生成器 （报表生成器） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 70ec1c794e86782551099b4fb5d8459c8bae6191
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157455"
---
# <a name="start-report-builder-report-builder"></a>启动报表生成器（报表生成器）
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 包含独立和[!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)]版本的报表生成器。 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版本可用于本机模式或 SharePoint 集成模式下安装的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
> [!NOTE]  
>  报表生成器不能安装在基于 Itanium 64 的计算机中。 这适用于报表生成器的 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版本和独立版本。  
  
 如果[!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)]将打开报表生成器版本是早期版本的报表生成器，请联系您的管理员可以更新报表管理器和 SharePoint 站点以使用[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本的报表生成器  
  
 还可以使用报表生成器的 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 版本来在已发布到 SharePoint 的 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 工作簿上创建报表。 有关使用报表生成器的详细信息[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]，请参阅[使用 PowerPivot 数据创建 Reporting Services 报表](https://go.microsoft.com/fwlink/?LinkId=185238)technet.microsoft.com 上。  
  
 若要启动报表生成器从独立**启动**菜单上在本地计算机，您或管理员必须直接在您的计算机上安装报表生成器，然后该工具可供你使用。 在安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时未安装独立版本；您必须单独下载并安装它。 若要下载报表生成器，请参阅[Microsoft® SQL Server® 2012年报表生成器](https://go.microsoft.com/fwlink/?LinkId=401502)。  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>从报表管理器启动 Report Builder ClickOnce  
  
1.  在 Web 浏览器的地址栏中，键入报表服务器的 URL。 默认情况下，该 URL 为 http://\<*servername*>/reports。 报表管理器随之打开。  
  
2.  单击 **“报表生成器”**。  
  
     报表生成器将打开，您随后可以在报表服务器上创建报表或打开报表。  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>使用 URL 启动报表生成器 ClickOnce  
  
1.  在 Web 浏览器的地址栏中，键入以下 URL：  
  
     http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0.application  
  
2.  按 Enter。  
  
     报表生成器将打开，您随后可以在报表服务器上创建报表或打开报表。  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>在 SharePoint 集成模式下启动 Report Builder ClickOnce  
  
1.  导航到包含所需库的 SharePoint 站点。  
  
2.  打开库。  
  
3.  单击 **“文档”**。  
  
4.  在 **“新建文档”** 菜单上，单击 **“报表生成器报表”**。  
  
     报表生成器将打开，您随后可以在报表服务器上创建报表或打开报表。  
  
     **请注意**如果**新的文档**菜单未列出**报表生成器报表**，**报表生成器模型**，和**报表数据源**选项，其内容类型需要将添加到 SharePoint 库。 有关详细信息，请参阅[将报表服务器内容类型添加到库&#40;在 SharePoint 集成模式下的 Reporting Services&#41; ](../add-reporting-services-content-types-to-a-sharepoint-library.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][联机丛书](https://go.microsoft.com/fwlink/?LinkId=154888)上msdn.microsoft.com。  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>从“开始”菜单启动报表生成器独立版本  
  
1.  在开始菜单上单击**所有程序**，然后单击[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]**报表生成器**。  
  
2.  单击“报表生成器”  。  
  
     报表生成器将打开，您可以创建或打开报表了。  
  
3.  若要创建新报表，请单击报表生成器左上角的 SQL Server 图标，然后单击“新建”。  
  
4.  若要打开存储在本地计算机或报表服务器上的已有报表，请单击左上角的 SQL Server 图标，然后单击“打开”。  
  
     如果看不到现有服务器列表中的报表服务器，关闭**打开报表**对话框，然后单击**Connect**底部的报表生成器来连接到服务器。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 中的报表生成器](report-builder-in-sql-server-2016.md)  
  
  
