---
title: "RDS 编程模型，在详细信息 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e3edfd1b1ec33d4c014fae4a0fed8d61d5ef8ed
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="rds-programming-model-in-detail"></a>在详细信息的 RDS 编程模型
RDS 的编程模型的关键元素如下：  
  
-   RDS.DataSpace  
  
-   提高  
  
-   RDS.DataControl  
  
-   事件  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 在服务器和要调用的服务器程序，必须指定客户端应用程序。 反过来，你的应用程序接收到服务器程序的引用，并可以将该引用，就像它是服务器程序本身。  
  
 RDS 对象模型，它包含与此功能[rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)对象。  
  
 使用一个程序标识符，指定服务器计划或*ProgID*。 服务器使用*ProgID*和服务器计算机的注册表来查找要启动的实际程序有关的信息。  
  
 RDS 使内部具体取决于服务器计划是远程服务器上跨 Internet 或 intranet; 区别在局域网; 服务器不在或服务器上所有，而是在本地动态链接库 (DLL)。 这一区别确定信息客户端和服务器之间交换和使有形在返回到客户端应用程序的引用的类型不同的方式。 但是，从你的角度来看，这一区别的没有特殊含义。 所有重要的是接收某个可用程序的引用。  
  
## <a name="rdsserverdatafactory"></a>提高  
 RDS 提供默认的服务器程序也可以执行对数据源和返回的 SQL 查询[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象或采取**记录集**对象并更新数据源。  
  
 RDS 对象模型，它包含与此功能[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。  
  
 此外，此对象具有用于创建一个空的方法**记录集**可以以编程方式填充的对象 ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md))，并将转换的另一种方法**记录集**对象转换为文本字符串生成的网页 ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md))。  
  
 用 ADO，你可以重写某些标准连接和命令行为**提高**与**DataFactory**命令处理程序，并包含连接的自定义文件时，和安全参数。  
  
 服务器程序有时称为*业务对象*。 你可以编写你自己自定义业务对象，用于执行复杂的数据访问、 有效性检查和等等。 即使编写自定义业务对象，你可以创建的实例**提高**对象，并使用它的一些方法来完成您自己的任务。  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS 提供的功能组合在一种**rds.DataSpace**和**提高**，并且还启用可视控件能够轻松使用**记录集**从数据源由查询返回的对象。 RDS 尝试最常见的情况下，要执行尽可能多地若要自动访问服务器上的信息并将其显示在可视控件。  
  
 RDS 对象模型，它包含与此功能[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 **Rds.DataControl**具有两个方面。 其中一个方面关系到数据源。 如果你设置的命令和连接信息使用**连接**和**SQL**属性**rds.DataControl**，它将自动使用**rds.DataSpace**来创建为默认值的引用**提高**对象。 则**提高**将使用**连接**要连接到数据源，请使用属性值**SQL**要获取的属性值**记录集**从数据源，并返回**记录集**对象传递给**rds.DataControl**。  
  
 第二个方面与的显示返回**记录集**visual 控件中的信息。 您可以将具有的可视控件相关联**rds.DataControl** （在一个称为绑定过程） 来访问的关联中的信息**记录集**对象，在 Microsoft® Internet Explorer 中的 Web 页上显示查询结果。 每个**rds.DataControl**对象绑定一个**记录集**对象，表示对一个或多个可视控件 （例如，文本框、 组合框、 网格控件等） 的单个查询的结果。 可能有多个**rds.DataControl**每一页上的对象。 每个**rds.DataControl**对象可以连接到其他数据源，并且包含一个单独的查询的结果。  
  
 **Rds.DataControl**对象还具有其自己的方法导航、 排序和筛选的关联行**记录集**对象。 这些方法非常相似，但不是与 ADO 上的方法相同**记录集**对象。  
  
## <a name="events"></a>事件  
 RDS 支持两个其自己的事件，独立于 ADO 事件模型。 [OnReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件时调用每当**rds.DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)属性更改，因此时成功完成一个异步操作后，通知您终止，或遇到错误。 [OnError](../../../ado/reference/rds-api/onerror-event-rds.md)事件时调用时出现错误，即使异步操作期间发生错误。  
  
> [!NOTE]
>  Microsoft Internet Explorer 到 RDS 提供两个其他事件： **onDataSetChanged**，这指示**记录集**是功能，但仍检索行，和**onDataSetComplete**，这指示**记录集**完毕检索行。  
  
## <a name="see-also"></a>另请参阅  
 [RDS 的编程模型和对象](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



