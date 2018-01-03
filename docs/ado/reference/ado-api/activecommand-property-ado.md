---
title: "ActiveCommand 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset20::ActiveCommand
helpviewer_keywords: ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e5384aff9ee8646493d26272cdeaae33ab49157
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="activecommand-property-ado"></a>ActiveCommand 属性 (ADO)
指示[命令](../../../ado/reference/ado-api/command-object-ado.md)创建关联的对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**Variant**包含**命令**对象。 默认值为空对象引用。  
  
## <a name="remarks"></a>Remarks  
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
