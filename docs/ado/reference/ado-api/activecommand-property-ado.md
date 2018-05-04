---
title: ActiveCommand 属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aa86180edc4117e89863bb232a2faa95d010272
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="activecommand-property-ado"></a>ActiveCommand 属性 (ADO)
指示[命令](../../../ado/reference/ado-api/command-object-ado.md)创建关联的对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**Variant**包含**命令**对象。 默认值为空对象引用。  
  
## <a name="remarks"></a>注释  
 **ActiveCommand**属性是只读的。  
  
 如果**命令**对象未用于创建当前**记录集**，则**Null**返回对象引用。  
  
 此属性用于查找关联**命令**对象给定仅生成时**记录集**对象。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActiveCommand 属性示例 (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [ActiveCommand 属性示例 (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand 属性示例 （VC + +）](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
