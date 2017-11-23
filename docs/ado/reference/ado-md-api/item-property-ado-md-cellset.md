---
title: "项属性 （ADO MD 单元集） |Microsoft 文档"
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
- Item
- Cellset::Item
helpviewer_keywords: Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34b0d4a5f2104d625091a0b39f1b009b933bedbe
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="item-property-ado-md-cellset"></a>Item 属性 （ADO MD 单元集）
检索从单元格[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)使用其坐标。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parameters  
 *位置*  
 A **VariantArray**唯一指定单元格的值。 *位置*可以是以下之一：  
  
-   位置数字数组  
  
-   成员名称的数组  
  
-   序号位置  
  
## <a name="remarks"></a>注释  
 使用**项**属性以返回[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)对象内[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。 如果**项**属性找不到对应的单元格*位置*自变量，就会出错。  
  
 **项**属性是其默认属性**单元集**对象。 以下语法窗体是可互换的：  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>注释  
 *位置*参数指定要返回的单元格。 你可以指定单元格的序号位置或每个轴位置。 在指定的每个轴的位置的单元格时，你可以指定位置的数字值或成员的每个位置的名称。  
  
 序号位置是唯一标识一个单元格内的数字**单元集**。 单元格中的编号从概念上讲，**单元集**就像**单元集**已*p*-维数组，其中*p*是的轴数。 单元按行优先的顺序排列。 下面是用于计算的单元格序号的公式：  
  
 如果传递的成员名称作为字符串应用于**项**，则必须列出成员以升序数值轴标识符。 在轴中，必须以维度嵌套的升序列出成员 — 也就是说，最外面的维度成员最先，然后跟随内部维度的成员。 每个维度应由单独的字符串，并且应该用逗号分隔的成员字符串的列表。  
  
> [!NOTE]
>  数据提供程序可能不支持按成员名称检索单元格。 请参阅你的提供程序的详细信息的文档。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [单元格对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
