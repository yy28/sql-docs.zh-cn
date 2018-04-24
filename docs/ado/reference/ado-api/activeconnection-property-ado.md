---
title: ActiveConnection 属性 (ADO) |Microsoft 文档
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
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00ca9b4b45deb31f3b0f4d233a452b58e9f8e40f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 属性 (ADO)
指示到[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象指定[命令](../../../ado/reference/ado-api/command-object-ado.md)，[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，或[记录](../../../ado/reference/ado-api/record-object-ado.md)当前所属的对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值，如果连接已关闭，或包含连接的定义**Variant**包含当前**连接**对象如果连接为打开状态。 默认值为空对象引用。 请参阅[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性。  
  
## <a name="remarks"></a>注释  
 使用**ActiveConnection**属性来确定**连接**通过该对象指定**命令**对象执行或指定**记录集**将打开。  
  
## <a name="command"></a>Command  
 有关**命令**对象， **ActiveConnection**属性为读/写。  
  
 如果你尝试调用[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法**命令**对象之前将此属性设置为打开**连接**对象或有效的连接字符串时，发生错误。  
  
 如果**连接**对象分配给**ActiveConnection**属性，必须打开的对象。 分配已关闭的连接对象会导致错误。  
  
### <a name="note"></a>注意  
 **Microsoft Visual Basic**设置**ActiveConnection**属性*执行任何操作*解除关联**命令**对象从当前**连接**并导致要释放任何关联的资源上的数据源的提供程序。 然后可以将关联**命令**具有相同或另一个对象**连接**对象。 某些提供程序允许你从一个更改的属性设置**连接**到另一个，而无需先将该属性设置为*执行任何操作*。  
  
 如果[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合**命令**对象包含由提供商提供的参数，如果你设置清除集合**ActiveConnection**属性设置为*执行任何操作*或其他**连接**对象。 如果你手动创建[参数](../../../ado/reference/ado-api/parameter-object.md)对象并使用它们来填充**参数**集合**命令**对象，并设置**ActiveConnection**属性*执行任何操作*或其他**连接**对象使**参数**集合保持不变。  
  
 关闭**连接**与其对象**命令**对象是关联的 set **ActiveConnection**属性*执行任何操作*。 此属性设置为关闭**连接**对象生成一个错误。  
  
## <a name="recordset"></a>记录集  
 打开**记录集**对象或**记录集**对象其[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性设置为有效**命令**对象、 **ActiveConnection**属性是只读的。 否则，它为读/写。  
  
 你可以将此属性设置为有效**连接**对象或有效的连接字符串。 在这种情况下，提供程序创建一个新**连接**对象使用此定义，并打开该连接。 此外，提供程序可能将此属性设置到新**连接**对象为你提供一种访问方法**连接**对象扩展的错误的信息或执行其他命令。  
  
 如果你使用*ActiveConnection*参数[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法打开**记录集**对象， **ActiveConnection**属性将继承自变量的值。  
  
 如果你设置**源**属性**记录集**到有效的对象**命令**对象变量， **ActiveConnection**属性**记录集**继承的设置**命令**对象的**ActiveConnection**属性。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**记录集**对象，可以设置此属性，只对连接字符串或 （在 Microsoft Visual Basic 或 Visual Basic Scripting Edition） 到*执行任何操作*.  
  
## <a name="record"></a>記錄  
 此属性为读/写时**记录**对象已关闭，并且可能包含的连接字符串或对打开引用**连接**对象。 此属性为只读时**记录**对象处于打开状态，并包含对已打开的引用**连接**对象。  
  
 A**连接**时在隐式创建对象**记录**从 URL 中打开对象。 打开**记录**与一个现有打开**连接**通过分配的对象**连接**对象传递给此属性，或使用**连接**对象中的参数作为[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法调用。 如果**记录**打开从现有**记录**或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，则它是自动关联的**记录**或**记录集**对象的**连接**对象。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
