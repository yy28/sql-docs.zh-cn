---
title: "LockType 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 231ca93c71468fc46ed7729170b2c58e224b1d6f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="locktype-property-ado"></a>LockType 属性 (ADO)
指示编辑过程上记录放置锁的类型。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值。 默认值是**adLockReadOnly**。  
  
## <a name="remarks"></a>注释  
 设置**LockType**属性在打开之前[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)以指定在打开时，应使用哪种类型的锁定的提供程序。 读取要返回的锁定中处于打开状态的使用类型的属性**记录集**对象。  
  
 提供程序可能不支持所有的锁类型。 如果提供程序不能支持所请求**LockType**设置，它将替换另一个类型的锁定。 若要确定中可用的实际锁定功能**记录集**对象，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法替换**adUpdate**和**adUpdateBatch**.  
  
 **AdLockPessimistic**如果不支持设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 如果设置不支持的值，则不会产生错误;最近支持**LockType**将改为使用。  
  
 **LockType**属性为读/写时**记录集**打开时为已关闭，只读的。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**记录集**对象， **LockType**属性只能设置为**adLockBatchOptimistic**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [游标类型、 LockType，以及 EditMode 属性示例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [游标类型、 LockType 和 EditMode 属性示例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [执行方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
