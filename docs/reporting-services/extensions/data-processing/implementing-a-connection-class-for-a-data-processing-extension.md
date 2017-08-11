---
title: "数据处理扩展的实现连接类 |Microsoft 文档"
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
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 19f059c0041cc9effc48e0db9c4b5ef1a504d020
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>为数据处理扩展插件实现 Connection 类
  **连接**对象表示的数据库连接或类似资源，并且用户的起始点[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]数据处理扩展插件。 它表示与数据库服务器的连接，但具有类似的行为的任何实体可作为公开**连接**。  
  
 若要实现**连接**对象，请创建一个类以实现<xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>并选择性实现<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>。  
  
 在实现中，您必须确保先创建和打开一个连接，然后才能执行命令。 确保您的实现要求客户端显式打开和关闭连接，而不是让实现为客户端隐式打开和关闭连接。 在获取连接时，将执行安全检查。 如果在 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 数据处理扩展插件中要求将某个现有连接用于其他类，则可以确保在使用数据源时始终执行安全检查。  
  
 所需连接的属性表示为一个连接字符串。 强烈建议 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 数据处理扩展插件使用由 OLE DB 定义的所熟悉的名称/值对系统支持 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> 属性。  
  
> [!NOTE]  
>  **连接**对象通常都是资源密集型若要获取，因此你可能想要考虑池连接或其他技术来缓解此问题。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 从 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 继承。 您必须将 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 接口作为连接类实现的一部分而实现。 借助于 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 接口，类可以实现本地化的扩展插件名称并处理存储在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 配置文件中的扩展插件特定的配置信息。  
  
 你**连接**对象包含<xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A>属性通过实现其<xref:Microsoft.ReportingServices.Interfaces.IExtension>。 强烈建议 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 数据处理扩展插件支持 <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> 属性，以便用户在用户界面（如报表管理器）中对于该扩展插件看到熟悉的本地化名称。  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension>此外允许你**连接**对象，用于检索并处理存储在 RSReportServer.config 文件中的自定义配置数据。 有关处理自定义配置数据的详细信息，请参阅 <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A> 方法。  
  
 对于实现 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 的类，当卸载其他数据处理扩展插件类时，不会从内存中卸载该类。 因此，你可以使用你**扩展**类来存储跨连接状态信息或在内存中存储可以缓存的数据。 你**扩展**类保留在内存中，只要报表服务器正在运行。  
  
 你可以扩展你**连接**类以包括对中的凭据的支持[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]通过实现<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>。 当实现<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>， <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A>，和<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A>属性<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>启用的接口，**集成安全性**复选框和**用户名**和**密码**文本框的**数据源**在报表设计器的对话框。 这使报表设计器能够针对支持身份验证的数据源存储和检索凭据。 将以安全的方式存储凭据，当以预览模式呈现报表时将使用这些凭据。  
  
> [!NOTE]  
>  隐式实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> 要求您实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 和 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 接口的成员。  
>   
>  有关示例**连接**类实现，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
