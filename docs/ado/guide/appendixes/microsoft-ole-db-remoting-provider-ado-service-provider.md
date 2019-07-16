---
title: Microsoft OLE DB 远程处理提供程序 （ADO 服务提供程序） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c60567da677564c168f0601625686bdfb8b3d67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926590"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB 远程处理提供程序概述
Microsoft OLE DB 远程处理提供程序使客户端计算机上的本地用户来调用远程计算机上的数据提供程序。 指定远程计算机的数据提供程序参数，就像您像在远程计算机上的本地用户。 然后指定远程处理提供程序用于访问远程计算机的参数。 然后，就像本地用户，可以访问远程计算机。

> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。

## <a name="provider-keyword"></a>提供程序关键字
 若要调用 OLE DB 远程处理提供程序，请连接字符串中指定以下关键字和值。 （请注意在提供程序名称中的空白空间。）

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>其他关键字
 当调用该服务提供程序时，以下其他关键字是相关。

|关键字|描述|
|-------------|-----------------|
|**数据源**|指定远程数据源的名称。 它将传递到 OLE DB 远程处理提供程序进行处理。<br /><br /> 此关键字等效于[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的[Connect](../../../ado/reference/rds-api/connect-property-rds.md)属性。|

## <a name="dynamic-properties"></a>动态属性
 当调用该服务提供程序时，将以下动态属性添加到[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。

|动态属性名称|描述|
|---------------------------|-----------------|
|**DFMode**|指示数据工厂模式。 一个字符串，指定所需的版本的[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)服务器上的对象。 将此属性设置打开的连接请求的特定版本之前**DataFactory**。 如果请求的版本不可用，将尝试使用以前的版本。 如果没有以前的版本，将会出错。 如果**DFMode**小于可用的版本中，将会出错。 在建立连接后，此属性是只读的。<br /><br /> 可以是下列有效的字符串值之一：<br /><br /> -"25"的版本 2.5 （默认值）<br />-"21"的版本 2.1<br />-"20"-2.0 版<br />-"15"-1.5 版|
|**命令属性**|指示将添加到由 MS 远程提供程序发送到服务器的命令 （行集） 属性的字符串的值。 此字符串的默认值为 vt_empty。|
|**当前 DFMode**|表示实际版本号**DataFactory**在服务器上。 检查此属性以了解是否请求中的版本**DFMode**接受属性。<br /><br /> 可以是下列有效的长整型值之一：<br /><br /> -25 版本 2.5 （默认值）<br />-21-版本 2.1<br />-20 版本 2.0<br />-15 版本 1.5<br /><br /> 添加"DFMode = 20;"到连接字符串使用时**MSRemote**更新数据时，提供程序可以提高你的服务器的性能。 使用此设置，**提高**对象在服务器上的使用较低占用大量资源的模式。 但是，以下功能不可用在此配置中：<br /><br /> -使用参数化的查询。<br />-获取参数或列的信息，然后再调用**Execute**方法。<br />-设置**Transact 更新**到**True**。<br />-获取行状态。<br />-调用**重新同步**方法。<br />-通过刷新 （显式或自动）**更新重新同步**属性。<br />-设置**命令**或**记录集**属性。<br />-使用**adCmdTableDirect**。|
|**处理程序**|指示扩展功能的服务器端自定义程序 （或处理程序） 的名称[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，并由逗号分隔所有分隔处理程序，使用任何参数 （"，"）。 一个字符串值  。|
|**Internet 超时**|指示最大请求传送到 / 从服务器等待毫秒的数。 （默认值为 5 分钟）。|
|**远程提供程序**|指示要在远程服务器上使用的数据提供程序的名称。|
|**远程服务器**|指示使用此连接的服务器名称和通信协议。 此属性等效于[rds。DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象[Server](../../../ado/reference/rds-api/server-property-rds.md)属性。|
|**Transact 更新**|如果设置为 **，则返回 True**，此值指示，当[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)执行的服务器上，它将在内部完成事务。 此布尔值的动态属性的默认值是**False**。|

 此外可以通过指定其名称为连接字符串中的关键字设置可写的动态属性。 例如，设置**Internet 超时**为通过指定五秒动态属性：

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 您也可设置或通过指定其名称为索引来检索动态属性**属性**属性。 下面的示例演示如何获取和打印的当前值**Internet 超时**动态属性，然后将设置新值：

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>备注
 ADO 2.0，OLE DB 远程处理提供程序可能只在中指定*ActiveConnection*的参数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象**打开**方法。 从 ADO 2.1 开始，提供程序还可以指定在*ConnectionString*的参数[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象**打开**方法。

 等效于**rds。DataControl**对象[SQL](../../../ado/reference/rds-api/sql-property.md)属性不可用。 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象**打开**方法*源*改为使用参数。

 **请注意**"...; 指定远程提供程序 = MS 远程;..."将创建四个层方案。 三个层以外的方案尚未经过测试，并应不必需的。

## <a name="example"></a>示例
 此示例执行一个查询在**作者**表的**Pubs**名为的服务器上的数据库*YourServer*。 中提供了远程数据源和远程服务器的名称[开放](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象和 SQL 查询中指定[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 一个**记录集**返回、 编辑和用于更新数据源对象。

```vb
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=https://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>请参阅
 [OLE DB 远程处理提供程序的概述](https://msdn.microsoft.com/4083b72f-68c4-4252-b366-abb70db5ca2b)
