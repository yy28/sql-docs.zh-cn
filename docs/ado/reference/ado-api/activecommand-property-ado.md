---
title: ActiveCommand 属性 (ADO) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: fef3eac34a624925401eeac2fd82b2f34eaa3a1f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704042"
---
# <a name="activecommand-property-ado"></a>ActiveCommand 属性 (ADO)
指示[命令](../../../ado/reference/ado-api/command-object-ado.md)创建关联对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**Variant** ，其中包含**命令**对象。 默认值为空对象引用。  
  
## <a name="remarks"></a>备注  
 **ActiveCommand**属性是只读的。  
  
 如果**命令**对象不用于创建当前**记录集**，然后**Null**返回对象引用。  
  
 此属性用于查找关联**命令**对象时你可以仅生成**记录集**对象。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [ActiveCommand 属性示例 (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [ActiveCommand 属性示例 (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand 属性示例 （VC + +）](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
