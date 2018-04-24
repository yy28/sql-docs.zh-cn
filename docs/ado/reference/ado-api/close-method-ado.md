---
title: Close 方法 (ADO) |Microsoft 文档
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
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 996da92c866789b91a317c152449f7ca2540d273
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="close-method-ado"></a>Close 方法 (ADO)
关闭打开的对象和任何从属对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>注释  
 使用**关闭**方法来关闭[连接](../../../ado/reference/ado-api/connection-object-ado.md)、[记录](../../../ado/reference/ado-api/record-object-ado.md)、[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，或[流](../../../ado/reference/ado-api/stream-object-ado.md)对象若要释放任何关联的系统资源。 关闭对象不会删除它从内存;你可以更改其属性设置，以后再打开它。 若要完全消除从内存的对象，关闭对象并将对象变量设置为*执行任何操作*（在 Visual Basic 中)。  
  
## <a name="connection"></a>连接  
 使用**关闭**方法来关闭**连接**对象也会关闭任何活动**记录集**与连接关联的对象。 A[命令](../../../ado/reference/ado-api/command-object-ado.md)与关联的对象**连接**将会保留你在将关闭的对象，但将不再与它关联**连接**对象; 即，其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性将设置为**执行任何操作**。 此外，**命令**对象的[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)将清除集合的任何提供程序定义的参数。  
  
 你可以稍后调用[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法才能重新建立与相同数据源或其他数据源的连接。 虽然**连接**对象已关闭，则调用需要与数据源的开放连接的任何方法将产生错误。  
  
 关闭**连接**对象时没有打开的**记录集**连接上的对象将回滚所有挂起的更改中的所有**记录集**对象。 显式关闭**连接**对象 (调用**关闭**方法) 在事务执行过程中进度将生成错误。 如果**连接**对象在事务正在进行时超出范围，ADO 自动回滚事务。  
  
## <a name="recordset-record-stream"></a>记录集，则请记录，流式传输  
 使用**关闭**方法来关闭**记录集**，**记录**，或**流**对象版本关联的数据和任何的独占访问权你可能获得了对通过该特定对象的数据。 你可以稍后调用[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法重新打开具有相同，或修改后，对象属性。  
  
 虽然**记录集**对象已关闭，则调用需要实时光标任何方法将产生错误。  
  
 如果正在处于立即更新模式下时进行了编辑，则调用**关闭**方法会生成错误; 而应调用[更新](../../../ado/reference/ado-api/update-method.md)或[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一个。 如果你关闭**记录集**对象在批处理更新模式下，自上次操作后的所有更改[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)调用都将丢失。  
  
 如果你使用[克隆](../../../ado/reference/ado-api/clone-method-ado.md)方法创建的打开副本**记录集**对象，则关闭原始或克隆不会影响任何其他副本。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [打开和关闭方法的示例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [打开和关闭方法的示例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [打开和关闭方法的示例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
