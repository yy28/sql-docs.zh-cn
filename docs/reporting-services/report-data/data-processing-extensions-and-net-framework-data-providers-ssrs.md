---
title: "数据处理扩展插件和.NET Framework 数据提供程序 (SSRS) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], data
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
- report data [Report Builder], accessing
ms.assetid: 42a5afb5-f4c8-4957-b1fd-77bf39afa5be
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 74e70cd67affe64f31076f362f36e813f3357f82
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="data-processing-extensions-and-net-framework-data-providers-ssrs"></a>数据处理扩展插件和 .NET Framework 数据访问接口 (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据处理扩展插件是随 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安装的组件，用于从特定类型的数据源检索数据，并提供支持报表设计和报表处理的额外功能。 A[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]数据提供程序是可从一个组件[!INCLUDE[msCoName](../../includes/msconame-md.md)]或支持的第三方源<xref:System.Data>允许您检索和修改特定类型的数据源中的数据的接口。  
  
## <a name="understanding-a-data-processing-extension"></a>了解数据处理扩展插件  
 A[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]数据处理扩展插件支持一部分<xref:System.Data>接口。 数据处理扩展插件要求对数据源进行只读访问，因此不实现写入接口和更新接口。 每个数据处理扩展插件都可提供自定义功能，以支持报表处理。 例如，数据处理扩展插件可能会支持下列功能类型：  
  
-   在连接字符串之外单独管理凭据  
  
-   支持多值参数  
  
-   检索对数据源计算的服务器聚合  
  
-   从数据源检索数据属性和数据值  
  
## <a name="understanding-a-data-provider"></a>了解数据访问接口  
 A [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] （有时称为驱动程序） 的数据提供程序支持的标准集<xref:System.Data>读取、 写入和更新数据源上的数据的接口。 对于特定类型的数据源，如果没有可用的数据处理扩展插件，则可以使用数据访问接口。 有许多第三方标准 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据访问接口可用。  
  
 因为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 具有一个可扩展的数据访问接口体系结构，所以您可以创建自定义数据处理扩展插件以包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据处理扩展插件提供的额外功能。 有关详细信息，请参阅 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)。 有关第三方数据处理扩展插件的信息，请参阅第三方数据处理扩展插件的随附文档。  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据访问接口或自定义数据处理扩展插件必须先行安装并注册，然后才能用于访问数据源中的数据。 必须同时在报表客户端和报表服务器安装并注册数据处理扩展插件，以便创作报表和查看已发布的报表。 不是所有数据访问接口都设计为在服务器环境中工作。 有关详细信息，请参阅[注册标准 .NET Framework 数据提供程序 (SSRS)](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md) 和[部署数据处理扩展插件](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据处理扩展插件概述](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
