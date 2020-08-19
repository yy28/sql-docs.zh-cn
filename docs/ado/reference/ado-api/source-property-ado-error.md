---
description: Source 属性（ADO 错误）
title: " (ADO 错误) 的源属性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fa7fc5c5098b6e429960e5d72702111abab55ac2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442049"
---
# <a name="source-property-ado-error"></a>Source 属性（ADO 错误）
指示最初生成错误的对象或应用程序的名称。  
  
## <a name="return-value"></a>返回值  
 返回一个 **字符串** 值，该值指示对象或应用程序的名称。  
  
## <a name="remarks"></a>备注  
 使用[错误](../../../ado/reference/ado-api/error-object.md)对象上的**Source**属性来确定最初生成错误的对象或应用程序的名称。 这可能是对象的类名或编程 ID。 对于 ADO 中的错误，属性值将为 **adodb.recordset。**_Objectname_，其中 *objectname* 是触发错误的对象的名称。 对于 ADOX 和 ADO MD，该值将为 **adox。**_ObjectName_ 和 **ADOMD。**_ObjectName_。  
  
 根据**错误**对象的 "**源**"、"[编号](../../../ado/reference/ado-api/number-property-ado.md)" 和 "[说明](../../../ado/reference/ado-api/description-property.md)" 属性中的错误文档，您可以编写将相应处理错误的代码。  
  
 对于**Error**对象， **Source**属性是只读的。  
  
## <a name="applies-to"></a>适用于  
 [Error 对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [Description、HelpContext、"帮助"、"NativeError"、"Number"、"Source" 和 "SQLState Properties" 示例 (VB) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、"帮助"、"NativeError"、"Number"、"Source" 和 "SQLState Properties" 示例 (VC + +) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 属性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext，帮助的属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [ADO (的数字属性) ](../../../ado/reference/ado-api/number-property-ado.md)   
 [ADO 记录 (源属性) ](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 属性（ADO 记录集）](../../../ado/reference/ado-api/source-property-ado-recordset.md)
