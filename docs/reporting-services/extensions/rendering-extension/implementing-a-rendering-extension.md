---
title: "实现呈现扩展插件 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
caps.latest.revision: "34"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a7b8dd1c3efc550f04f3e5eff77dccbadfe305e7
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="implementing-a-rendering-extension"></a>实现呈现扩展插件
  呈现扩展插件是将报表数据和布局信息转换为设备特定格式的报表服务器的组件或模块。 SQL Server Reporting Services 包含六种呈现扩展插件：HTML、Excel、Word、CSV 或 Text、XML、Image 和 PDF。 您可以创建其他呈现扩展插件以便以其他格式生成报表。  
  
> [!NOTE]  
>  若要确定哪些呈现扩展插件可用，您可以在 RSReportServer.config 文件中查看已安装的扩展插件列表。  
  
## <a name="in-this-section"></a>本节内容  
 [呈现扩展插件概述](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 编写自定义呈现扩展插件。  
  
 [实现 IRenderingExtension 接口](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)  
 说明呈现扩展插件的属性。  
  
 [部署呈现扩展插件](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
 说明如何将呈现扩展插件部署到报表服务器。  
  
 [删除呈现扩展插件](../../../reporting-services/extensions/rendering-extension/removing-a-rendering-extension.md)  
 说明如何从报表服务器上删除呈现扩展插件。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
