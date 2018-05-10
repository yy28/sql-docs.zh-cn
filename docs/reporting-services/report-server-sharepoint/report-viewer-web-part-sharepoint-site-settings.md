---
title: 用于报表查看器 Web 部件的 SharePoint 网站设置 - SSRS | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: jt000
ms.author: jasontre
ms.openlocfilehash: 57e0e7ca8aa76570f70ae2279964d47f50da31aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part---reporting-services"></a>用于报表查看器 Web 部件的 SharePoint 网站设置 - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

报表查看器 Web 部件有一些可配置的设置。 可由网站管理员在 SharePoint 网站设置页上启用或禁用这些设置。 请注意，每个站点都有其自己的设置。 另外，重新安装报表查看器 Web 部件之后，不会重置这些设置。

## <a name="accessing-the-site-settings-page"></a>访问“站点设置”页

可通过以下操作访问网站设置：

1. 在 SharePoint 网站上，选择左上角的“齿轮”图标并选择“网站设置”。

    ![从齿轮图标进行网站设置。](media/sharepoint-site-settings.png)

2. 单击“Reporting Services”网站设置组中的“报表查看器 Web 部件设置”。

    > [!NOTE]
    > 还可通过直接导航到 `<site>/_layouts/15/ReportViewerWebPart/ReportViewerWebPartSettings.aspx` 访问网站设置

## <a name="report-viewer-web-part-settings"></a>报表查看器 Web 部件设置

|设置|注释|  
|-------------|--------------|  
|收集使用情况数据|启用要发送给 Microsoft 的错误和使用情况信息，以帮助改进产品。 有关 Microsoft 错误报表数据收集策略的信息，请参阅 [Microsoft SQL Server 隐私声明](https://go.microsoft.com/fwlink/?linkid=860782&clcid=0x409)。|  
|启用报表的辅助功能元数据|为呈现的报表设置 [`AccessibleTablix` 设备信息](../html-device-information-settings.md)。| 
