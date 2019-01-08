---
title: 在尝试建立连接期间出错 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28d5bd077da96e3dd6f8a48004c3a5df1b681f61
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215737"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>在尝试建立连接期间出错
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果你在未安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的服务器上查询 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据，则系统会生成此错误。 它也会发生如果 SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 服务已停止，或者如果您尝试查看[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]从早期版本的数据。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|数据连接失败。|  
|消息正文|在尝试建立与外部数据源的连接的过程中出现错误。 以下连接无法刷新：[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据|  
  
## <a name="explanation"></a>解释  
 在查询时，Excel Services 将返回此错误[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]发布到 SharePoint 和 SharePoint 环境的 Excel 工作簿中的数据不具有[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]for SharePoint 服务器或 SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])服务已停止。  
  
 当你对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据执行切片或筛选操作时，如果查询引擎不可用，则系统会生成此错误。  
  
## <a name="user-action"></a>用户操作  
 安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，或者将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿移到安装了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 环境中。 有关详细信息，请参阅 [Power Pivot for SharePoint 2010 安装](http://msdn.microsoft.com/8d47dde7-c941-4280-a934-e2fe3f9a938f)。  
  
 如果安装了软件，请验证 SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 实例正在运行。 请在管理中心内检查 **“管理服务器上的服务”** 。 还要在“管理工具”中检查“服务”控制台应用程序。  
  
 对于在 SQL Server 2008 R2 版本的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中创建的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿，你必须安装 SQL Server 2008 R2 版本的 Analysis Services OLE DB 提供程序。 如果您安装了该访问接口，但未注册 Microsoft.AnalysisServices.ChannelTransport.dll 文件，则将出现此错误。 有关文件注册的详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
## <a name="see-also"></a>请参阅  
 [数据连接使用 Windows 身份验证并且无法对用户凭据进行委托。以下连接无法刷新：Power Pivot 数据](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  
