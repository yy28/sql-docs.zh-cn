---
title: 实现数据处理扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e4aaea407128642cb8ce9e8696eac0236cd60379
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="implementing-a-data-processing-extension"></a>实现数据处理扩展插件
  借助于 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的数据处理扩展插件，您可以连接到数据源并检索数据。 它们还可以充当数据源和数据集之间的桥梁。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件是模仿 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 数据提供程序接口的子集创建的。  
  
## <a name="in-this-section"></a>本节内容  
 [数据处理扩展插件概述](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 编写自定义数据处理扩展插件。  
  
 [准备实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 介绍在实现 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件时可用的接口以及何时要求实现特定接口。  
  
 [创建数据处理扩展插件库](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件分配命名空间以及如何将数据处理扩展插件编译成库 DLL。  
  
 [为数据处理扩展插件实现 Connection 类](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 介绍连接的属性以及如何为数据处理扩展插件实现你自己的 Connection 类。  
  
 [为数据处理扩展插件实现 Command 类](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 介绍命令的属性以及如何为数据处理扩展插件实现你自己的 Command 类。  
  
 [为数据处理扩展插件实现 DataReader 类](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 介绍数据读取器的属性以及如何为数据处理扩展插件实现自己的 DataReader 类。  
  
 [将外部数据集用于 Reporting Services](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 介绍如何向报表服务器公开自定义 DataSet 对象以供使用。  
  
 [部署数据处理扩展插件](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 介绍如何部署数据处理扩展插件。  
  
 [调试数据处理扩展插件代码](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 介绍如何调试数据处理扩展插件中的代码。  
  
 [删除数据处理扩展插件](../../../reporting-services/extensions/data-processing/removing-a-data-processing-extension.md)  
 介绍如何从报表服务器或报表设计器中删除数据处理扩展插件。  
  
 有关完全实现的数据处理扩展插件的示例，请参阅 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
