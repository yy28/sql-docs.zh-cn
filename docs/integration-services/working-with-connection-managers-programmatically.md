---
title: "以编程方式使用连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9093b9eadce231aea248cd04c2b57dc5dd5e1a76
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-connection-managers-programmatically"></a>以编程方式使用连接管理器
  在[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]，关联的连接管理器类的 AcquireConnection 方法是最常时你正在使用连接管理器在托管代码中调用的方法。 当你编写托管的代码时，你必须调用 AcquireConnection 方法使用的功能的连接管理器。 无论是在脚本任务、脚本组件、自定义对象还是自定义应用程序中编写托管代码，都必须调用此方法。  
  
 若要成功调用 AcquireConnection 方法，你必须知道以下问题的答案：  
  
-   **连接管理器从 AcquireConnection 方法返回托管的对象？**  
  
     许多连接管理器返回非托管的 COM 对象 (System.__ComObject) 这些对象无法轻松地使用和从托管代码。 此类连接管理器的列表包括经常使用的 OLE DB 连接管理器。  
  
-   **对于这些连接管理器返回托管的对象，哪些对象其 AcquireConnection 方法返回？**  
  
     若要强制转换为适当的类型的返回值，你必须知道什么类型的 AcquireConnection 方法返回的对象。 例如，有关 AcquireConnection 方法[!INCLUDE[vstecado](../includes/vstecado-md.md)]连接管理器在您使用 SqlClient 提供程序返回打开的 SqlConnection 对象。 但是，文件连接管理器的 AcquireConnection 方法只返回一个字符串。  
  
 本主题回答 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中包含的连接管理器的这些问题。  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>不返回托管代码的连接管理器  
 下表列出的连接管理器从 AcquireConnection 方法返回本机 COM 对象 (System.__ComObject)。 无法轻松地从托管代码中使用这些非托管代码。  
  
|连接管理器类型|连接管理器名称|  
|-----------------------------|-----------------------------|  
|ADO|ADO 连接管理器|  
|MSOLAP90|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 连接管理器|  
|EXCEL|Excel 连接管理器|  
|FTP|FTP 连接管理器|  
|HTTP|HTTP 连接管理器|  
|ODBC|ODBC 连接管理器|  
|OLEDB|OLE DB 连接管理器|  
  
 通常情况下，你可以使用[!INCLUDE[vstecado](../includes/vstecado-md.md)]连接管理器从托管代码，以连接到 ADO、 Excel、 ODBC 或 OLE DB 数据源。  
  
## <a name="return-values-from-the-acquireconnection-method"></a>从 AcquireConnection 方法返回值  
 下表列出的连接管理器从 AcquireConnection 方法返回托管的对象。 可以轻松地从托管代码中使用这些托管代码。  
  
|连接管理器类型|连接管理器名称|返回值的类型|其他信息|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|[!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器|**System.Data.SqlClient.SqlConnection**||  
|FILE|文件连接管理器|**System.String**|文件的路径。|  
|FLATFILE|平面文件连接管理器|**System.String**|文件的路径。|  
|MSMQ|MSMQ 连接管理器|**System.Messaging.MessageQueue**||  
|MULTIFILE|多文件连接管理器|**System.String**|其中一个文件的路径。|  
|MULTIFLATFILE|多平面文件连接管理器|**System.String**|其中一个文件的路径。|  
|SMOServer|SMO 连接管理器|**Microsoft.SqlServer.Management.Smo.Server**||  
|SMTP|SMTP 连接管理器|**System.String**|例如： `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|WMI 连接管理器|**System.Management.ManagementScope**||  
|SQLMOBILE|SQL Server Compact 连接管理器|**System.Data.SqlServerCe.SqlCeConnection**||  
  
## <a name="see-also"></a>另请参阅  
 [连接到在脚本任务中的数据源](../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [连接到脚本组件中的数据源](../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [在自定义任务中连接数据源](../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  

