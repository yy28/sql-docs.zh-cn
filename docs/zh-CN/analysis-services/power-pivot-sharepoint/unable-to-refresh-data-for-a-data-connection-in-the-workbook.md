---
title: 无法刷新工作簿中的数据连接的数据 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c1961c883a5e38c56acf65def83272aa1e5adb8d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook"></a>无法刷新工作簿中用于数据连接的数据
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  对于包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的 Excel 工作簿，如果 Excel Services 提交对某一 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器的连接请求并且该请求失败，则会返回此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用范围：|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|请参阅下文。|  
|訊息文字|无法刷新工作簿中用于数据连接的数据。 请重试，或与系统管理员联系。 以下连接无法刷新： [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据|  
  
## <a name="explanation-and-resolution"></a>说明和解决方法  
 Excel Services 无法连接到或加载 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据。 在下列情况下会出现此错误：  
  
 **应用场景 1：服务未启动**  
  
 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 实例未启动。 到期的密码将导致服务停止运行。 有关更改密码的详细信息，请参阅 [配置 Power Pivot 服务帐户](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md) 和 [启动或停止 Power Pivot for SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)。  
  
 **应用程序 2a：在服务器中打开早期版本的工作簿**  
  
 你正尝试打开的工作簿可能是在 SQL Server 2008 R2 版本的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中创建的。 数据连接字符串中指定的 Analysis Services 数据访问接口很可能在要处理请求的计算机上不存在。  
  
 如果出现这种情况，你将在 ULS 日志中找到此消息:"对于刷新失败[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]t 数据工作簿中\<到工作簿的 URL >'"后, 跟"无法建立连接"。  
  
 若要确定工作簿的版本，请在 Excel 中打开它，然后查看连接字符串中指定的数据访问接口。 SQL Server 2008 R2 工作簿将 MSOLAP.4 用作其数据访问接口。  
  
 若要解决此问题，可以升级工作簿。 或者，可以在运行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或 Excel Services 的物理计算机上安装 SQL Server 2008 R2 版本的 Analysis Services 中的客户端库，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
 **应用场景 2b：Excel Services 正在具有错误版本的客户端库的应用程序服务器上运行**  
  
 默认情况下，SharePoint Server 2010 会在运行 Excel Services 的应用程序服务器上安装 SQL Server 2008 版本的 Analysis Services OLE DB 访问接口。 在支持 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问的场中，运行请求 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的应用程序（如 Excel Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint）的所有物理服务器都必须使用更高版本的数据提供程序。  
  
 运行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的服务器将自动获取更新后的 OLE DB 数据提供程序。 必须对其他服务器（例如运行独立 Excel Services 实例、但在同一台计算机上没有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的服务器）进行修补才能使用更高版本的客户端库。 有关更多信息，请参见 [Install the Analysis Services OLE DB Provider on SharePoint Servers](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
 **应用场景 3：域控制器不可用**  
  
 原因可能是域控制器不可用于确认用户标识。 Claims to Windows Token Service 要求域控制器针对每个连接验证 SharePoint 用户的身份。 Claims to Windows Token Service 不使用缓存凭据。 它会验证每个连接的用户标识。  
  
 您可以通过查看 SharePoint 日志文件确认导致此错误的原因。 如果 SharePoint 日志包括消息“Failed to get WindowsIdentity from IClaimsIdentity”，则无法对该用户标识进行身份验证。  
  
 若要解决此问题，请将计算机加入到与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器相同的域中，或在本地计算机上安装一个域控制器。 第二种解决方案是安装域控制器，这将要求您为所有服务和用户创建本地域帐户。 您将需要为您定义的帐户配置服务帐户和 SharePoint 权限。  
  
 如果你的目标是在脱机状态下使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则在计算机上安装域控制器将非常有用。 有关详细说明如何使用[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]脱机，请参阅博客文章以了解"采用你[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务器与网络断开"上[ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241)。  
  
 **应用场景 4：服务器不稳定**  
  
 一个或多个服务可能处于不一致的状态。 在某些情况下，运行 IISRESET 将会解决该问题。  
  
  
