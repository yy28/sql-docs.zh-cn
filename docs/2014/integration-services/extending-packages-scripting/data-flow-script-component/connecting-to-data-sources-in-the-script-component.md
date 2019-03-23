---
title: 在脚本组件中连接数据源| Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96041fa9b632be0162259d72cd4001e9d7defdd5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390065"
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>在脚本组件中连接数据源
  连接管理器是一个封装和存储连接特定类型数据源所需信息的便利单元。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](../../connection-manager/integration-services-ssis-connections.md)。  
  
 单击“脚本转换编辑器”的“连接管理器”页上的“添加”和“删除”按钮，可使现有连接管理器可供源或目标组件中的自定义脚本访问。 但是，您必须编写自己的自定义代码才能加载或保存数据，并且才有可能打开和关闭与数据源的连接。 有关“脚本转换编辑器”的“连接管理器”页的详细信息，请参阅[在脚本组件编辑器中配置脚本组件](configuring-the-script-component-in-the-script-component-editor.md)和[脚本转换编辑器（“连接管理器”页）](../../script-transformation-editor-connection-managers-page.md)。  
  
 脚本组件在 `Connections` 项目项中创建一个 `ComponentWrapper` 集合类，该集合类为每个连接管理器包含一个强类型的取值函数，该取值函数与连接管理器本身同名。 此集合通过 `Connections` 类的 `ScriptMain` 属性公开。 该取值函数属性返回对作为 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 实例的连接管理器的引用。 例如，如果已在对话框的“连接管理器”页中添加名为 `MyADONETConnection` 的连接管理器，则可在脚本中添加以下代码来获取对该连接管理器的引用：  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  您在调用 `AcquireConnection` 之前必须了解连接管理器返回的连接的类型。 由于脚本任务启用了 `Option Strict`，因此在使用连接之前，必须先将连接（返回类型为 `Object`）转换为适当的连接类型。  
  
 接下来，调用特定连接管理器的 `AcquireConnection` 方法以获取基础连接或连接数据源所需的信息。 例如，可以使用以下代码获取对 ADO.NET 连接管理器包装的 System.Data.SqlConnection 的引用：  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 相反，对平面文件连接管理器的相同调用只返回该文件数据源的路径和文件名。  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 然后，必须向 `System.IO.StreamReader` 或 `Streamwriter` 提供此路径和文件名才能读或写该平面文件中的数据。  
  
> [!IMPORTANT]  
>  在脚本组件中编写托管代码时，不能调用返回非托管对象的连接管理器（如 OLE DB 连接管理器和 Excel 连接管理器）的 AcquireConnection 方法。 但是，可以读取这些连接管理器的 ConnectionString 属性，并使用 System.Data.OleDb 命名空间中 OLEDB 连接的连接字符串在代码中直接连接数据源。  
>   
>  如果需要调用返回非托管对象的连接管理器的 AcquireConnection 方法，可使用 ADO.NET 连接管理器。 配置 ADO.NET 连接管理器为使用 OLE DB 访问接口时，该连接管理器使用用于 OLE DB 的 .NET Framework 数据访问接口进行连接。 在这种情况下，AcquireConnection 方法返回`System.Data.OleDb.OleDbConnection`而不是非托管对象。 要配置用于 Excel 数据源的 ADO.NET 连接管理器，请选择 Microsoft OLE DB Provider for Jet，再指定 Excel 工作簿，然后在“连接管理器”对话框的“全部”页上输入 `Excel 8.0`（对于 Excel 97 及更高版本）作为“扩展属性”的值。  
  
 有关如何在脚本组件中使用连接管理器的详细信息，请参阅[通过脚本组件创建源](../../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)和[通过脚本组件创建目标](../../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。  
  
![集成服务图标 （小）](../../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 连接](../../connection-manager/integration-services-ssis-connections.md)   
 [创建连接管理器](../../create-connection-managers.md)  
  
  
