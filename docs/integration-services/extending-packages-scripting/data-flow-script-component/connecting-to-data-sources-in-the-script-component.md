---
title: "Connecting to Data Sources in the Script Component |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
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
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2accca553f1bd9c536076fd0bbcebbff0ff2c42
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-component"></a>在脚本组件中连接数据源
  连接管理器是一个封装和存储连接特定类型数据源所需信息的便利单元。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](../../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
 你可以进行现有连接管理器可用于访问源或目标组件中的自定义脚本通过单击**添加**和**删除**按钮**连接管理器**页**脚本转换编辑器**。 但是，您必须编写自己的自定义代码才能加载或保存数据，并且才有可能打开和关闭与数据源的连接。 有关详细信息**连接管理器**页**脚本转换编辑器**，请参阅[配置脚本组件编辑器中的脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)和[脚本转换编辑器 &#40;连接管理器页 &#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 脚本组件创建**连接**中的集合类**ComponentWrapper**包含强类型化访问器为每个具有相同的名称为连接管理器本身的连接管理器的项目项。 此集合公开通过**连接**属性**ScriptMain**类。 该取值函数属性返回对作为 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 实例的连接管理器的引用。 例如，如果已在对话框的“连接管理器”页中添加名为 `MyADONETConnection` 的连接管理器，则可在脚本中添加以下代码来获取对该连接管理器的引用：  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  你必须知道的之前调用返回的连接管理器的连接类型**AcquireConnection**。 因为脚本任务具有**Option Strict**启用，你必须强制转换的连接，作为类型返回**对象**，到适当的连接类型后，才能使用。  
  
 接下来，调用**AcquireConnection**的特定连接管理器，以获取基础的连接或连接到数据源所需的信息的方法。 例如，你获得对引用**System.Data.SqlConnection**包装 ADO.NET 连接管理器通过使用下面的代码：  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 相反，对平面文件连接管理器的相同调用只返回该文件数据源的路径和文件名。  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 然后必须提供此路径和文件名称在**System.IO.StreamReader**或**Streamwriter**读取或写入平面文件中的数据。  
  
> [!IMPORTANT]  
>  当脚本组件中编写托管的代码时，不能调用 AcquireConnection 方法的连接管理器返回非托管的对象，如 OLE DB 连接管理器和 Excel 连接管理器。 但是，你可以读取这些连接管理器中的 ConnectionString 属性，并连接到数据源在代码中直接使用 OLEDB 连接字符串**连接**从**System.Data.OleDb**命名空间。  
>   
>  如果你需要调用 AcquireConnection 方法的返回非托管的对象的连接管理器，使用 ADO.NET 连接管理器。 配置 ADO.NET 连接管理器为使用 OLE DB 访问接口时，该连接管理器使用用于 OLE DB 的 .NET Framework 数据访问接口进行连接。 在这种情况下，AcquireConnection 方法返回**System.Data.OleDb.OleDbConnection**而不是非托管对象。 若要使用 Excel 数据源配置为使用 ADO.NET 连接管理器，选择 Microsoft OLE DB Provider for Jet，指定 Excel 工作簿，，然后输入`Excel 8.0`（Excel 97 及更高版本） 的值作为**扩展属性**上**所有**页**连接管理器**对话框。  
  
 有关如何使用脚本组件使用连接管理器的详细信息，请参阅[使用脚本组件创建源](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)和[使用脚本组件创建目标](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;连接](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [创建连接管理器](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
