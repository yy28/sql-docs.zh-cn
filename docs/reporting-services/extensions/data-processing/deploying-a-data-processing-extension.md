---
title: "部署数据处理扩展插件 | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4acfb4c0643a3bea2654b36027e4c6756ff28698
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="deploying-a-data-processing-extension"></a>部署数据处理扩展插件
  在编写 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件并将其编译为 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 库之后，你需要使其变得可供报表服务器和报表设计器发现。 这就像将扩展插件复制到适当的目录并向适当的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配置文件添加条目一样轻松。  
  
## <a name="configuration-file-extension-element"></a>配置文件扩展插件元素  
 在配置文件中，你向报表服务器或报表设计器部署的数据处理扩展插件需要作为 Extension 元素输入。 对于报表服务器，这些文件为 RSReportServer.config；对于报表设计器则为 RSReportDesigner.config。  
  
 下表介绍数据处理扩展插件的 Extension 元素的属性。  
  
|Attribute|Description|  
|---------------|-----------------|  
|**名称**|扩展插件的唯一名称，例如，“SQL”表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据处理扩展插件，或者“OLEDB”表示 OLE DB 数据处理扩展插件。 **Name** 属性的最大长度是 255 个字符。 该名称在配置文件的 **Extension** 元素内的所有条目中必须唯一。|  
|**类型**|以逗号分隔的列表，其中包含完全限定的命名空间以及程序集的名称。|  
|**Visible**|值为 false 指示在用户界面中将不显示数据处理扩展插件。 如果未包含此属性，则默认值为 **true**。|  
  
 有关 RSReportServer.config 或 RSReportDesigner.config 文件的详细信息，请参阅 [Reporting Services 配置文件](../../../reporting-services/report-server/reporting-services-configuration-files.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[如何向报表服务器部署数据处理扩展插件](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|介绍如何将数据处理扩展插件部署到报表服务器。|  
|[如何向报表设计器部署数据处理扩展插件](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|介绍如何将数据处理扩展插件部署到报表设计器。|  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
