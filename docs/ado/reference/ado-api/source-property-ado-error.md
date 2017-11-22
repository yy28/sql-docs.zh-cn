---
title: "Source 属性 （ADO 错误） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords: Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a0f34bfbe5c4d7fa251316658dd76878c7b53c5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="source-property-ado-error"></a>源属性 （ADO 错误）
指示最初生成了错误的应用程序的对象的名称。  
  
## <a name="return-value"></a>返回值  
 返回**字符串**值，该值指示对象或应用程序的名称。  
  
## <a name="remarks"></a>注释  
 使用**源**属性[错误](../../../ado/reference/ado-api/error-object.md)对象确定最初生成了错误的应用程序的对象的名称。 这可能是对象的类名称或以编程方式的 id。 属性值将是在 ADO 中的错误， **ADODB。***ObjectName*，其中*ObjectName*是触发错误的对象的名称。 对于 ADOX ADO MD，则值将是**ADOX。***ObjectName*和**ADOMD。***ObjectName，*分别。  
  
 基于的错误文档**源**，[数](../../../ado/reference/ado-api/number-property-ado.md)，和[说明](../../../ado/reference/ado-api/description-property.md)属性**错误**对象，你可以编写代码将相应地处理错误。  
  
 **源**属性是只读的**错误**对象。  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 属性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext，HelpFile 属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 属性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [源属性 （ADO 记录）](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 属性（ADO 记录集）](../../../ado/reference/ado-api/source-property-ado-recordset.md)
