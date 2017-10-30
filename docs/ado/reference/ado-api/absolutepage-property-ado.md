---
title: "AbsolutePage 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 54d429f0920da7f68bcea54b72077b96d6d198f7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="absolutepage-property-ado"></a>AbsolutePage 属性 (ADO)
指示当前记录驻留在哪一页上。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 对于 32 位代码中，设置或返回**长**介于 1 和中的页面数量值[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象 ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md))，或返回类型之一[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 对于 64 位代码，使用提供的存储的 64 位值的数据类型。 例如，你可以使用**长**或另一个值，可以如 DBORDINAL 的 64 位长度。 不要使用**PositionEnum**值，因为它们被限制为 32 位长度。  
  
## <a name="remarks"></a>注释  
 可以使用此属性来标识当前记录所在的页号。 它使用[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)属性上逻辑划分的总的行集计数**记录集**对象插入一系列页面，其中每个具有相等的记录数**PageSize**（除外的最后一页，因此可能具有较少的记录）。 提供程序必须支持相应的功能，此属性才可用。  
  
-   获取或设置时**AbsolutePage**属性、 ADO 使用[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)属性和[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)在一起，如下所示的属性：  
  
-   若要获取**AbsolutePage**，第一次检索 ADO **AbsolutePosition**，，然后将它**PageSize**。  
  
-   若要设置**AbsolutePage**，ADO 移动**AbsolutePosition** ，如下所示： 它乘以**PageSize**通过新**AbsolutePage**值，然后将 1 添加的值。 因此，当前置于**记录集**成功设置后**AbsolutePage**是该页面中的第一个记录。  
  
 如**AbsolutePosition**属性， **AbsolutePage**是基于 1 的并且等于 1 时的当前记录是中的第一个记录**记录集**。 设置此属性将移到特定页的第一个记录。 获取从页总数**PageCount**属性。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AbsolutePage、 PageCount，以及 PageSize 属性示例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount 和 PageSize 属性示例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 属性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)

