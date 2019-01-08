---
title: 无法刷新工作簿中用于数据连接的数据。 请重试，或与系统管理员联系。 以下连接无法刷新：PowerPivot 数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0f6fd52d-ac72-43e3-aa08-05a2d2bb873d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7904e42d9ffd82d2c8a5ec7f5c9226d01c5059ef
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370999"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook-try-again-or-contact-your-system-administrator-the-following-connections-failed-to-refresh-powerpivot-data"></a>无法刷新工作簿中用于数据连接的数据。 请重试，或与系统管理员联系。 以下连接无法刷新：PowerPivot 数据
  对于包含 PowerPivot 数据的 Excel 工作簿，如果 Excel Services 提交对某一 PowerPivot 服务器的连接请求并且该请求失败，则会返回此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用范围：|PowerPivot for SharePoint 安装|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|请参阅下文。|  
|消息正文|无法刷新工作簿中用于数据连接的数据。 请重试，或与系统管理员联系。 以下连接无法刷新：PowerPivot 数据|  
  
## <a name="explanation-and-resolution"></a>说明和解决方法  
 Excel Services 无法连接到或加载 PowerPivot 数据。 在下列情况下会出现此错误：  
  
 **方案 1:服务未启动**  
  
 SQL Server Analysis Services (PowerPivot) 实例未启动。 到期的密码将导致服务停止运行。 有关更改密码的详细信息，请参阅[配置 PowerPivot 服务帐户](configure-power-pivot-service-accounts.md)并[启动或停止 PowerPivot for SharePoint 服务器](start-or-stop-a-power-pivot-for-sharepoint-server.md)。  
  
 **应用场景 2a:打开早期版本的工作簿的服务器**  
  
 您正尝试打开的工作簿可能是在 SQL Server 2008 R2 版本的 PowerPivot for Excel 中创建的。 数据连接字符串中指定的 Analysis Services 数据访问接口很可能在要处理请求的计算机上不存在。  
  
 如果出现这种情况，你将在 ULS 日志中看到此消息："刷新工作簿中的 'PowerPivot 数据' 失败 '\<指向工作簿 URL >'"后, 跟"无法获取连接"。  
  
 若要确定工作簿的版本，请在 Excel 中打开它，然后查看连接字符串中指定的数据访问接口。 SQL Server 2008 R2 工作簿将 MSOLAP.4 用作其数据访问接口。  
  
 若要解决此问题，可以升级工作簿。 或者，可以在运行 PowerPivot for SharePoint 或 Excel Services 的物理计算机上安装 SQL Server 2008 R2 版本的 Analysis Services 中的客户端库：  
  
 [在 SharePoint 服务器上安装 Analysis Services OLE DB Provider](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 **应用场景 2b:Excel Services 正在具有错误版本的客户端库的应用程序服务器**  
  
 默认情况下，SharePoint Server 2010 会在运行 Excel Services 的应用程序服务器上安装 SQL Server 2008 版本的 Analysis Services OLE DB 访问接口。 在支持 PowerPivot 数据访问的场中，运行请求 PowerPivot 数据的应用程序（如 Excel Services 和 PowerPivot for SharePoint）的所有物理服务器都必须使用更高版本的数据访问接口。  
  
 运行 PowerPivot for SharePoint 的服务器将自动获取更新后的 OLE DB 数据访问接口。 必须对其他服务器（例如运行独立 Excel Services 实例、但在同一台计算机上没有 PowerPivot for SharePoint 的服务器）进行修补才能使用更高版本的客户端库。 有关详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
 **方案 3:域控制器不可用**  
  
 原因可能是域控制器不可用于确认用户标识。 Claims to Windows Token Service 要求域控制器针对每个连接验证 SharePoint 用户的身份。 Claims to Windows Token Service 不使用缓存凭据。 它会验证每个连接的用户标识。  
  
 您可以通过查看 SharePoint 日志文件确认导致此错误的原因。 如果 SharePoint 日志包括消息“Failed to get WindowsIdentity from IClaimsIdentity”，则无法对该用户标识进行身份验证。  
  
 若要解决此问题，请将计算机加入到与 PowerPivot 服务器相同的域中，或在本地计算机上安装一个域控制器。 第二种解决方案是安装域控制器，这将要求您为所有服务和用户创建本地域帐户。 您将需要为您定义的帐户配置服务帐户和 SharePoint 权限。  
  
 如果您的目标是在脱机状态下使用 PowerPivot for SharePoint，则在计算机上安装域控制器将非常有用。 有关如何脱机使用 PowerPivot 的详细的说明，请参阅博客条目的"使 PowerPivot 服务器断开网络" [ http://www.powerpivotgeek.com ](https://go.microsoft.com/fwlink/?LinkId=184241)。  
  
 **方案 4:服务器不稳定**  
  
 一个或多个服务可能处于不一致的状态。 在某些情况下，运行 IISRESET 将会解决该问题。  
  
  
