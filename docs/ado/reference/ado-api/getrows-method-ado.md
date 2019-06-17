---
title: GetRows 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6babeebec1eac78949f0a80eb0701b5b5ba1dcc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694839"
---
# <a name="getrows-method-ado"></a>GetRows 方法 (ADO)
检索的多个记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到一个数组对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>返回值  
 返回**变体**其值是一个二维数组。  
  
#### <a name="parameters"></a>Parameters  
 *行*  
 可选。 一个[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)值，该值指示要检索的记录数。 默认值是**adGetRowsRest**。  
  
 *开始*  
 可选。 一个**字符串**值或**变体**的计算结果为记录书签从其**GetRows**应开始操作。 此外可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
 *Fields*  
 可选。 一个**变体**表示单个字段名称或序号位置或数组的字段名称或序号位置编号。 ADO 仅返回的数据在这些字段中。  
  
## <a name="remarks"></a>备注  
 使用**GetRows**方法将复制的记录**记录集**到二维数组。 第一个下标标识字段，第二个标识的记录号。 *数组*变量自动划分为正确大小**GetRows**方法返回的数据。  
  
 如果未指定的值*行*自变量， **GetRows**方法自动检索中的所有记录**记录集**对象。 如果请求超过可用，数量的记录，则**GetRows**返回仅可用记录数。  
  
 如果**记录集**对象支持书签，您可以指定在哪条记录**GetRows**方法应开始检索数据，通过将该记录的值传递[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)中的属性*启动*参数。  
  
 如果你想要限制字段的**GetRows**调用返回时，可以传递单个字段名称/编号或数组中的字段名称/数字*字段*参数。  
  
 调用后**GetRows**下, 一个未读的记录将成为当前的记录，或[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性设置为**True**如果没有更多记录。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [GetRows 方法示例 (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 方法示例 (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
