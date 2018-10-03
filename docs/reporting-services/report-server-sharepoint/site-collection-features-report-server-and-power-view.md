---
title: 在 SharePoint 中激活报表服务器和 Power View 集成功能 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ae416f429c2a2d709290a49f477674e86be3f907
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696766"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>在 SharePoint 中激活报表服务器和 Power View 集成功能

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  默认情况下，在安装用于 SharePoint 产品的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 加载项后，将激活 Reporting Services 网站集功能。 在某些情况下，你需要手动激活这些功能。  

> [!NOTE]
> 自 SQL Server 2016 之后，不再提供 Reporting Services 与 SharePoint 的集成这一功能。

 如果在安装 SharePoint 产品后安装了用于 SharePoint 2010 产品的 Reporting Services 加载项，则仅对根网站集激活报表服务器集成功能和 Power View 集成功能。 对于其他网站集，你需要手动激活这些功能。 例如，如果具有 http://[我的服务器名称]/sites/[网站集名称] 的网站集，将需要手动激活 Reporting Services 网站集功能。  
  
 没有根网站集时，Reporting Services 加载项将记录一条类似于以下内容的消息。  
  
 “SharePoint Web 应用程序 80 没有根网站集”  
  
 该消息可以在名为“RS_SP_#.log”的加载项安装日志中找到，其中 # 为递增数字。 该日志文件位于当前用户的 Temp 文件夹中，例如 C:\Users\\[用户名]\AppData\Local\Temp。有关该外接程序日志记录选项的详细信息，请参阅 [安装或卸载用于 SharePoint 的 Reporting Services 外接程序](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>激活报表服务器和 Power View 集成网站集功能
  
1.  打开浏览器，转到要激活 Reporting Services 功能的网站。  
  
2.  单击 **“网站操作”**。  
  
3.  单击 **“网站设置”**。  
  
4.  在网站集管理组中单击 **“网站集功能”** 。  
  
5.  在列表中找到 **“报表服务器集成功能”** 或 **“Power View 集成功能”** 。  
  
6.  单击 **“激活”**。  
  
 若要停用这些功能，您可以使用相同的过程，但单击 **“停用”** 而非 **“激活”**。  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>激活或停用 Reporting Services 管理中心网站集功能
  
1.  打开浏览器找到 SharePoint 管理中心。  
  
2.  单击 **“网站操作”**。  
  
3.  单击 **“网站设置”**。  
  
4.  在网站集管理组中单击 **“网站集功能”** 。  
  
5.  在列表中找到 **“报表服务器管理中心功能”** 。  
  
6.  单击 **“激活”**。  
  
 若要停用这些功能，您可以使用相同的过程，但单击 **“停用”** 而非 **“激活”**。  
  
## <a name="next-steps"></a>后续步骤

激活此功能后，可以继续进行服务器集成。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
