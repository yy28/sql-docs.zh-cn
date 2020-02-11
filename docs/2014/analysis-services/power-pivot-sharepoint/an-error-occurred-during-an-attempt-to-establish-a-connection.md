---
title: 在尝试建立与外部数据源的连接的过程中出现错误。 以下连接无法刷新： PowerPivot 数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c09c8984e964b4bdfa93b0fcebae2e613d484892
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071945"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection-to-the-external-data-source-the-following-connections-failed-to-refresh-powerpivot-data"></a>在尝试建立与外部数据源的连接的过程中出现错误。 以下连接无法刷新：PowerPivot 数据
  如果您在未安装 PowerPivot for SharePoint 的服务器上查询 PowerPivot 数据，将发生此错误。 如果停止 SQL Server Analysis Services (PowerPivot) 服务，或是您试图查看以前版本的 PowerPivot 数据，此时也会发生此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|PowerPivot for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|数据连接失败。|  
|消息正文|在尝试建立与外部数据源的连接的过程中出现错误。 以下连接无法刷新：PowerPivot 数据|  
  
## <a name="explanation"></a>说明  
 当您在发布到 SharePoint 的 Excel 工作簿中查询 PowerPivot 数据时，如果 SharePoint 环境不具有 PowerPivot for SharePoint 服务器，或者 SQL Server Analysis Services (PowerPivot) 服务停止运行，Excel Services 将返回此错误。  
  
 在您切分或筛选 PowerPivot 数据时，如果查询引擎不可用，则会发生此错误。  
  
## <a name="user-action"></a>用户操作  
 安装 PowerPivot for SharePoint 或者将 PowerPivot 工作簿移到安装了 PowerPivot for SharePoint 的 SharePoint 环境。 有关详细信息，请参阅 [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)。  
  
 如果安装了该软件，则请确认 SQL Server Analysis Services (PowerPivot) 实例正在运行。 请在管理中心内检查 **“管理服务器上的服务”** 。 还要在“管理工具”中检查“服务”控制台应用程序。  
  
 对于在 SQL Server 2008 R2 版本的 PowerPivot for Excel 中创建的 PowerPivot 工作簿，必须安装 SQL Server 2008 R2 版本的 Analysis Services OLE DB 访问接口。 如果您安装了该访问接口，但未注册 Microsoft.AnalysisServices.ChannelTransport.dll 文件，则将出现此错误。 有关文件注册的详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据连接使用 Windows 身份验证，因此无法委托用户凭据。以下连接无法刷新： PowerPivot 数据](the-data-connection-user-could-not-be-delegated.md)  
  
  
