---
title: "报表查看器 web 部件在 SharePoint 站点上的 |Microsoft 文档"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a37ed5efe7c365c601deb95d9fe761d227e7021e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>报表查看器 web 部件在 SharePoint 站点上

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

报表查看器 web 部件是自定义 web 部件。 你可以使用 web 部件查看、 导航、 打印和导出在 SharePoint 站点内的报表服务器上的报表。 报表查看器 web 部件是由 Microsoft SQL Server Reporting Services 报表服务器处理的报表定义 (.rdl) 文件与相关联。 

最新的报表查看器 web 部件还可以部署到 Power BI 报表服务器服务已分页的报表。 Web 部件并不适用于 Power BI 报表。

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>报表查看器 web 部件为何重新引入

报表查看器 web 部件无法作为 Reporting Services 外接程序用于 SharePoint 产品的一部分。 Web 部件是特定于报表服务器在 SharePoint 集成模式下。 SharePoint 集成模式下在 SQL Server 2016 后已弃用。

从 SQL Server 自 2017 年开始，没有只有一种 Reporting Services 的安装模式：**纯模式**。 无法嵌入使用页面查看器 web 部件使用的所有报表类型*rs： 都嵌入 = true* URL 参数。 将报表嵌入到 SharePoint 页是请求的客户和更新的报表查看器 web 部件集成情景使此方案中的分页报表。

虽然页面查看器 web 部件就足够嵌入到 SharePoint 页的分页的报表，更新的报表查看器 web 部件提供了附加功能。

* 显示/隐藏特定工具栏按钮
* 重写报表参数值
* 连接到报表参数的筛选器 web 部件

## <a name="download-the-report-viewer-web-part-solution-package"></a>下载报表查看器 web 部件解决方案包

报表查看器 web 部件在 Microsoft 下载中心才可用。

[下载报表查看器 web 部件解决方案包](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>注意事项和限制

列出的项是特定于更新的报表查看器 web 部件。

* Web 部件可以只能用于*经典*SharePoint 页。
* 支持唯一分页 (RDL) 报表嵌入在报表查看器 web 部件中。 如果你希望为嵌入 Power BI 报表或移动报表，则可以使用*rs： 嵌入 = true* URL 参数。

## <a name="next-steps"></a>后续步骤

若要开始使用更新的报表查看器 web 部件，请参阅[部署报表查看器 web 部件在 SharePoint 站点上的](deploy-report-viewer-web-part.md)。

