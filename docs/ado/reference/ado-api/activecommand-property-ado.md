---
title: ActiveCommand 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2a2f23360cf3ce032d14af7ca475d5c2c3ea638
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921679"
---
# <a name="activecommand-property-ado"></a>ActiveCommand 属性 (ADO)
指示创建关联[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回一个包含**命令**对象的**变量**。 默认值为 null 对象引用。  
  
## <a name="remarks"></a>备注  
 **ActiveCommand**属性是只读的。  
  
 如果未使用**命令**对象创建当前**记录集**，则返回**Null**对象引用。  
  
 当只给定生成的**记录集**对象时，使用此属性可查找关联的**命令**对象。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActiveCommand 属性示例（VB）](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [ActiveCommand 属性示例（JScript）](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand 属性示例（VC + +）](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
