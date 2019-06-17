---
title: 源属性 （ADO 错误） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 89a4597cc846db1bb3bb2fac0a79ec8c2090d9d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711145"
---
# <a name="source-property-ado-error"></a>Source 属性（ADO 错误）
指示最初生成错误的应用程序的对象的名称。  
  
## <a name="return-value"></a>返回值  
 返回**字符串**值，该值指示对象或应用程序的名称。  
  
## <a name="remarks"></a>备注  
 使用**源**上的属性[错误](../../../ado/reference/ado-api/error-object.md)对象，以确定最初生成错误的应用程序的对象的名称。 这可能是该对象的类名称或以编程方式的 id。 对于在 ADO 中的错误，属性值将为**ADODB。** _ObjectName_，其中*ObjectName*触发错误的对象的名称。 对于 ADOX 和 ADO MD，值将为**ADOX。** _ObjectName_并**ADOMD。** _ObjectName_分别。  
  
 基于从的错误文档**源**，[数量](../../../ado/reference/ado-api/number-property-ado.md)，并[说明](../../../ado/reference/ado-api/description-property.md)属性的**错误**对象，您可以编写代码将相应地处理错误。  
  
 **源**属性是只读的**错误**对象。  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 属性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext、 HelpFile 属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 属性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [源属性 （ADO 记录）](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 属性（ADO 记录集）](../../../ado/reference/ado-api/source-property-ado-recordset.md)
