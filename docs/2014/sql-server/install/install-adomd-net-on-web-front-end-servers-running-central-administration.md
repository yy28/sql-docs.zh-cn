---
title: 在运行管理中心的 Web 前端服务器上安装 ADOMD.NET |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2372180-e847-4cdb-b267-4befac3faf7e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f36e00a9393dcbdf1f8cbfe878b8382e6a8dac9d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952155"
---
# <a name="install-adomdnet-on-web-front-end-servers-running-central-administration"></a>在运行管理中心的 Web 前端服务器上安装 ADOMD.NET
  如果您将 PowerPivot for SharePoint 安装到具有管理中心拓扑，但没有 Excel Services 或 PowerPivot for SharePoint 的场中，并且希望对 PowerPivot 管理面板中的内置报表具有完全访问权限，则需下载和安装 Microsoft ADOMD.NET 客户端库。 该面板中的某些报表将使用 ADOMD.NET 来访问内部数据，内部数据可提供有关 PowerPivot 查询处理和场中服务器运行状况的报告数据。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010  
  
 对于 SharePoint 2013，访问接口包含在 SQL Server 功能包中。 有关如何下载 spPowerPivot.msi 的信息，请参阅 [Microsoft SQL Server 2014 功能包](https://www.microsoft.com/download/details.aspx?id=35577)  
  
### <a name="download-and-install-the-client-library"></a>下载并安装客户端库  
  
1.  在 [“SQL Server 2014 功能包”页](https://go.microsoft.com/fwlink/?LinkID=296473)上查找 Microsoft ADOMD.NET。  
  
2.  下载 `SQL_AS_ADOMD.msi` 安装程序的 x64 包。  
  
3.  运行 .msi 安装库。  
  
4.  安装完成后，重置 IIS。 打开管理命令提示符，然后键入 **IISRESET**。  
  
### <a name="verify-installation"></a>验证安装  
  
1.  转到 Windows\Assembly。  
  
2.  右键单击 Microsoft.AnalysisServices.AdomdClient 并选择 **“属性”**。  
  
3.  单击 **“版本”**。  
  
4.  验证版本是否包含12.00。\<> 的内部版本号，并且说明为 AdomdClient。  
  
## <a name="see-also"></a>另请参阅  
 [PowerPivot 管理面板和使用情况数据](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)  
  
  
