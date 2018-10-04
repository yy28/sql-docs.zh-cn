---
title: 实现数据处理扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 919f77d0f2295091133203de2474cf81a070d956
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162187"
---
# <a name="implementing-a-data-processing-extension"></a>实现数据处理扩展插件
  借助于 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的数据处理扩展插件，您可以连接到数据源并检索数据。 它们还可以充当数据源和数据集之间的桥梁。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件是模仿 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 数据提供程序接口的子集创建的。  
  
## <a name="in-this-section"></a>本节内容  
 [数据处理扩展插件概述](data-processing-extensions-overview.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 编写自定义数据处理扩展插件。  
  
 [准备实现数据处理扩展插件](preparing-to-implement-a-data-processing-extension.md)  
 介绍在实现 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件时可用的接口以及何时要求实现特定接口。  
  
 [创建数据处理扩展插件库](creating-a-data-processing-extension-library.md)  
 介绍如何为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件分配命名空间以及如何将数据处理扩展插件编译成库 DLL。  
  
 [为数据处理扩展插件实现 Connection 类](implementing-a-connection-class-for-a-data-processing-extension.md)  
 介绍连接的属性以及如何为数据处理扩展插件实现你自己的 Connection 类。  
  
 [为数据处理扩展插件实现 Command 类](implementing-a-command-class-for-a-data-processing-extension.md)  
 介绍命令的属性以及如何为数据处理扩展插件实现你自己的 Command 类。  
  
 [为数据处理扩展插件实现 DataReader 类](implementing-a-datareader-class-for-a-data-processing-extension.md)  
 介绍数据读取器的属性以及如何为数据处理扩展插件实现自己的 DataReader 类。  
  
 [将外部数据集用于 Reporting Services](using-an-external-dataset-with-reporting-services.md)  
 介绍如何向报表服务器公开自定义 DataSet 对象以供使用。  
  
 [部署数据处理扩展插件](deploying-a-data-processing-extension.md)  
 介绍如何部署数据处理扩展插件。  
  
 [调试数据处理扩展插件代码](debugging-data-processing-extension-code.md)  
 介绍如何调试数据处理扩展插件中的代码。  
  
 [删除数据处理扩展插件](removing-a-data-processing-extension.md)  
 介绍如何从报表服务器或报表设计器中删除数据处理扩展插件。  
  
 有关完全实现的数据处理扩展插件的示例，请参阅 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 扩展插件](../reporting-services-extensions.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
