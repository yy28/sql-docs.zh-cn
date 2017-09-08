---
title: "部署数据处理扩展插件 |Microsoft 文档"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: dbf0fd628630b51b3e8847539888d46c0c8a590e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="deploying-a-data-processing-extension"></a>部署数据处理扩展插件
  编写并编译后你[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]到的数据处理扩展插件[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]库，你需要使它成为可发现由报表服务器和报表设计器。 这就像将扩展插件复制到适当的目录并向适当的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配置文件添加条目一样轻松。  
  
## <a name="configuration-file-extension-element"></a>配置文件扩展插件元素  
 你将部署到报表服务器或报表设计器的数据处理扩展插件需要作为输入**扩展**配置文件中的元素。 对于报表服务器，这些文件为 RSReportServer.config；对于报表设计器则为 RSReportDesigner.config。  
  
 下表描述的特性**扩展**数据处理扩展插件的元素。  
  
|Attribute|Description|  
|---------------|-----------------|  
|**名称**|扩展插件的唯一名称，例如，“SQL”表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据处理扩展插件，或者“OLEDB”表示 OLE DB 数据处理扩展插件。 **Name** 属性的最大长度是 255 个字符。 该名称在配置文件的 **Extension** 元素内的所有条目中必须唯一。|  
|**类型**|以逗号分隔的列表，其中包含完全限定的命名空间以及程序集的名称。|  
|**Visible**|值为**false**指示的数据处理扩展插件应不会显示在用户界面。 如果未包含此属性，则默认值为 **true**。|  
  
 有关 RSReportServer.config 或 RSReportDesigner.config 文件的详细信息，请参阅[Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[如何： 将数据处理扩展插件部署到报表服务器](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|介绍如何将数据处理扩展插件部署到报表服务器。|  
|[如何： 将数据处理扩展插件部署到报表设计器](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|介绍如何将数据处理扩展插件部署到报表设计器。|  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
