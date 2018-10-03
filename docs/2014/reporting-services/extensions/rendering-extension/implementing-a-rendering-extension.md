---
title: 实现呈现扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 665b13c8a163c67a800ee0a1771da46af58ab67c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113690"
---
# <a name="implementing-a-rendering-extension"></a>实现呈现扩展插件
  呈现扩展插件是将报表数据和布局信息转换为设备特定格式的报表服务器的组件或模块。 SQL Server Reporting Services 包含六种呈现扩展插件：HTML、Excel、Word、CSV 或 Text、XML、Image 和 PDF。 您可以创建其他呈现扩展插件以便以其他格式生成报表。  
  
> [!NOTE]  
>  若要确定哪些呈现扩展插件可用，您可以在 RSReportServer.config 文件中查看已安装的扩展插件列表。  
  
## <a name="in-this-section"></a>本节内容  
 [呈现扩展插件概述](rendering-extensions-overview.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 编写自定义呈现扩展插件。  
  
 [实现 IRenderingExtension 接口](implementing-the-irenderingextension-interface.md)  
 说明呈现扩展插件的属性。  
  
 [部署呈现扩展插件](deploying-a-rendering-extension.md)  
 说明如何将呈现扩展插件部署到报表服务器。  
  
 [删除呈现扩展插件](removing-a-rendering-extension.md)  
 说明如何从报表服务器上删除呈现扩展插件。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 扩展插件](../reporting-services-extensions.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
