---
title: 项属性 （ADO MD 单元集） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 68191a6d6e8541eb89a7c4be3c6820b2627fc90a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709234"
---
# <a name="item-property-ado-md-cellset"></a>Item 属性（ADO MD 单元集）
检索从单元格[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)使用其坐标。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parameters  
 *位置*  
 一个**VariantArray**唯一指定单元格的值。 *位置*可以是以下之一：  
  
-   位置数字数组  
  
-   成员名称的数组  
  
-   序号位置  
  
## <a name="remarks"></a>备注  
 使用**项**属性以返回[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)对象内[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。 如果**项**属性找不到对应的单元格*位置*参数，就会出错。  
  
 **项**属性是默认属性**单元集**对象。 下面的语法形式是可互换的：  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>备注  
 *位置*参数指定要返回的单元格。 您可以指定按序号位置或每个轴的位置的单元格。 在指定的每个轴的位置的单元格时，可以指定位置的数值或每个位置的成员的名称。  
  
 序号位置是唯一标识一个单元格内的数字**单元集**。 从概念上讲，单元以编号**单元集**像**单元集**已*p*-维数组，其中*p*是轴的数目。 单元按行优先的顺序排列。 下面是用于计算单元格的序号的公式：  
  
 如果传递的成员名称作为字符串应用于**项**，成员必须以递增的数值轴标识符的顺序列出。 在一条轴必须在维度嵌套的升序列出成员-，即最外面的维度成员在前后, 跟的内部维度成员。 应通过单独的字符串，表示每个维度和成员字符串列表应该用逗号分隔。  
  
> [!NOTE]
>  数据访问接口可能不支持按成员名称检索单元格。 请参阅你的详细信息的提供商的文档。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>请参阅  
 [Cell 对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
