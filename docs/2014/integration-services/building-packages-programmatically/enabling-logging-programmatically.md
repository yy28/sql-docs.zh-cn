---
title: 以编程方式启用日志记录 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bff8df8004c4553d5fa07ebb5ca46863a998bd85
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176547"
---
# <a name="enabling-logging-programmatically"></a>以编程方式启用日志记录
  运行时引擎提供 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 对象的集合，这些对象用于在包验证和执行过程中捕获特定于事件的信息。 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 对象可用于 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer> 对象，包括 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>、<xref:Microsoft.SqlServer.Dts.Runtime.Package>、<xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> 和 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 对象。 日志记录对个别容器或整个包启用。

 有多种类型的日志提供程序可供容器使用。 这为以多种格式创建和存储日志信息提供了灵活性。 在日志记录中登记容器对象分为两个步骤：首先启用日志记录，然后选择日志提供程序。 容器的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 属性用于指定记录的事件和选择日志提供程序。

## <a name="enabling-logging"></a>启用日志记录
 每个可执行日志记录的容器中的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 属性用于确定容器的事件信息是否记录到事件日志中。 此属性从 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> 结构赋值，并且默认情况下此属性从容器的父级继承。 如果容器是包，并因此没有父级，则该属性使用 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>，其默认值为 `Disabled`。

### <a name="selecting-a-log-provider"></a>选择日志提供程序
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 属性设置为 `Enabled` 后，日志提供程序将添加到容器的 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 集合以完成该处理。 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 集合可用于 <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> 对象，该集合包含为容器选择的日志提供程序。 调用 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> 方法可创建提供程序并将其添加到集合中。 然后该方法会返回添加到集合中的日志提供程序。 每个提供程序都有其特有的配置设置，这些属性是使用 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 属性设置的。

 下表列出了可用的日志提供程序、其说明和 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 信息。

|提供程序|说明|ConfigString 属性|
|--------------|-----------------|---------------------------|
|SQL Server Profiler|生成可捕获并在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 中查看的 SQL 跟踪。 这种提供程序的默认文件扩展名是 .trc。|不需要任何配置。|
|SQL Server|将事件日志条目写入任意  **数据库的 sysssislog**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序要求指定与数据库的连接以及目标数据库的名称。|
|文本文件|将事件日志条目以逗号分隔值 (CSV) 格式写入 ASCII 文本文件。 这种提供程序的默认文件扩展名是 .log。|文件连接管理器的名称。|
|Windows 事件日志|记录到本地计算机的标准 Windows 事件日志的应用程序日志中。|不需要任何配置。|
|XML 文件|将事件日志条目写入 XML 格式的文件中。 这种提供程序的默认文件扩展名是 .xml。|文件连接管理器的名称。|

 通过设置容器的 `EventFilterKind` 和 `EventFilter` 属性可将事件包含或排除在事件日志中。 `EventFilterKind` 结构包含两个值，`ExclusionFilter` 和 `InclusionFilter`，它们指示添加到 `EventFilter` 中的事件是否包含在事件日志中。 然后赋给 `EventFilter` 属性一个字符串数组，其中包含属于筛选主题的事件的名称。

 下面的代码对包启用日志记录，将文本文件的日志提供程序添加到 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 集合，并指定要包含在日志记录输出中的事件列表。

## <a name="sample"></a>示例

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Package p = new Package();

      ConnectionManager loggingConnection = p.Connections.Add("FILE");
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";

      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");
      provider.ConfigString = loggingConnection.Name;
      p.LoggingOptions.SelectedLogProviders.Add(provider);
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute", 
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };
      p.LoggingMode = DTSLoggingMode.Enabled;

      // Add tasks and other objects to the package.

    }
  }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Runtime

Module Module1

  Sub Main()

    Dim p As Package = New Package()

    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"

    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")
    provider.ConfigString = loggingConnection.Name
    p.LoggingOptions.SelectedLogProviders.Add(provider)
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}
    p.LoggingMode = DTSLoggingMode.Enabled

    ' Add tasks and other objects to the package.

  End Sub

End Module
```

![Integration Services 图标（小）](../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。

## <a name="see-also"></a>另请参阅
 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)


