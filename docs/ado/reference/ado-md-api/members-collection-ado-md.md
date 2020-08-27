---
description: 成员集合 (ADO MD)
title: 成员集合 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: rothja
ms.author: jroth
ms.openlocfilehash: e0f12771ebb759a658d5e3c99244755c4daa99b0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986378"
---
# <a name="members-collection-ado-md"></a>成员集合 (ADO MD)
包含某一级别的 [成员](./member-object-ado-md.md) 对象或沿某个轴的位置。  
  
## <a name="remarks"></a>注解  
 **成员**集合用于包含以下类型的成员：  
  
-   构成多维数据集中的某一级别的成员。 它们包含在[Level](./level-object-ado-md.md)对象的**Members**集合中。 例如，使用 [多维架构和数据的概述](../../guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)中的示例，国家/地区级别的四个成员为加拿大、美国、英国和德国。  
  
-   作为层次结构中特定成员的子级的成员。 父**成员**对象的[子](./children-property-ado-md.md)属性返回这些成员。 例如，再次使用同一个示例，加拿大成员的两个子成员分别为加拿大东部和加拿大西部。  
  
-   定义沿 [单元集](./cellset-object-ado-md.md)的轴的特定位置的成员。 使用单元集从 [处理多维数据](../../guide/multidimensional/working-with-multidimensional-data.md) 作为示例，x 轴上第一个位置的两个成员为 "情人" 和 "西雅图"。 [位置](./position-object-ado-md.md)对象的**members**集合包含这些成员。  
  
 **成员** 是标准 ADO 集合。 通过集合的属性和方法，你可以执行以下操作：  
  
-   获取集合中具有 [Count](../ado-api/count-property-ado.md) 属性的对象的数目。  
  
-   返回集合中具有默认 [项](../ado-api/item-property-ado.md) 属性的对象。  
  
-   用 [Refresh](../ado-api/refresh-method-ado.md) 方法更新集合中的对象。  
  
 本部分包含以下主题。  
  
-   [属性、方法和事件](./members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (VBScript) 成员示例 ](./members-example-vbscript.md)   
 [成员对象 (ADO MD)](./member-object-ado-md.md)