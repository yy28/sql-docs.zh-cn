---
title: RDS 编程模型的详细信息 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b498377a32b33211f8f46a154137f483b98cb56
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773405"
---
# <a name="rds-programming-model-in-detail"></a>RDS 编程模型的详细信息
RDS 编程模型的关键元素如下：  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   事件  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 在服务器和要调用的服务器程序，必须指定客户端应用程序。 反过来，应用程序接收对服务器程序的引用，并可以将该引用，就好像服务器程序本身。  
  
 RDS 对象模型包含此功能通过[rds。数据空间](../../../ado/reference/rds-api/dataspace-object-rds.md)对象。  
  
 使用一个程序标识符，指定服务器程序或*ProgID*。 服务器使用*ProgID*和服务器计算机的注册表来查找要初始化的实际程序有关的信息。  
  
 RDS 使在内部根据服务器程序是否在远程服务器上跨 Internet 或 intranet; 区别服务器上本地局域网;或不在服务器上所有，而是在本地动态链接库 (DLL)。 这一区别确定如何在客户端和服务器之间交换和具有重要意义有形中返回到客户端应用程序的引用的类型信息。 但是，从应用角度来看，这一区别没有任何特殊的意义。 最重要的就是，您将收到某个可用的程序的引用。  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS 提供了默认的服务器程序，可以执行针对数据源并返回的 SQL 查询[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象或采取**记录集**对象并更新数据源。  
  
 RDS 对象模型包含此功能通过[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。  
  
 此外，此对象具有用于创建一个空的方法**记录集**您可以以编程方式填充的对象 ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md))，并将转换为另一种方法**记录集**到要生成的网页的文本字符串的对象 ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md))。  
  
 使用 ADO 中，您可以重写一些标准的连接和命令行为**提高**与**DataFactory**命令处理程序，并包含连接的自定义文件，和安全参数。  
  
 服务器程序有时称为*业务对象*。 您可以编写自己的自定义业务对象可以执行复杂的数据访问、 有效性检查，依次类推。 甚至在编写自定义业务对象，可以创建的实例**提高**对象，并使用它的一些方法来完成您自己的任务。  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS 提供了一种的功能合并**rds。DataSpace**和**提高**，并且启用可视控件能够轻松地**记录集**查询从数据源返回的对象。 RDS 尝试最常见的情况下，若要执行尽可能多地以自动获取访问权限的服务器上的信息并将其显示在可视控件。  
  
 RDS 对象模型包含此功能通过[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 **Rds。DataControl**具有两个方面。 与数据源相关的一个方面。 如果设置的命令和使用连接信息**Connect**并**SQL**的属性**rds。DataControl**，它将自动使用**rds。DataSpace**以创建为默认值的引用**提高**对象。 然后**提高**将使用**Connect**属性值连接到数据源，请使用**SQL**属性的值以获取**记录集**从数据源，并返回**记录集**对象传递给**rds。DataControl**。  
  
 第二个方面与显示的返回**记录集**可视控件中的信息。 可以将与可视控件相关联**rds。DataControl** （在称为绑定的进程） 并获取访问权限的信息关联**记录集**对象，在 Microsoft® Internet Explorer 中的网页上显示查询结果。 每个**rds。DataControl**对象将一个绑定**记录集**对象，表示为一个或多个可视控件 （例如，文本框、 组合框，网格控件等） 的单个查询的结果。 可能有多个**rds。DataControl**每一页上的对象。 每个**rds。DataControl**对象可以连接到不同的数据源，并包含一个单独的查询的结果。  
  
 **Rds。DataControl**对象还具有它自己的方法用于导航、 排序和筛选关联的行**记录集**对象。 这些方法非常相似，但不是与 ADO 上的方法相同**记录集**对象。  
  
## <a name="events"></a>事件  
 RDS 支持两个自己独立于 ADO 事件模型的事件。 [OnReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)调用事件时**rds。DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)属性更改，因此通知您已成功完成一个异步操作后，已终止，或遇到错误。 [OnError](../../../ado/reference/rds-api/onerror-event-rds.md)事件时出现错误，即使调用异步操作期间发生错误。  
  
> [!NOTE]
>  Microsoft Internet Explorer 到 RDS 提供两个其他事件： **onDataSetChanged**，这指示**记录集**功能，但仍检索行和**onDataSetComplete**，表示**记录集**已完成中检索行。  
  
## <a name="see-also"></a>请参阅  
 [RDS 编程模型和对象](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



