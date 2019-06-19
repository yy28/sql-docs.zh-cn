---
title: GetString 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 14bb7fd2e4a6dd8e6eb8f369342923ce1a9728c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697612"
---
# <a name="getstring-method-ado"></a>GetString 方法 (ADO)
返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)作为字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>返回值  
 返回**记录集**作为字符串值**变体**(BSTR)。  
  
#### <a name="parameters"></a>Parameters  
 *StringFormat*  
 一个[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)值，该值指定如何**记录集**应转换为字符串。 *RowDelimiter*， *ColumnDelimiter*，并*NullExpr*参数只能与一起使用*StringFormat*的**adClipString**。  
  
 *NumRows*  
 可选。 要在转换的行数**记录集**。 如果*NumRows*未指定，或如果它大于中的行的总数**记录集**，然后中的所有行**记录集**转换。  
  
 *ColumnDelimiter*  
 可选。 如果指定，否则 TAB 字符的列之间所用的分隔符。  
  
 *RowDelimiter*  
 可选。 如果指定，否则回车字符的行之间所用的分隔符。  
  
 *NullExpr*  
 可选。 一个表达式，用于代替空值，如果指定，否则为空字符串。  
  
## <a name="remarks"></a>备注  
 行数据，但无架构数据，将保存到字符串。 因此，**记录集**不能使用此字符串重新打开。  
  
 此方法等效于 RDO **GetClipString**方法。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [GetString 方法示例 (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
