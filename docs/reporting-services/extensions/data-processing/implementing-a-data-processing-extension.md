---
title: "实现数据处理扩展插件 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 1497690ebccc010601542308747240d0e91d89db
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-data-processing-extension"></a>实现数据处理扩展插件
  借助于 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的数据处理扩展插件，您可以连接到数据源并检索数据。 它们还可以充当数据源和数据集之间的桥梁。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]数据处理扩展插件进行建模的子集后[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]数据提供程序接口。  
  
## <a name="in-this-section"></a>本節內容  
 [数据处理扩展概述](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 编写自定义数据处理扩展插件。  
  
 [准备实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 介绍在实现 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件时可用的接口以及何时要求实现特定接口。  
  
 [创建数据处理扩展库](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件分配命名空间以及如何将数据处理扩展插件编译成库 DLL。  
  
 [数据处理扩展的实现连接类](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 描述的连接以及如何实现你自己的特性**连接**数据处理扩展插件的类。  
  
 [对数据处理扩展插件实施命令类](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 描述的一个命令，以及如何实现你自己的特性**命令**数据处理扩展插件的类。  
  
 [实现 DataReader 类用于数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 描述的数据读取器以及如何实现你自己的特性**DataReader**数据处理扩展插件的类。  
  
 [使用 Reporting Services 的外部数据集](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 介绍如何公开您的自定义**数据集**到报表服务器使用的对象。  
  
 [部署数据处理扩展插件](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 介绍如何部署数据处理扩展插件。  
  
 [调试数据处理扩展代码](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 介绍如何调试数据处理扩展插件中的代码。  
  
 [删除数据处理扩展插件](../../../reporting-services/extensions/data-processing/removing-a-data-processing-extension.md)  
 介绍如何从报表服务器或报表设计器中删除数据处理扩展插件。  
  
 完全实现的数据处理扩展插件的示例，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

