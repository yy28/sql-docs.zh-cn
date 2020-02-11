---
title: Close 方法（ADO） |Microsoft Docs
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
ms.openlocfilehash: 8a1d153d1433a377bb488366111b75a986365132
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919935"
---
# <a name="close-method-ado"></a>Close 方法 (ADO)
关闭打开的对象和所有依赖对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>备注  
 使用**close**方法可关闭[连接](../../../ado/reference/ado-api/connection-object-ado.md)、[记录](../../../ado/reference/ado-api/record-object-ado.md)、[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或[流](../../../ado/reference/ado-api/stream-object-ado.md)对象，以释放任何关联的系统资源。 关闭对象并不会将其从内存中删除;您可以更改其属性设置，稍后再次打开它。 若要从内存中完全消除对象，请关闭对象，然后将对象变量设置为*Nothing* （在 Visual Basic 中）。  
  
## <a name="connection"></a>连接  
 使用**close**方法关闭**连接**对象也会关闭与该连接关联的任何活动**记录集**对象。 与正在关闭的**连接**对象关联的[命令](../../../ado/reference/ado-api/command-object-ado.md)对象将会保持不变，但它将不再与**连接**对象关联;也就是说，其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性将设置为**Nothing**。 此外，将清除**命令**对象的[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合中的任何提供程序定义的参数。  
  
 稍后可以调用[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法来重新建立与相同或其他数据源的连接。 **连接**对象关闭时，调用任何需要打开到数据源的连接的方法都会生成错误。  
  
 如果在连接上存在打开的**记录集**对象时关闭**连接**对象，则会回滚所有**记录集**对象中的所有挂起的更改。 当事务正在进行时，显式关闭**连接**对象（调用**Close**方法）会生成错误。 如果某个**连接**对象在事务正在进行时超出范围，则 ADO 会自动回滚该事务。  
  
## <a name="recordset-record-stream"></a>记录集，记录，流  
 使用**close**方法关闭**Recordset**、 **Record**或**Stream**对象时，将释放关联的数据和您通过此特定对象对数据所拥有的任何独占访问权限。 稍后可以调用[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，以打开具有相同的或已修改的特性的对象。  
  
 当**记录集**对象关闭时，调用任何需要动态游标的方法将生成错误。  
  
 如果在即时更新模式下编辑正在进行，则调用**Close**方法会生成错误;请先调用[Update](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。 如果在批处理更新模式下关闭**Recordset**对象，则自上次调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)后发生的所有更改都会丢失。  
  
 如果使用[Clone](../../../ado/reference/ado-api/clone-method-ado.md)方法创建打开的**Recordset**对象的副本，则关闭原始或克隆不会影响任何其他副本。  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [Open 和 Close 方法示例（VB）](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法示例（VBScript）](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [打开和关闭方法示例（VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法（ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
