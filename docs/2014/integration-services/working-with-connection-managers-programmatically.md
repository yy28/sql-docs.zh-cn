---
title: 以编程方式使用连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 973cb7dcfe7eb95e003428adf0c8a0beb7e68e87
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877698"
---
# <a name="working-with-connection-managers-programmatically"></a>以编程方式使用连接管理器
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，关联的连接管理器类的 AcquireConnection 方法是以托管代码方式使用连接管理器时最常调用的方法。 编写托管代码时，必须调用 AcquireConnection 方法以使用连接管理器的功能。 无论是在脚本任务、脚本组件、自定义对象还是自定义应用程序中编写托管代码，都必须调用此方法。  
  
 若要成功调用 AcquireConnection 方法，必须知道以下问题的答案：  
  
-   **哪些连接管理器从 AcquireConnection 方法返回托管对象？**  
  
     许多连接管理器返回非托管 COM 对象 (System.__ComObject)，并且无法轻松地从托管代码中使用这些对象。 此类连接管理器的列表包括经常使用的 OLE DB 连接管理器。  
  
-   **对于返回托管对象的那些连接管理器，其 AcquireConnection 方法返回哪些对象？**  
  
     若要将返回值转换为适当的类型，必须知道 AcquireConnection 方法所返回的对象类型。 例如，使用 SqlClient 提供程序时，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器的 AcquireConnection 方法返回打开的 SqlConnection 对象。 但是，文件连接管理器的 AcquireConnection 方法仅返回字符串。  
  
 本主题回答 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中包含的连接管理器的这些问题。  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>不返回托管代码的连接管理器  
 下表列出了从 AcquireConnection 方法返回本机 COM 对象 (System.__ComObject) 的连接管理器。 无法轻松地从托管代码中使用这些非托管代码。  
  
|连接管理器类型|连接管理器名称|  
|-----------------------------|-----------------------------|  
|ADO|ADO 连接管理器|  
|MSOLAP90|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 连接管理器|  
|EXCEL|Excel 连接管理器|  
|FTP|FTP 连接管理器|  
|HTTP|HTTP 连接管理器|  
|ODBC|ODBC 连接管理器|  
|OLEDB|OLE DB 连接管理器|  
  
 通常，可以从托管代码使用 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器连接到 ADO、Excel、ODBC 或 OLE DB 数据源。  
  
## <a name="return-values-from-the-acquireconnection-method"></a>从 AcquireConnection 方法返回值  
 下表列出了从 AcquireConnection 方法返回托管对象的连接管理器。 可以轻松地从托管代码中使用这些托管代码。  
  
|连接管理器类型|连接管理器名称|返回值的类型|其他信息|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|[!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器|`System.Data.SqlClient.SqlConnection`||  
|FILE|文件连接管理器|`System.String`|文件的路径。|  
|FLATFILE|平面文件连接管理器|`System.String`|文件的路径。|  
|MSMQ|MSMQ 连接管理器|`System.Messaging.MessageQueue`||  
|MULTIFILE|多文件连接管理器|`System.String`|其中一个文件的路径。|  
|MULTIFLATFILE|多平面文件连接管理器|`System.String`|其中一个文件的路径。|  
|SMOServer|SMO 连接管理器|`Microsoft.SqlServer.Management.Smo.Server`||  
|SMTP|SMTP 连接管理器|`System.String`|例如： `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|WMI 连接管理器|`System.Management.ManagementScope`||  
|SQLMOBILE|SQL Server Compact 连接管理器|`System.Data.SqlServerCe.SqlCeConnection`||  
  
![集成服务图标 （小）](media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [在脚本任务中连接数据源](extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [在脚本组件中连接数据源](extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [在自定义任务中连接数据源](extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
