---
title: Close 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e692e8853417abae386ac151eca4b49f11b12f02
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698998"
---
# <a name="close-method-ado"></a>Close 方法 (ADO)
关闭打开的对象和所有依赖对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>备注  
 使用**关闭**方法以关闭[连接](../../../ado/reference/ado-api/connection-object-ado.md)即[记录](../../../ado/reference/ado-api/record-object-ado.md)即[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，或[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象若要释放所有关联的系统资源。 关闭对象不会删除它从内存;可以更改其属性设置，并在以后再次打开它。 若要完全消除从内存对象，关闭该对象，然后将对象变量设置为*Nothing* （在 Visual Basic)。  
  
## <a name="connection"></a>连接  
 使用**关闭**方法以关闭**连接**对象也会关闭任何活动**记录集**与连接关联的对象。 一个[命令](../../../ado/reference/ado-api/command-object-ado.md)与关联的对象**连接**将会保留你在关闭的对象，但它不能再将关联**连接**对象; 即，其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性将设置为**Nothing**。 此外，**命令**对象的[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合将被清除的任何提供程序定义的参数。  
  
 你可以稍后调用[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法以重新建立与源相同，或其他数据源连接。 虽然**连接**对象已关闭，则调用需要与数据源的开放连接的任何方法将产生错误。  
  
 关闭**连接**对象时没有开放**记录集**在连接上的对象将回滚所有挂起的更改中的所有**记录集**对象。 显式关闭**连接**对象 (调用**关闭**方法) 在事务正在进行生成错误。 如果**连接**对象超出作用域事务正在进行时，ADO 自动回滚事务。  
  
## <a name="recordset-record-stream"></a>记录集，则请记录，Stream  
 使用**关闭**方法以关闭**记录集**，**记录**，或者**Stream**对象释放关联的数据和任何独占访问权限你可能已具有通过此特定对象的数据。 你可以稍后调用[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法重新打开具有相同，或修改对象属性。  
  
 虽然**记录集**对象已关闭，则调用需要实时游标的任何方法将产生错误。  
  
 如果编辑正在进行中立即更新模式中，则调用**关闭**方法将生成错误; 而是调用[更新](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一个。 如果关闭**记录集**对象在批更新模式中，最后一个之后的所有更改[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)调用都将丢失。  
  
 如果您使用[克隆](../../../ado/reference/ado-api/clone-method-ado.md)方法来创建副本的一种开放**记录集**对象，则关闭原始或克隆不会影响任何其他副本。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [Open 和 Close 方法示例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法示例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法示例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
