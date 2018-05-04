---
title: GetRows 方法 (ADO) |Microsoft 文档
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
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efe7a21a26e99d089c64fcd3a627c693c5f7de09
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getrows-method-ado"></a>GetRows 方法 (ADO)
检索的多个记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到一个数组对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>返回值  
 返回**Variant**的值是二维数组。  
  
#### <a name="parameters"></a>Parameters  
 *行*  
 選擇性。 A [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)值，该值指示要检索的记录数。 默认值是**adGetRowsRest**。  
  
 *开始*  
 選擇性。 A**字符串**值或**Variant**计算结果为记录的书签从其**GetRows**应开始操作。 你还可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
 *Fields*  
 選擇性。 A **Variant**表示单个字段名称或序号位置或数组的字段名称或序号位置编号。 ADO 仅返回的数据在这些字段中。  
  
## <a name="remarks"></a>注释  
 使用**GetRows**方法以从记录中复制**记录集**到二维数组。 第一个下标标识字段，第二个标识记录编号。 *数组*变量自动尺寸到正确大小时**GetRows**方法返回的数据。  
  
 如果未指定的值*行*自变量， **GetRows**方法自动检索中的所有记录**记录集**对象。 如果请求更多记录多于可用， **GetRows**返回仅可用的记录数。  
  
 如果**记录集**对象支持书签，你可以指定在哪一记录**GetRows**方法应开始检索数据，通过将该记录的值传递[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)中的属性*启动*自变量。  
  
 如果你想要限制字段， **GetRows**调用返回时，可以传递单个字段名称/数或字段名称/中的数字数组*字段*自变量。  
  
 调用后**GetRows**下, 一步的未读的记录将成为当前记录，或[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性设置为**True**如果没有更多记录。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [GetRows 方法示例 (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [GetRows 方法示例 (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
