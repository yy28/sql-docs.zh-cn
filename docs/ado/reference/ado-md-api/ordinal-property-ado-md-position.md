---
description: Ordinal 属性（ADO MD 位置）
title: 序号属性 (ADO MD 位置) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Position::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: 6efe8b5d-a2d5-43a9-a5ea-f9244f8d4ec9
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d2485e8331a3eee95cfd5937ffbdbd570b2ecdc
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986188"
---
# <a name="ordinal-property-ado-md-position"></a>Ordinal 属性（ADO MD 位置）
唯一标识沿轴的 [位置](./position-object-ado-md.md) 。  
  
## <a name="return-values"></a>返回值  
 返回一个 **长** 整型，并且为只读。  
  
## <a name="remarks"></a>注解  
 [Position](./position-object-ado-md.md)对象的**序号**属性对应于[位置集合中的](./positions-collection-ado-md.md)**位置**的索引。  
  
 使用单元格[集](./cellset-object-ado-md.md)对象的[Item](./item-property-ado-md-cellset.md)属性沿每个轴上的**位置****序号**，可以快速检索单元格。  
  
## <a name="applies-to"></a>适用于  
 [位置对象 (ADO MD)](./position-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [单元集对象 (ADO MD) ](./cellset-object-ado-md.md)   
 [项属性 (ADO MD 单元集) ](./item-property-ado-md-cellset.md)   
 [Ordinal 属性（ADO MD 单元）](./ordinal-property-ado-md-cell.md)