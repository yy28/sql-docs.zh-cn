---
title: ActiveConnection 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f423eb2d06ccdc925402d0db5d8a459f7ffdd5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698926"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 属性 (ADO)
指示向其[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象指定[命令](../../../ado/reference/ado-api/command-object-ado.md)，[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，或者[记录](../../../ado/reference/ado-api/record-object-ado.md)当前所属对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值，该值包含连接的定义，如果连接已关闭，或**变体**包含当前**连接**对象如果连接处于打开状态。 默认值为空对象引用。 请参阅[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性。  
  
## <a name="remarks"></a>备注  
 使用**ActiveConnection**属性来确定**连接**通过该对象指定**命令**将执行对象或指定**记录集**将打开。  
  
## <a name="command"></a>Command  
 有关**命令**对象， **ActiveConnection**属性为读/写。  
  
 如果你尝试调用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法**命令**对象之前将此属性设置为一种开放**连接**对象或有效的连接字符串，就会出错。  
  
 如果**连接**对象分配给**ActiveConnection**属性，必须打开对象。 分配已关闭的连接对象会导致错误。  
  
### <a name="note"></a>注意  
 **Microsoft Visual Basic**设置**ActiveConnection**属性设置为*Nothing*取消关联**命令**对象从当前**连接**并导致要释放数据源上的所有关联的资源的提供程序。 然后，可以将关联**命令**具有相同或另一个对象**连接**对象。 某些提供程序允许您从一个更改的属性设置**连接**到另一个，而无需首先将该属性设置为*Nothing*。  
  
 如果[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)系列**命令**对象包含提供程序提供的参数，如果将清除集合**ActiveConnection**属性设置为*Nothing*或另一个**连接**对象。 如果您手动创建[参数](../../../ado/reference/ado-api/parameter-object.md)对象，并使用它们来填充**参数**的集合**命令**对象，设置**ActiveConnection**属性设置为*Nothing*或另一个**连接**对象叶**参数**集合保持不变。  
  
 关闭**连接**对象与其**命令**对象是关联的集**ActiveConnection**属性设置为*Nothing*。 此属性设置为已关闭**连接**对象生成一个错误。  
  
## <a name="recordset"></a>记录集  
 为开放**记录集**对象; 二是**记录集**对象其[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性设置为有效**命令**对象、 **ActiveConnection**属性是只读的。 否则，它为读/写。  
  
 可以将此属性设置为有效**连接**对象或到有效的连接字符串。 在这种情况下，该提供程序创建一个新**连接**对象使用此定义，并打开的连接。 此外，该提供程序可能会将此属性设置到新**连接**对象，为您提供一种访问方法**连接**对象扩展的错误的信息或执行其他命令。  
  
 如果您使用*ActiveConnection*的参数[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法以打开**记录集**对象， **ActiveConnection**属性将继承自变量的值。  
  
 如果您设置**源**的属性**记录集**为有效的对象**命令**对象变量**ActiveConnection**属性**记录集**继承的设置**命令**对象的**ActiveConnection**属性。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**记录集**对象，可以设置此属性，仅为连接字符串或 （在 Microsoft Visual Basic 或 Visual Basic Scripting Edition） 到*执行任何操作*.  
  
## <a name="record"></a>录制  
 此属性为读/写时**记录**对象已关闭，并且可能包含连接字符串或打开引用**连接**对象。 此属性是只读的何时**记录**对象处于打开状态，并包含一种开放的引用**连接**对象。  
  
 一个**连接**时隐式创建对象**记录**从 URL 打开对象。 打开**记录**与某个现有打开**连接**通过分配对象**连接**对象传递给此属性，或使用**连接**对象中的参数作为[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法调用。 如果**记录**打开从现有**记录**或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，然后它会自动与该关联**记录**或**记录集**对象的**连接**对象。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
