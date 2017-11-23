---
title: "在尝试建立连接的过程出错 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bbc70ccf710772ba1b32abe5b65858d95ef2b38e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>在尝试建立连接的过程时出错
  如果你在未安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的服务器上查询 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据，则系统会生成此错误。 如果 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 服务停止运行，或想要尝试查看旧版 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据，则系统也会生成此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|数据连接失败。|  
|消息正文|在尝试建立与外部数据源的连接的过程中出现错误。 以下连接刷新失败： [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据|  
  
## <a name="explanation"></a>解释  
 如果你在发布到 SharePoint 的 Excel 工作簿中查询 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据且 SharePoint 环境中没有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 服务器，或者 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 服务停止运行，则 Excel Services 会返回此错误。  
  
 当你对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据执行切片或筛选操作时，如果查询引擎不可用，则系统会生成此错误。  
  
## <a name="user-action"></a>用户操作  
 安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，或者将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿移到安装了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 环境中。 有关详细信息，请参阅 [Power Pivot for SharePoint 2010 安装](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)。  
  
 如果该软件已安装，请确认 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 实例是否正在运行。 请在管理中心内检查 **“管理服务器上的服务”** 。 还要在“管理工具”中检查“服务”控制台应用程序。  
  
 对于在 SQL Server 2008 R2 版本的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中创建的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿，你必须安装 SQL Server 2008 R2 版本的 Analysis Services OLE DB 提供程序。 如果您安装了该访问接口，但未注册 Microsoft.AnalysisServices.ChannelTransport.dll 文件，则将出现此错误。 有关文件注册的详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
## <a name="see-also"></a>另请参阅  
 [数据连接使用 Windows 身份验证并且无法对用户凭据进行委托。以下连接刷新失败：Power Pivot 数据](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  
