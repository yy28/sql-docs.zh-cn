---
title: Microsoft OLE DB 远程处理提供程序 （ADO 服务提供商） |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f132bb8124afecea1b1f7fb519ecf64d1cfe88a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB 远程处理提供程序概述
Microsoft OLE DB 远程处理提供了让客户端计算机上的本地用户以调用在远程计算机上的数据提供程序。 就像你可以像远程计算机上的本地用户，请指定远程计算机的数据提供程序参数。 然后指定远程处理提供程序用于访问远程计算机的参数。 然后，就可以访问远程计算机，就像是本地用户。

> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。

## <a name="provider-keyword"></a>提供程序关键字
 若要调用 OLE DB 远程处理提供程序，请在连接字符串中指定以下关键字和值。 （请注意在提供程序名称中的空白区域。）

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>其他关键字
 当调用此服务提供程序时，以下的其他关键字是相关的。

|关键字|Description|
|-------------|-----------------|
|**数据源**|指定远程数据源的名称。 它将传递到 OLE DB 远程处理提供程序进行处理。<br /><br /> 此关键字等效于[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的[连接](../../../ado/reference/rds-api/connect-property-rds.md)属性。|

## <a name="dynamic-properties"></a>动态属性
 当调用此服务提供程序时，将下面的动态属性添加到[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。

|动态属性名称|Description|
|---------------------------|-----------------|
|**DFMode**|指示 DataFactory 模式。 一个字符串，指定所需的版本[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)服务器上的对象。 打开一个连接以请求的特定版本之前设置此属性**DataFactory**。 如果请求的版本不可用，将尝试使用以前的版本。 如果没有以前的版本，则将出错。 如果**DFMode**小于可用的版本中，将会出错。 在建立连接后，此属性是只读的。<br /><br /> 可以是下列有效的字符串值之一：<br /><br /> -"25"-版本 2.5 （默认值）<br />-"21"-版本 2.1<br />-"20"-版本 2.0<br />-"15"-1.5 版|
|**命令属性**|指示将添加到由 MS 远程提供程序发送到服务器的命令 （行集） 属性的字符串的值。 此字符串的默认值是 vt_empty。|
|**当前 DFMode**|指示的实际版本数**DataFactory**服务器上。 检查此属性以了解是否请求中的版本**DFMode**接受属性。<br /><br /> 可以是下列有效的长整型值之一：<br /><br /> -25-版本 2.5 （默认值）<br />-21-版本 2.1<br />-20-2.0 版<br />-15-1.5 版<br /><br /> 添加"DFMode = 20;"到连接字符串使用时**MSRemote**时更新数据，提供程序可以提高你的服务器的性能。 使用此设置，**提高**服务器上的对象使用的不太占用大量资源的模式。 但是，以下功能不可用在此配置：<br /><br /> -使用参数化的查询。<br />-获取之前调用的参数或列信息**执行**方法。<br />-设置**Transact 更新**到**True**。<br />-获取行状态。<br />-调用**重新同步**方法。<br />-通过刷新 （显式或自动）**更新重新同步**属性。<br />-设置**命令**或**记录集**属性。<br />-使用**adCmdTableDirect**。|
|**处理程序**|指示扩展的功能的服务器端自定义程序 （或处理） 的名称[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，和处理程序使用的任何参数*，*各项之间由逗号 （","). A**字符串**值。|
|**Internet 超时**|指示最大请求传送到或从服务器等待毫秒的数。 （默认值为 5 分钟）。|
|**远程提供程序**|指示要在远程服务器上使用的数据提供程序的名称。|
|**远程服务器**|指示用于此连接的服务器名称和通信协议。 此属性等效于[rds.DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象[服务器](../../../ado/reference/rds-api/server-property-rds.md)属性。|
|**Transact 更新**|当设置为**True**，此值表示当[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)执行在服务器上，它将完成在事务内。 此布尔值的动态属性的默认值是**False**。|

 您可以通过指定其名称作为连接字符串中的关键字来设置可写的动态属性。 例如，设置**Internet 超时**为五秒，通过指定的动态属性：

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 您也可设置或通过指定其名称作为到索引中检索的动态属性**属性**属性。 下面的示例演示如何获取和打印的当前值**Internet 超时**动态属性，然后将设置新值：

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>注释
 在 ADO 2.0 中，OLE DB 远程处理提供程序仅可指定的*ActiveConnection*参数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象**打开**方法。 用 ADO 2.1 从开始，提供程序还可以指定在*ConnectionString*参数[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象**打开**方法。

 等效于**rds.DataControl**对象[SQL](../../../ado/reference/rds-api/sql-property.md)属性不可用。 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象**打开**方法*源*改为使用自变量。

 **请注意**"...; 指定远程提供程序 = MS 远程;..."将创建四个层方案。 超出三个层的方案未经测试和应不必需的。

## <a name="example"></a>示例
 此示例执行一个查询在**作者**表**Pubs**名为的服务器上的数据库*您的服务器*。 中提供了远程数据源和远程服务器的名称[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，并且 SQL 查询中指定[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 A**记录集**返回、 编辑和用于更新数据源对象。

```
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=http://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>另请参阅
 [OLE DB 远程处理提供程序的概述](http://msdn.microsoft.com/en-us/4083b72f-68c4-4252-b366-abb70db5ca2b)
