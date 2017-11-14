---
title: "Number 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8d5567283a62a31842185afce7682d3641d6fcc4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="number-property-ado"></a>Number 属性 (ADO)
指示唯一标识的数字[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**长**可能与之一相对应的值[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)常量。  
  
## <a name="remarks"></a>注释  
 使用**数**属性以确定哪一类错误发生。 属性的值是唯一的编号对应于错误条件。  
  
 [错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合以十六进制格式 (例如，0x80004005) 或 long 类型的值 (例如，2147467259) 返回的 HRESULT。 可以由基础组件，如 OLE DB 或甚至 OLE 本身引发这些 Hresult。 有关这些编号的详细信息，请参阅[错误 (OLE DB)](http://msdn.microsoft.com/en-us/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd)中[OLE DB 程序员参考](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)*。*  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 属性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext，HelpFile 属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [源属性 （ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)

