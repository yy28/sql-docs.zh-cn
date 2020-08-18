---
description: Ordinal 属性（ADO MD 单元）
title: 序号属性 (ADO MD 单元格) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: rothja
ms.author: jroth
ms.openlocfilehash: 55db23316b4d920154f00aa3b03fb101b2382483
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440809"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal 属性（ADO MD 单元）
按单元格集中的位置唯一标识 [单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md) 。  
  
## <a name="return-values"></a>返回值  
 返回一个 **长** 整型，并且为只读。  
  
## <a name="remarks"></a>备注  
 单元格的序号值用于唯一标识单元格集中的单元格。 从概念上讲，单元在单元集中编号，就如同单元集 *是一个二维*数组，其中 *p* 是 [轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)的数目。 单元按行优先顺序从零开始编号。 下面是用于计算单元序号的公式：  
  
 单元格的序号值可以与单元格[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象的[Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性一起使用，以快速检索[单元](../../../ado/reference/ado-md-api/cell-object-ado-md.md)。  
  
## <a name="applies-to"></a>适用于  
 [单元对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (VBScript) 的轴示例 ](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [单元集对象 (ADO MD) ](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [项属性 (ADO MD 单元集) ](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal 属性（ADO MD 位置）](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
